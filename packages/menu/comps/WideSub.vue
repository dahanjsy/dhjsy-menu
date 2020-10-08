<template>
  <el-submenu
    v-if="menu.children && menu.children.length > 0"
    :key="menu.path"
    :index="menu.path"
  >
    <template slot="title">
      <jsy-icon v-if="menu.icon" :name="menu.icon" class="mr10" />
      <span :class="{ 'ml5': !menu.icon }">{{ menu.label }}</span>
    </template>
    <template v-for="subMenu in menu.children">
      <WideSub :key="subMenu.path" :menu="subMenu" />
    </template>
  </el-submenu>

  <el-menu-item v-else :key="menu.path" :index="menu.path">
    <jsy-icon v-if="menu.icon" :name="menu.icon" class="mr10" />
    <span :class="{ 'ml5': !menu.icon }">{{ menu.label }}</span>
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
  }
}
</script>
