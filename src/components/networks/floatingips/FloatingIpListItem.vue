<template>
  <tr>
    <td>{{ floatingip.floating_ip_address }}</td>
    <td>{{ floatingip.description || '-' }}</td>
    <td>{{ floatingip.fixed_ip_address }}</td>
    <td>
      <!-- XXX This whole template "thingy" could be placed in a computed method -->
      <template v-for="network in networks">
        {{ network.id === floatingip.floating_network_id ? network.name : '' }}
      </template>
    </td>
    <td>{{ floatingip.status }}</td>
    <td>
      <div class="btn-group" role="group" aria-label="Actions">
        <btn
          class="mr-1"
          is="floating-ip-list-item-button-associate"
          v-bind:floatingip="floatingip">
        </btn>
        <btn
          is="floating-ip-list-item-button-release"
          v-bind:floatingip="floatingip">
        </btn>
      </div>
    </td>
  </tr>
</template>

<script>
import FloatingIpListItemButtonAssociate from './FloatingIpListItemButtonAssociate'
import FloatingIpListItemButtonRelease from './FloatingIpListItemButtonRelease'
export default {
  name: 'FloatingIpListItem',
  components: {
    FloatingIpListItemButtonAssociate,
    FloatingIpListItemButtonRelease
  },
  props: {
    floatingip: Object
  },
  computed: {
    networks () {
      return this.$store.state.networks.networks
    }
  },
  mounted () {
    console.log('FloatingIpListItem created and mounted for floating IP with id ' + this.floatingip.id)
  }
}
</script>
