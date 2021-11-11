<template>
  <el-submenu
    v-if="menu[dataProps.children] && menu[dataProps.children].length > 0"
    :key="menu[dataProps.path]"
    :index="menu[dataProps.path]"
  >
    <template slot="title">
      <MenuIcon v-if="menu[dataProps.icon]" :name="menu[dataProps.icon]" style="margin-right: 10px;" />
      <span :class="{ 'label': !menu[dataProps.icon] }">{{ menu[dataProps.label] }}</span>
    </template>
    <template v-for="subMenu in menu[dataProps.children]">
      <WideSub :key="subMenu[dataProps.path]" :menu="subMenu" />
    </template>
  </el-submenu>

  <el-menu-item v-else :key="menu[dataProps.path]" :index="menu[dataProps.path]">
    <MenuIcon v-if="menu[dataProps.icon]" :name="menu[dataProps.icon]" style="margin-right: 10px;" />
    <span :class="{ 'label': !menu[dataProps.icon] }">{{ menu[dataProps.label] }}</span>
  </el-menu-item>
</template>

<script>
import MenuIcon from './MenuIcon.vue'

export default {
  name: 'WideSub',
  components: {
    MenuIcon
  },
  props: {
    menu: {
      type: Object,
      default: () => {}
    }
  },
  inject: ['dataProps']
}
</script>

<style lang="stylus" scoped>
.label {
  margin-left: 5px;
}
</style>