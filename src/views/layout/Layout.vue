<template>
  <v-app class="app" :class="`theme-${chartTheme}`">
    <sidebar></sidebar>
    <navbar @showadom="showAdom = true"></navbar>
    <v-navigation-drawer temporary :value="leftdrawer" fixed></v-navigation-drawer>
    <slider></slider>
    <v-content class="main-content">
        <v-jumbotron :gradient="gradient" :height="`100%`">
              <app-main></app-main>
        </v-jumbotron>
    </v-content>
    <select-adom :show-adom="showAdom" @adomselect="adomSelect"></select-adom>
  </v-app>
</template>

<script>
import { mapGetters } from 'vuex'
import { Slider, Navbar, Sidebar, AppMain } from './components'
import SvgIcon from '@/components/SvgIcon.vue'// svg组件
import SelectAdom from '@/components/SelectAdom'

export default {
  name:'Layout',
  components: { Slider, Navbar,Sidebar,AppMain,'svg-icon': SvgIcon, SelectAdom},
  data:() => ({
    //gradient:'to top, #cfd9df 0%, #e2ebf0 100%',
    //gradient:'to top, #a8edea 0%, #fed6e3 100%',
    showAdom: false,
  }),
  computed: {
    ...mapGetters([
      'leftdrawer',
      'gradient',
      'chartTheme'
    ]),
    routes() {
      return this.$router.options.routes
    },
  },
  methods: {
    adomSelect(args){
        this.showAdom = false;
    },
  }
}
</script>
<style lang="less" scoped>
.main-content{
  height: 100%;
}
  .content--wrap{
    overflow-y: auto;
  }
</style>
