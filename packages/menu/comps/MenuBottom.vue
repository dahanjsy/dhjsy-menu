<template>
  <div
    class="jsy-collapse-box flex item-center c12 border-box border-white-2 border-top"
  >
    <div
      class="collapse-btn flex items-middle text-sm text-white-5 pointer"
      @click="onCollapse"
    >
      <jsy-icon
        :name="isNarrow ? 'el-icon-s-unfold' : 'el-icon-s-fold'"
        size="23"
      />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    logo: {
      type: String,
      default: ''
    },
    name: {
      type: String,
      default: ''
    },
    isNarrow: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    onCollapse () {
      this.$emit('collapse')
    }
  }
}
</script>

<style lang="stylus">
.jsy-collapse-box {
  height: 60px;
  position: absolute;
  bottom: 0;

  .collapse-btn:hover {
    color: #fff;
  }
}
</style>
