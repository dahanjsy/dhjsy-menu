<template>
  <div class="jsy-collapse-box">
    <div class="collapse-btn" @click="onCollapse">
      <MenuIcon
        :name="isNarrow ? 'el-icon-s-unfold' : 'el-icon-s-fold'"
        size="23"
      />
    </div>
  </div>
</template>

<script>
import MenuIcon from './MenuIcon.vue'
export default {
  components: {
    MenuIcon
  },
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

<style lang="stylus" scoped>
.jsy-collapse-box {
  height: 60px;
  position: absolute;
  bottom: 0;

  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  box-sizing: border-box;
  border-top: 1px solid #eee
  border-color: rgba(#fff, 0.2);

  .collapse-btn {
    display: flex;
    align-items: center;
    font-size: 13px;
    color: #A9B3D0;
    border-color: rgba(#fff, 0.5);
    cursor: pointer;
  }

  .collapse-btn:hover {
    color: #fff;
  }
}
</style>
