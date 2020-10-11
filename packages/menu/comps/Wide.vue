<template>
  <el-menu
    v-bind="$attrs"
    :default-active="defaultActive"
    v-on="$listeners"
  >
    <template v-for="menu in data">
      <WideSub :data-props="dataProps" :key="menu[dataProps.path]" :menu="menu" />
    </template>
  </el-menu>
</template>

<script>
import WideSub from './WideSub.vue'

export default {
  components: {
    WideSub
  },
  props: {
    data: {
      type: Array,
      default: () => []
    },
    defaultActive: {
      type: String,
      default: ''
    }
  },
  inject: ['dataProps']
}
</script>
