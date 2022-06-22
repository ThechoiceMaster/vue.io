<template>
  <div id="app">
    <v-app-bar color="deep-purple accent-4" dense dark class="header-app">
      <v-app-bar-nav-icon></v-app-bar-nav-icon>

      <v-toolbar-title>Page title</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn icon>
        <v-icon>mdi-heart</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>

      <v-menu left bottom>
        <template v-slot:activator="{ on, attrs }">
          <v-btn icon v-bind="attrs" v-on="on">
            <v-icon>mdi-dots-vertical</v-icon>
          </v-btn>
        </template>

        <v-list>
          <v-list-item v-for="n in 5" :key="n" @click="() => {}">
            <v-list-item-title>Option {{ n }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>
    <div>
      <v-card height="100vh" width="200" class="mx-auto fix-side">
        <v-navigation-drawer permanent>
          <v-toolbar dense elevation="2"></v-toolbar>

          <v-divider></v-divider>

          <v-list dense nav>
            <v-list-item
              v-for="item in items"
              :key="item.title"
              link
              @click="goToPush(item.path)"
            >
              <v-list-item-icon>
                <v-icon>{{ item.icon }}</v-icon>
              </v-list-item-icon>
              <v-list-item-content>
                <v-list-item-title>{{ item.title }}</v-list-item-title>
              </v-list-item-content>
            </v-list-item>

            <v-list-group :value="true" prepend-icon="mdi-account-circle">
              <template v-slot:activator>
                <v-list-item-title>Users</v-list-item-title>
              </template>
              <v-list-item
                v-for="item in items"
                :key="item.title"
                link
                @click="goToPush(item.path)"
              >
                <v-list-item-icon>
                  <v-icon>{{ item.icon }}</v-icon>
                </v-list-item-icon>
                <v-list-item-content>
                  <v-list-item-title>{{ item.title }}</v-list-item-title>
                </v-list-item-content>
              </v-list-item>
            </v-list-group>
          </v-list>
        </v-navigation-drawer>
      </v-card>

      <v-main>
        <v-toolbar dense elevation="4"></v-toolbar>
        <router-view></router-view>
      </v-main>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        { title: "Dashboard", icon: "mdi-view-dashboard", path: "/" },
        { title: "Photos", icon: "mdi-image", path: "/photos" },
        { title: "About", icon: "mdi-help-box", path: "/about" },
      ],
      right: null,
    };
  },
  methods: {
    goToPush(path) {
      this.$router.push(path);
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
