<template>
    <div>
    <v-card>
      <v-card-title>
        Filter the API here ->
      <v-spacer></v-spacer>
      <v-text-field
        v-model="search"
        append-icon="search"
        label="Filter"
        single-line
        hide-details
      ></v-text-field>
      </v-card-title>
      <v-data-table v-model="selected" :headers="headers" :items="results" :search="search">
      <template slot="items" slot-scope="props">
        <tr @click="showAlert(props.item)">
          <td>{{ props.item.API }}</td>
          <td>{{ props.item.API }}</td>
          <td>{{ props.item.desc }}</td>
        </tr>
      </template>
      <v-alert slot="no-results" :value="true" color="error" icon="warning">
          Your search for "{{ search }}" found no results.
        </v-alert>
    </v-data-table>
    </v-card>
    
    </div>
</template>

<script>
export default {
    name: 'Result',
    props: {
        results: {
          type: Array,
          required: true
        }
    },
    methods: {
      showAlert(a) {
        if (event.target.classList.contains('btn__content')) return;
        alert('Alert! \n' + a.name);
      }
    },
    data() {
      return {
        selected: [],
        search: '',
        headers: [
          { text: "API Name", value: "API"},
          { text: "API URL", value: "Link"},
          { text: "API Description", value: "Description"}
        ]
      }
    }
}
</script>

<style scoped>

</style>