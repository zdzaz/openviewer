<template>
  <div class="container table-responsive">
    <b-table
      bordered
      :per-page="perPage"
      :current-page="currentPage"
      striped
      hover
      :items="roles"
      :fields="fields"
    />
    <b-pagination
      v-model="currentPage"
      :total-rows="rows"
      :per-page="perPage"
      aria-controls="my-table"
      align="right"
    />
  </div>
</template>

<script>
import moment from 'moment'
export default {
  name: 'RolesList',
  data () {
    return {
      perPage: 5,
      currentPage: 1,
      fields: [
        {
          key: 'metadata.name',
          label: 'Name'
        },
        {
          key: 'metadata.creationTimestamp',
          label: 'Created',
          formatter: 'created'
        },
        {
          key: 'metadata.uid',
          label: 'UID'
        }
      ]

    }
  },
  computed: {
    roles () {
      return this.$store.state.roles.roles
    },
    rows () {
      return this.roles.length
    }
  },
  methods: {
    created: function (timestamp) {
      return moment(timestamp).fromNow()
    }
  }
}
</script>

<style scoped>
.opacity {
  opacity: 0.8;
}
</style>
