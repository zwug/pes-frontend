<template>
  <div>
    <h1>Scouts</h1>
    <vue-autosuggest
      v-model="query"
      :suggestions="options" 
      @selected="onSelected"
      :input-props="inputProps">
    </vue-autosuggest>
  </div>
</template>

<script>
import { VueAutosuggest } from 'vue-autosuggest';

export default {
  name: 'Scouts',
  components: {
    VueAutosuggest,
  },
   props: {
    onScoutSelected: { type: Function },
  },
  data: function() {
    return {
      inputProps: {id:'autosuggest__input', placeholder:'Do you feel lucky, punk?'},
      onSelected: selected => {
        const scout = this.scouts.find(({name}) => selected.item === name);
        this.$emit('onScoutSelected', scout)
      },
      query: '',
      suggestions: [{data: []}],
      options: [{data: []}],
      scouts: [],
    }
  },
  computed: {
    filteredOptions() {
      return [
        { 
          data: this.suggestions[0].data.filter(option => {
            return option.toLowerCase().indexOf(this.query.toLowerCase()) > -1;
          })
        }
      ];
    }
  },
  watch: {
    query: function(newQuery, oldQuery) {      
      fetch(`${process.env.VUE_APP_BACKEND_URL}/scouts?name=${newQuery}`)
      .then((response) => response.json())
      .then((json) => {
        this.options = [{data: json.map(({name}) => name)}]
        this.scouts = json;
      });
    }
  }
}
</script>

<style>
.autosuggest__results ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

#autosuggest__input,
.autosuggest__results-container {
  width: 480px;
}

#autosuggest__input {
  border: 1px solid #000000;
  border-radius: 4px;
  box-sizing: border-box;
  padding: 8px;
  font-size: 16px;
}

.autosuggest__results {
  background: #ffffff;
}

.autosuggest__results-item {
  margin: 2px 0;
  padding: 8px;
  color: #000000;
  cursor: pointer;
}

.autosuggest__results-item:hover {
  background: #d3d3d3;
}

#autosuggest__input:focus {
  outline-color: #ffffff;
}

</style>
