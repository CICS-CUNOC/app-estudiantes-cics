<template>
  <v-app :theme="theme">
    <v-app-bar :elevation="elevation" class="app-bar">
      <template #prepend>
        <v-btn
          :icon="drawer ? 'mdi-backburger' : 'mdi-menu'"
          @click="drawer = !drawer"
        />
      </template>

      <v-app-bar-title class="mt-n1">
        <strong>Administración </strong> - CICS APP
        <!-- <v-spacer /> -->
      </v-app-bar-title>

      <div class="app-bar__user-info">
        <!-- Dashboard action (regular and admin) -->
        <span>
          <strong>{{ user?.first_name }} {{ user?.last_name }}</strong>
        </span>
        <v-tooltip text="Cerrar sesión" location="bottom">
          <template #activator="{ props }">
            <v-btn v-bind="props" class="app-bar__avatar" icon @click="logout">
              <v-icon> mdi-logout-variant </v-icon>
            </v-btn>
          </template>
        </v-tooltip>
      </div>
    </v-app-bar>

    <v-navigation-drawer
      v-model="drawer"
      :width="$vuetify.display.mdAndUp ? 340 : 300"
    >
      <AdminNavigator @theme="() => changeTheme()" />
    </v-navigation-drawer>

    <v-main>
      <v-container class="page-v-container">
        <NuxtPage :theme="theme" />
      </v-container>
    </v-main>
  </v-app>
</template>

<script lang="ts" setup>
import AdminNavigator from '~/components/partials/AdminNavigator.vue'
import { useStaffAuthStore } from '~/stores/staff-auth'
import { useConfigsStore } from '~/stores/config'
import { useAuthStore } from '~/stores/auth'

const { theme } = storeToRefs(useConfigsStore())
const { user, authenticated } = storeToRefs(useStaffAuthStore())

const { logout } = useAuthStore()
const { switchTheme, changeTheme } = useConfigsStore()

const elevation = computed(() => (drawer.value ? 2 : 0))

const drawer = ref(false)
const currentPage = ref('')
</script>
<style lang="scss" scoped>
.app-bar {
  padding: 0 1rem 0 0;
  &__user-info {
    display: flex;
    flex-direction: row;
    align-items: center;
    gap: 1rem;
  }
  &__avatar {
    cursor: pointer;
    outline: 1px solid #ccc;
    transition: outline 0.07s linear;

    &:hover {
      outline: 3px solid #ccc;
    }
  }
}
</style>
