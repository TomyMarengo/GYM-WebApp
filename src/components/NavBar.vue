<template>
  <div>
    <v-app-bar class="hidden-md-and-up" color="secondary" dark>
      <v-btn class="no-active" dark text to="/">
        <v-icon class="mr-2" color="primary">mdi-dumbbell</v-icon>
        <v-toolbar-title class="pa-0 primary--text">ENTRENAGRATIS.ES</v-toolbar-title>
      </v-btn>
      <v-spacer></v-spacer>
      <v-app-bar-nav-icon color="primary" @click="drawer = true"></v-app-bar-nav-icon>
    </v-app-bar>

    <v-navigation-drawer v-if="isDrawer" v-model="drawer" absolute temporary right color="secondary">
      <v-list nav dense>
        <v-list-item-group v-model="group" active-class="primary--text text--accent-4">
          <v-list-item to="/" dark >
            <v-list-item-icon>
              <v-icon>mdi-home</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Inicio</v-list-item-title>
          </v-list-item>
          <v-list-item to="/rutinas" dark>
            <v-list-item-icon>
              <v-icon>mdi-dumbbell</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Entrenamientos</v-list-item-title>
          </v-list-item>
          <v-list-item to="/ingresar" v-if="!isLoggedIn" dark>
            <v-list-item-icon>
              <v-icon>mdi-account</v-icon>
            </v-list-item-icon>
            <v-list-item-title >Iniciar Sesión</v-list-item-title>
          </v-list-item>
          <v-list-item to="/registrarse" v-if="!isLoggedIn" dark>
            <v-list-item-icon>
              <v-icon>mdi-account-arrow-left</v-icon>
            </v-list-item-icon>
            <v-list-item-title >Registrarse</v-list-item-title>
          </v-list-item>
          <v-list-item to="/perfil" v-if="isLoggedIn" dark>
            <v-list-item-icon>
              <v-icon>mdi-account-arrow-right</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Mi perfil</v-list-item-title>
          </v-list-item>
          <v-list-item v-if="isLoggedIn" dark>
            <v-list-item-icon>
              <v-icon>mdi-account-arrow-right</v-icon>
            </v-list-item-icon>
            <v-list-item-title @click="$store.commit('logout')">Cerrar Sesión</v-list-item-title>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar class="hidden-sm-and-down" color="secondary">

      <v-toolbar-items>
        <v-btn class="no-active" dark text to="/">
            <v-icon class="mr-2" color="primary">mdi-dumbbell</v-icon>
          <v-toolbar-title class="pa-0 primary--text">ENTRENAGRATIS.ES</v-toolbar-title>
        </v-btn>
      </v-toolbar-items>
      <v-toolbar-items class="inicio-entrenamientos">
        <v-btn class="primary--text" to="/" text>Inicio</v-btn>
        <v-btn class="primary--text" to="/rutinas" text>Rutinas</v-btn>
      </v-toolbar-items>
      <v-spacer></v-spacer>
      <v-toolbar-items v-if="!isLoggedIn">
        <v-btn class="primary--text" to="/ingresar" text>Iniciar Sesión</v-btn>
        <div class="d-flex align-center ml-1">
          <v-btn class="primary secondary--text" to='/registrarse' text rounded>Registrarse</v-btn>
        </div>
      </v-toolbar-items>
      <v-toolbar-items v-else>
        <v-btn class="primary--text" to="/perfil" text>Mi perfil</v-btn>
        <div class="d-flex align-center ml-1">
          <v-btn @click="$store.commit('logout')" class="primary secondary--text" to="/" text rounded>Cerrar Sesión</v-btn>
        </div>

      </v-toolbar-items>
    </v-app-bar>
  </div>
</template>

<script>

export default {
  name: "NavBar",
  data: function () {
    return {
      green: '#D6FF00',
      darkgray: '#343333',
      lightgray: '#E4E5E7',
      drawer: false,
      group: null,
    }
  },
  computed: {
    isLoggedIn (){
      return this.$store.getters.getLogged
    },
    isDrawer() {
      return this.drawer
    }
  }
}
</script>

<style scoped>
  .inicio-entrenamientos {
    position: absolute;
    top: 50%;  /* position the top  edge of the element at the middle of the parent */
    left: 50%; /* position the left edge of the element at the middle of the parent */
    transform: translate(-50%, -50%); /* This is a shorthand of translateX(-50%) and translateY(-50%) */
  }

  .v-btn--active.no-active::before {
    opacity: 0 !important;
  }
</style>