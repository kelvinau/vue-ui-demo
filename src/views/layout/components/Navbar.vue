<template>
    <v-toolbar color="" height="50" light fixed app>
        <v-jumbotron :gradient="topBgColor" height="50px">
          <div class="content">
            <hamburger class="hamburger-container" :toggleClick="toggleSideBar" :isActive="sidebar.opened"></hamburger>
            <route-tags class="route-tags"></route-tags>
            <!--
            <my-breadcrumb></my-breadcrumb>
            <span class="setting-icon" @click.stop="toggleRightDrawer">
              <svg-icon :icon-class="`settings`" :class-name="'settings'" ></svg-icon>
            </span>
            -->
            <v-chip class="adom-title" @click="$emit('showadom')">ADOM: {{adom.current}}</v-chip>
          </div>
        </v-jumbotron>
    </v-toolbar>
</template>
<script>
import { mapGetters } from 'vuex'
import MyBreadcrumb from '@/components/Breadcrumb.vue'
import RouteTags from '@/components/RouteTags.vue'
import Hamburger from '@/components/Hamburger.vue'

export default {
  name: 'NavBar',
  data () {
    return {
        theme1: 'light'
    }
  },
  components: {
    RouteTags,
    MyBreadcrumb,
    Hamburger
  },
  computed: {
    ...mapGetters([
      'sidebar',
      'rightdrawer',
      'topBgColor',
      'avatar',
      'adom'
    ])
  },
  methods: {
    toggleSideBar() {
      this.$store.dispatch('ToggleSideBar')
    },
    toggleRightDrawer() {
      this.$store.dispatch('ToggleRight')
    },
    logout() {
      this.$store.dispatch('LogOut').then(() => {
        location.reload() // 为了重新实例化vue-router对象 避免bug
      })
    }
  }
}
</script>
<style lang="less" scoped>
.content{
  height: 100%;
  display: flex;
  align-items: center;
  padding: 0px 20px 0 10px;
}
.route-tags{
  margin: 0 20px;
  flex-grow: 1;
}
.adom-title{
  cursor: pointer;
  min-width: 80px;
  margin-right: 100px;
}
</style>
