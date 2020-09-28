<template>
  <div class="over-auto-y">
    <div class="flex-col item-center">
      <template v-for="menu in data">
        <template v-if="menu.children && menu.children.length > 0">
          <el-popover
            :key="menu.path"
            class="full-w"
            placement="right-start"
            trigger="hover"
            popper-class="popper-box"
          >
            <template v-for="subMenu in menu.children">
              <NarrowSub
                :key="subMenu.path"
                :menu="subMenu"
                :default-active="defaultActive"
                @select="onMenuSelect"
              />
            </template>

            <div
              slot="reference"
              class="c12 text-white pointer flex-col item-center ptb15"
              :class="menuClass(menu)"
            >
              <jsy-icon :name="menu.icon" scale="1.3" />
              <span class="text-xs pt10">{{ menu.name }}</span>
            </div>
          </el-popover>
        </template>

        <el-tooltip
          v-else
          :key="menu.path"
          :content="menu.name"
          effect="light"
          placement="right"
        >
          <div
            class="c12 text-white pointer flex-col items-middle flex-center ptb15"
            :class="menuClass(menu)"
            @click="onMenuSelect(menu.path)"
          >
            <jsy-icon :name="menu.icon" scale="1.3" />
            <span class="text-xs pt10">{{ menu.name }}</span>
          </div>
        </el-tooltip>
      </template>
    </div>
  </div>
</template>

<script>
import NarrowSub from './NarrowSub.vue'

export default {
  components: {
    NarrowSub
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
  methods: {
    menuClass (menu) {
      if (menu.path === this.defaultActive) return 'select-bg'

      const func = menu => {
        const children = menu.children || []
        for (const subMenu of children) {
          if (subMenu.path === this.defaultActive) return 'select-bg'
          return func(subMenu)
        }
        return 'unselect-bg narrow-item'
      }

      return func(menu)
    },

    onMenuSelect (path) {
      this.$emit('select', path)
    }
  }
}
</script>

<style lang="stylus" scoped>
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
</style>
