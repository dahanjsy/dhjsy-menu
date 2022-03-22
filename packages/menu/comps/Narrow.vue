<template>
  <div class="jsy-narrow">
    <div class="narrow-content">
      <template v-for="menu in data">
        <template v-if="menu[dataProps.children] && menu[dataProps.children].length > 0">
          <el-popover
            :key="menu[dataProps.path]"
            placement="right-start"
            trigger="hover"
            style="width: 100%;"
            popper-class="popper-box"
          >
            <template v-for="subMenu in menu[dataProps.children]">
              <NarrowSub
                :key="subMenu[dataProps.path]"
                :data-props="dataProps"
                :menu="subMenu"
                :default-active="defaultActive"
                @select="onMenuSelect"
              />
            </template>

            <div
              slot="reference"
              class="menu-item"
              :class="menuClass(menu)"
            >
              <MenuIcon :name="menu[dataProps.icon]" scale="1.3" />
              <span class="label">{{ menu[dataProps.label] }}</span>
            </div>
          </el-popover>
        </template>

        <div
          v-else
          :key="menu[dataProps.path]"
          class="menu-item"
          :class="menuClass(menu)"
          @click="onMenuSelect(menu[dataProps.path])"
        >
          <MenuIcon :name="menu[dataProps.icon]" scale="1.3" />
          <span class="label">{{ menu[dataProps.label] }}</span>
        </div>

      </template>
    </div>
  </div>
</template>

<script>
import NarrowSub from "./NarrowSub.vue";
import MenuIcon from './MenuIcon.vue'

export default {
  components: {
    NarrowSub,
    MenuIcon
  },
  props: {
    data: {
      type: Array,
      default: () => [],
    },
    defaultActive: {
      type: String,
      default: "",
    },
  },
  inject: ['dataProps'],
  methods: {
    menuClass(menu) {
      if (menu[this.dataProps.path] === this.defaultActive) return "select-bg"

      let className
      const recursion = item => {
        const children = item[this.dataProps.children] || []
        for (const subMenu of children) {
          if (subMenu[this.dataProps.path] === this.defaultActive) {
            className = "select-bg"
            return
          } else {
            recursion(subMenu)
          }
        }
      }
      recursion(menu)
      return className || "unselect-bg narrow-item"
    },

    onMenuSelect(path) {
      this.$emit("select", path)
    },
  },
};
</script>

<style lang="stylus">
@import '../style/index.styl'
</style>