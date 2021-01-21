<template>
  <div class="jsy-narrow">
    <div class="flex-col item-center">
      <template v-for="menu in data">
        <template v-if="menu[dataProps.children] && menu[dataProps.children].length > 0">
          <el-popover
            :key="menu[dataProps.path]"
            class="full-w"
            placement="right-start"
            trigger="hover"
            popper-class="popper-box"
          >
            <template v-for="subMenu in menu[dataProps.children]">
              <NarrowSub
                :key="subMenu[dataProps.path]"
                :data-props="dataProps"
                :menu="subMenu"
                :default-active="defaultActive"
                @select="onMenuSelect(subMenu)"
              />
            </template>

            <div
              slot="reference"
              class="c12 text-white pointer flex-col item-center ptb15"
              :class="menuClass(menu)"
            >
              <jsy-icon :name="menu[dataProps.icon]" scale="1.3" />
              <span class="text-xs pt10">{{ menu[dataProps.label] }}</span>
            </div>
          </el-popover>
        </template>

        <el-tooltip
          v-else
          :key="menu[dataProps.path]"
          :content="menu[dataProps.label]"
          effect="light"
          placement="right"
        >
          <div
            class="c12 text-white pointer flex-col items-middle flex-center ptb15"
            :class="menuClass(menu)"
            @click="onMenuSelect(menu)"
          >
            <jsy-icon :name="menu[dataProps.icon]" scale="1.3" />
            <span class="text-xs pt10">{{ menu[dataProps.label] }}</span>
          </div>
        </el-tooltip>
      </template>
    </div>
  </div>
</template>

<script>
import NarrowSub from "./NarrowSub.vue";

export default {
  components: {
    NarrowSub,
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

    onMenuSelect(menu) {
      this.$emit("select", menu)
    },
  },
};
</script>

<style lang="stylus">
.jsy-narrow {
  overflow-y auto
  overflow-x hidden
  
  .popper-box {
    padding: 0 !important;
  }

  .narrow-item:hover {
    background-color: rgba(#303133, 0.3);
  }

  .select-bg {
    background: #08c4a2;
  }

  .unselect-bg {
    background: transparent;
  }
}
</style>
