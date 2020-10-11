<template>
  <el-submenu
    v-if="menu[dataProps.children] && menu[dataProps.children].length > 0"
    :key="menu[dataProps.path]"
    :index="menu[dataProps.path]"
  >
    <template slot="title">
      <jsy-icon v-if="menu[dataProps.icon]" :name="menu[dataProps.icon]" class="mr10" />
      <span :class="{ 'ml5': !menu[dataProps.icon] }">{{ menu[dataProps.label] }}</span>
    </template>
    <template v-for="subMenu in menu[dataProps.children]">
      <WideSub :key="subMenu[dataProps.path]" :menu="subMenu" />
    </template>
  </el-submenu>

  <el-menu-item v-else :key="menu[dataProps.path]" :index="menu[dataProps.path]">
    <jsy-icon v-if="menu[dataProps.icon]" :name="menu[dataProps.icon]" class="mr10" />
    <span :class="{ 'ml5': !menu[dataProps.icon] }">{{ menu[dataProps.label] }}</span>
  </el-menu-item>
</template>

<script>
export default {
  name: 'WideSub',
  props: {
    menu: {
      type: Object,
      default: () => {}
    }
  },
  inject: ['dataProps']
}
</script>
