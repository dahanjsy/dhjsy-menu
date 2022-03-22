<template>
  <div class="jsy-narrow-sub">
    <el-menu v-bind="$attrs" :default-active="defaultActive" v-on="$listeners">
      <WideSub :menu="menu" :data-props="dataProps" />
    </el-menu>
  </div>
</template>

<script>
import WideSub from "./WideSub.vue";

export default {
  name: "NarrowSub",
  components: {
    WideSub,
  },
  props: {
    menu: {
      type: Object,
      default: () => {},
    },
    defaultActive: {
      type: String,
      default: "",
    },
  },
  inject: ["dataProps"],
};
</script>

<style lang="stylus">
@import '../style/index.styl'

.jsy-narrow-sub {
  width: 200px;

  .el-menu {
    border-right: none !important;
    background-color: transparent !important;

    .el-menu-item, .el-submenu__title, .el-submenu .el-menu-item {
      height: 40px;
      line-height: 40px;
      font-size: 13px;
      color: #303133 !important;
    }

    .el-menu-item.is-active {
      color: #294189 !important;
      background-color: rgba(#294189, 0.1) !important;
    }

    .el-submenu__title i {
      color: #606266;
    }

    .el-submenu__title:hover, .el-menu-item:focus, .el-menu-item:hover {
      background: rgba(#303133, 0.1);
    }
  }
}
</style>
