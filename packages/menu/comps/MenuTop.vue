<template>
  <div
    class="flex plr20 border-box border-bottom border-white-2"
    :class="isNarrow ? 'item-center' : 'items-middle'"
    style="height: 60px;"
  >
    <el-image
      style="width: 30px; height: 30px;"
      lazy
      :src="logo"
      fit="cover"
    />
    <h5 v-if="!isNarrow" class="text-white h5 bold ml10">{{ name }}</h5>
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
