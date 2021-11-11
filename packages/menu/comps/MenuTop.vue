<template>
  <div
    class="jsy-menu-top"
    :class="isNarrow ? 'narrow' : 'no-narrow'"
    style="height: 60px;"
  >
    <el-image
      style="width: 30px; height: 30px;"
      lazy
      :src="logo"
      fit="cover"
    />
    <h5 v-if="!isNarrow" class="top-title">{{ name }}</h5>
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
  }
}
</script>

<style lang="stylus" scoped>
.jsy-menu-top {
  display: flex;
  padding: 0 20px;
  box-sizing: border-box;
  border-bottom: 1px solid #eee
  border-color: rgba(#fff, 0.2);

  &.narrow {
    justify-content: center;
    align-items: center;
  }
  &.no-narrow {
    align-items: center;
  }

  .top-title {
    color: #fff;
    font-size: 16px;
    font-weight: bold;
    margin-left: 10px;
  }
}
</style>
