<template>
  <v-app>
    <v-navigation-drawer v-model="drawer" enable-resize-watcher app temporary>
      <v-toolbar flat>
        <v-list>
          <v-list-tile>
            <v-img src="@static/logo.png" height="50px"/>

            <v-list-tile-title class="title grey--text">
              Maison Network
            </v-list-tile-title>
          </v-list-tile>
        </v-list>
    </v-toolbar>
    <v-divider></v-divider>
    <v-list>
      <v-list-tile
      v-for="item in items"
      :key="item.title"
      :to="item.to"
      >
      <v-list-tile-content>
      <v-list-tile-title >{{ item.title }}</v-list-tile-title>
      </v-list-tile-content>
      </v-list-tile>
    </v-list>
    </v-navigation-drawer>
    <v-toolbar fixed app>
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
      <nuxt-link class="title black--text" style="text-decoration: none" to="/">Maison Network</nuxt-link>
      <v-spacer></v-spacer>
      <v-toolbar-items class="hidden-sm-and-down">
        <v-btn flat to="/info">Learn More</v-btn>
      </v-toolbar-items>
    </v-toolbar>
    <v-content>
      <nuxt/>
    </v-content>
    <v-footer :fixed="true" app>
      <span class="ml-5">&copy; Maison Network 2018. An Xalpha Protocol.</span>
    </v-footer>
  </v-app>
</template>

<style lang="stylus">
.background {
  background-color: #FF7D9D;
background-size: 58px 58px;
background-position: 0px 2px, 4px 35px, 29px 31px, 33px 6px,
0px 36px, 4px 2px, 29px 6px, 33px 30px;
background-image:
linear-gradient(335deg, #C90032 23px, transparent 23px),
linear-gradient(155deg, #C90032 23px, transparent 23px),
linear-gradient(335deg, #C90032 23px, transparent 23px),
linear-gradient(155deg, #C90032 23px, transparent 23px),

linear-gradient(335deg, #C90032 10px, transparent 10px),
linear-gradient(155deg, #C90032 10px, transparent 10px),
linear-gradient(335deg, #C90032 10px, transparent 10px),
linear-gradient(155deg, #C90032 10px, transparent 10px);
}
</style>


<script>
export default {
    data () {
    return {
      drawer: false,
      items: [
        { title: 'Learn more', to: "/info"}
      ],
      right: null
    }
  }
};
</script>
