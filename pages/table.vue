<template>
  <div>
    <v-card color="#117c00">
      <v-card-title>
        <v-spacer></v-spacer>
        <v-text-field
          v-model="search"
          append-icon="mdi-magnify"
          label="Search"
          single-line
          hide-details
        ></v-text-field>
      </v-card-title>
      <v-data-table
        :headers="headers"
        :items="desserts"
        :items-per-page="5"
        :search="search"
        class="elevation-3"
      ></v-data-table>
    </v-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      search: '',
      headers: [
        {
          text: 'Booking name',
          align: 'start',
          sortable: false,
          value: 'name',
        },
        {
          text: 'E-mail',
          value: 'email',
        },
        {
          text: 'Phone Number',
          value: 'phone',
        },
        {
          text: 'Address',
          value: 'address.add',
        },
        {
          text: 'Tombon',
          value: 'address.sub_district',
        },
        {
          text: 'Amphoe',
          value: 'address.district',
        },
        {
          text: 'Province',
          value: 'address.province',
        },
        {
          text: 'Number of rooms',
          value: 'room',
        },
        {
          text: 'Number of people',
          value: 'costumers',
        },
        {
          text: 'Book a date',
          value: 'date_in',
        },
        {
          text: 'Up to date',
          value: 'date_out',
        },
      ],
    }
  },
  computed: {
    desserts: {
      get() {
        return this.$nuxt.$store.state.list
      },
    },
    // listdata: {},
  },
}
</script>
