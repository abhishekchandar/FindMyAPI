<template>
    <div>
        <v-simple-table>
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-left">API Name</th>
            <th class="text-left">API URL</th>
            <th class="text-left">API Description</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="result in results" :key="result.Link">
            <td>{{ result.API }}</td>
            <td><a :href="`${result.Link}`" target="_new">{{ result.Link }}</a></td>
            <td>{{result.Description}}</td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
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
    data () {
    return {
      headers: [
        {
          text: 'API Name',
          align: 'left',
          sortable: false,
          value: 'name'
        },
        { text: 'API link', value: 'link' },
        { text: 'API Description', value: 'desc' },
      ],
      desserts: [
        {
          name: 'Frozen Yogurt',
          link: `www.google.com`,
          desc: `Google is a tech company.`
        },
        {
          name: 'Ice cream sandwich',
          link: `www.google.com`,
          desc: `Google is a tech company.`
        },
        {
          name: 'Eclair',
          link: `www.google.com`,
          desc: `Google is a tech company.`
        },
        {
          name: 'Cupcake',
          link: `www.google.com`,
          desc: `Google is a tech company.`
        }
      ]
    }
  }
}
</script>

<style scoped>

</style>