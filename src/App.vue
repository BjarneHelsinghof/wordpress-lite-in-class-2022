<template>
  <v-app>
    <v-card>
      <v-layout>
        <!-- add permanent to have it always be shown -->
        <v-navigation-drawer permanent expand-on-hover rail>
          <v-list>
            <v-list-item prepend-avatar="https://randomuser.me/api/portraits/men/22.jpg" title="Admin"
              subtitle="admin@admin.com"></v-list-item>
          </v-list>

          <v-divider></v-divider>

          <v-list density="compact" nav>
            <router-link to="/navguardviewtest">
              <v-list-item prepend-icon="mdi-lock" title="navguard" value="login"></v-list-item>
            </router-link>
            <router-link to="/">
              <v-list-item prepend-icon="mdi-post" title="discussion forum" value="myfiles"></v-list-item>
            </router-link>
            <router-link to="/about">
              <v-list-item prepend-icon="mdi-plus-box" title="make new post" value="shared"></v-list-item>
            </router-link>

            <router-link to="/editpostsview">
              <v-list-item prepend-icon="mdi-pencil-outline" title="Edit posts" value="starred"></v-list-item>
            </router-link>

            <router-link to="/login">
              <v-list-item prepend-icon="mdi-login" title="Login" value="login"></v-list-item>
            </router-link>



            <span v-if="isLoggedin">
              <v-btn block prepend-icon="mdi-logout" color="error" @click="logOut()">
              </v-btn>

            </span>
          </v-list>
        </v-navigation-drawer>

        <v-main class="ma-2">
          <Suspense>
            <router-view></router-view>
          </Suspense>
        </v-main>
      </v-layout>
    </v-card>
  </v-app>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { getAuth, onAuthStateChanged } from 'firebase/auth'

import useUsers from '@/modules/useUsers'

const { logOut } = useUsers()

let auth
const isLoggedin = ref(false)

onMounted(() => {
  auth = getAuth();
  onAuthStateChanged(auth, (user) => {
    if (user) {
      isLoggedin.value = true
    }
    else {
      isLoggedin.value = false
    }
  })
})
</script>


<style lang="scss">
.v-main {
  min-height: 100vh;
}

.v-layout {
  background-color: lavender;
}

.v-navigation-drawer__content {
  background-color: bisque;
}
</style>