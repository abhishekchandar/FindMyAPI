<template>
  <v-app>
    <v-flex >
        <v-toolbar color="cyan" dark>
          <v-toolbar-side-icon></v-toolbar-side-icon>
          <v-toolbar-title>FindMyAPI</v-toolbar-title>
          <v-spacer></v-spacer>
          <v-btn icon>
            <v-icon>search</v-icon>
          </v-btn>
        </v-toolbar>
     <v-layout class="py-5 mt-auto">
      <v-flex xs12 sm6 offset-sm3 >
        <v-card>
          <v-card-title primary-title>
            <div>
              <h3 class="headline mb-0">Search the API here:</h3>
              <div> {{ card_text }} </div>
            </div>
          </v-card-title>
        <v-text-field class="py-3 mx-3"
            label="Enter the keyword"
            single-line
            v-model="term"
            type="search"
            outlined
            value="term"
          ></v-text-field>
  
          <v-card-actions>
            <v-btn flat color="success" @click="search">Search</v-btn>
          </v-card-actions>
          
              </v-card>
      <div v-if="results">
            <Result :results="results"/>
      </div>
      <div v-else>
        <v-alert :value="true" color="error" icon="warning">
          Your search for "{{ term }}" found no results.
        </v-alert>
        </div>
            
      </v-flex>
     </v-layout>
    </v-flex>
    <v-footer class="pa-3">
    <v-spacer></v-spacer>
    <div>&copy; {{ new Date().getFullYear() }}</div>
  </v-footer>
</v-app>
</template>

<script src="https://cdn.jsdelivr.net/npm/axios@0.12.0/dist/axios.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/lodash@4.13.1/lodash.min.js"></script>

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
        if(this.term.trim() === '') {
          return;
        }
        fetch(`https://api.publicapis.org/entries?title=${encodeURIComponent(this.term)}`)
          .then(res => res.json())
          .then(res => {
            console.log('Results', res);
            this.results = res.entries;
          })
          .catch(function(error) {
            this.comment = 'Error! Could not reach the API.' + error
          })
      }
    }
  }
</script>

<style scoped>

</style>