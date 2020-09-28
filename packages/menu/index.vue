<template>
  <div class="jsy-menu-box flex">
    <div class="jsy-panel jsy-panel-wide">
      <MenuTop :logo="logo" :name="name" :is-narrow="isNarrow" />
      <Wide
        :data="data"
        :default-active="currentActive"
        @select="onMeneSelect"
      />
      <MenuBottom :is-narrow="isNarrow" @collapse="onCollapse(true)" />
    </div>
    <div class="jsy-panel jsy-panel-narrow">
      <MenuTop :logo="logo" :name="name" :is-narrow="isNarrow" />
      <Narrow
        :data="data"
        :default-active="currentActive"
        @select="onMeneSelect"
      />
      <MenuBottom :is-narrow="isNarrow" @collapse="onCollapse(false)" />
    </div>
  </div>
</template>

<script>
import MenuBottom from './comps/MenuBottom.vue'
import MenuTop from './comps/MenuTop.vue'
import Wide from './comps/Wide.vue'
import Narrow from './comps/Narrow.vue'
import gsap, { TweenLite } from 'gsap'
gsap.registerPlugin(TweenLite)

export default {
  name: 'JsyMenu',
  components: {
    MenuBottom,
    MenuTop,
    Narrow,
    Wide
  },
  props: {
    logo: {
      type: String,
      default: ''
    },
    name: {
      type: String,
      default: '项目名称'
    },
    defaultActive: {
      type: String,
      default: 'home2'
    },
    data: {
      type: Array,
      default: () => []
    }
  },
  data () {
    return {
      isNarrow: false,
      currentActive: this.defaultActive
    }
  },
  methods: {
    onMeneSelect (path) {
      this.currentActive = path
    },

    onCollapse (isNarrow) {
      this.isNarrow = isNarrow
      if (isNarrow) {
        TweenLite.to('.jsy-panel-wide', 0.4, {
          width: 0,
          opacity: 0
        })
        TweenLite.to('.jsy-panel-narrow', 0.2, {
          width: 80,
          opacity: 1
        })
      } else {
        TweenLite.to('.jsy-panel-narrow', 0.2, {
          width: 0,
          opacity: 0
        })
        TweenLite.to('.jsy-panel-wide', 0.4, {
          width: 200,
          opacity: 1
        })
      }
      // 主动触发resize事件，避免首页表格不刷新的问题
      setTimeout(() => {
        window.dispatchEvent(new Event('resize'))
      }, 401)
    }
  }
}
</script>

<style lang="stylus" scoped>
.jsy-menu-box {
  height: 100%;
  position: relative;
  background #294189;

  .jsy-panel {
    height: 100%;
    white-space: nowrap;
    position: relative;
    overflow: hidden;

    &.jsy-panel-wide {
      width: 200px;
    }

    &.jsy-panel-narrow {
      width: 0;
    }
  }
}
</style>
