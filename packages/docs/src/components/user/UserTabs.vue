<template>
  <v-tabs color="primary">
    <v-tab
      v-for="(tab, i) in tabs"
      :key="i"
      class="text-none text-body-2 font-weight-regular"
      v-bind="tab"
    />
  </v-tabs>
</template>

<script setup>
  // Composables
  import { useAuthStore, useUserStore } from '@vuetify/one'

  // Utilities
  import { computed } from 'vue'
  import { rpath } from '@/util/routes'

  const auth = useAuthStore()
  const user = useUserStore()

  const tabs = computed(() => {
    const array = [
      {
        prependIcon: 'mdi-view-dashboard-outline',
        text: 'Dashboard',
        to: rpath('/user/dashboard/'),
      },
      {
        prependIcon: 'mdi-cog-outline',
        text: 'Options',
        to: rpath('/user/options/'),
      },
    ]

    if (auth.user && user.dev) {
      array.push({
        prependIcon: '$vuetify',
        text: 'Subscriptions',
        to: rpath('/user/subscriptions/'),
      })
    }

    return array
  })
</script>
