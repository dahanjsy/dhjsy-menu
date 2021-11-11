<template>
  <i v-if="!isElIcon">
    <svg
      aria-hidden="true"
      :class="clazz"
      :style="style"
      @click="handClick"
    >
      <use :xlink:href="xlinkHref" />
    </svg>
  </i>
  <i v-else :class="[clazz, name]" :style="style" @click="handClick" />
</template>

<script>
export default {
  name: 'MenuIcon',
  props: {
    size: {
      type: [Number, String],
      default: 14
    },
    name: {
      type: String,
      required: true,
      default: ''
    },
    scale: {
      type: [Number, String],
      default: 0
    },
    spin: Boolean
  },
  computed: {
    xlinkHref () {
      return `#${this.name}`
    },
    style () {
      const fontSize = this.scale ? this.scale + 'em' : this.size + 'px'
      return { fontSize }
    },
    clazz () {
      return {
        icon: true,
        spin: this.spin
      }
    },
    isElIcon () {
      return this.name.indexOf('el-icon-') === 0
    }
  },
  methods: {
    handClick (event) {
      this.$emit('click', event)
    }
  }
}
</script>

<style lang="stylus" scoped>
.icon {
  width: 1em;
  height: 1em;
  vertical-align: -0.15em;
  fill: currentColor;
  overflow: hidden;
  min-width: 10px;
}

.spin {
  animation: spin 1s infinite linear;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
