<template>
  <v-app :theme="theme">
    <v-main class="main-content">
      <v-container class="main-content__page">
        <NuxtPage />
      </v-container>
    </v-main>
  </v-app>
</template>

<script lang="ts" setup>
import { useConfigsStore } from '~/stores/config'

const { theme } = storeToRefs(useConfigsStore())
</script>
<style lang="scss" scoped>
.main-content {
  &__page {
    padding: 0 !important;
    height: 100%;
    width: 100%;
    min-height: 100vh;
  }
}

@import '@/assets/styles/main.scss';
</style>
