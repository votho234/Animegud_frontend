<template>
  <v-app id="inspire">
    <v-navigation-drawer
      v-model="drawer"
      app class="teal accent-3"
    >
    <v-list-item class="teal accent-4">
      <v-list-item-content>
        <v-list-item-title class="font-weight-bold" >
          Anime Gud
        </v-list-item-title>
        <v-list-item-subtitle class="font-italic">
          All Version
        </v-list-item-subtitle>
      </v-list-item-content>
    </v-list-item>
    <v-divider>
    </v-divider>
    <v-list dense>
      <v-list-item-group color="primary">
        <v-list-item
          v-for="(item, i) in items"
          :key="i" :to="item.link" link
        >
          <v-list-item-icon>
            <v-icon v-text="item.icon"></v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title v-text="item.title"></v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list-item-group>
    </v-list>
    </v-navigation-drawer>

    <v-app-bar app class="teal lighten-3">
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title class="font-weight-light" color="teal">Storage</v-toolbar-title>
    </v-app-bar>

    <v-main class="teal accent-1">
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
  export default {
    data: () => ({ 
      drawer: null ,
      items: [
        { title: "Home", icon: "mdi-home", link: "/" },
        { title: "Add", icon: "mdi-note-plus", link: "/add-post" },
        { title: "About", icon: "mdi-help-box", link: "/about" },
        
      ],
      }),
  }
</script>