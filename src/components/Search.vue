<template>
  <v-app>
    <h1> Search Page</h1>
    <v-form
    ref="form"
    v-model="valid"
    lazy-validation
  >
    <v-text-field
    v-model="term"
    type="search"
      label="Enter the keyword !"
    ></v-text-field>

    <v-btn class="mr-5 ml-5" color="success" @click="search">Search</v-btn>
    <div v-if="results">
      <Result :results="results"/>
    </div>
  </v-form>
  
</v-app>
</template>

<script>
import Result from './Result'
  export default {
    name: 'Search',
    created() {
      this.search()
    },
    components: {
     Result
    },
    data() {
      return {

        term: '',
        results:null,
        headers: [
        {
          text: 'API Name',
          align: 'left',
          sortable: false,
          value: 'name'
        },
        { text: 'API link', value: 'link' },
        { text: 'API Description', value: 'desc' },
      ]
      }
    },
    methods: {
      search() {
        if(this.term.trim() === '') return;
        console.log('Searched for ' + this.term);
        fetch(`https://api.publicapis.org/entries?title=${encodeURIComponent(this.term)}`)
          .then(res => res.json())
          .then(res => {
            console.log('Results', res);
            this.results = res.entries;
          })
      }
    }
  }
</script>

<style scoped>

</style>