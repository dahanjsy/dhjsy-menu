<template>
  <div class="jsy-menu-box" :class="`${styleType}-style`">
    <div class="jsy-panel jsy-panel-wide">
      <MenuTop v-if="name" :logo="logo" :name="name" :is-narrow="isNarrow" />
      <el-scrollbar class="menu-content" :class="name ? 'hasTop' : 'noTop'">
        <Wide
          class="menu-item"
          :data="data"
          :data-props="dataProps"
          :default-active="currentActive"
          :default-openeds="currentOpeneds"
          @select="onMenuSelect"
        />
      </el-scrollbar>

      <MenuBottom :is-narrow="isNarrow" @collapse="onCollapse(true)" />
    </div>
    <div class="jsy-panel jsy-panel-narrow">
      <MenuTop v-if="name" :logo="logo" :name="name" :is-narrow="isNarrow" />
      <el-scrollbar class="menu-content" :class="name ? 'hasTop' : 'noTop'">
        <Narrow
          class="menu-item"
          :data="data"
          :data-props="dataProps"
          :default-active="currentActive"
          @select="onMenuSelect"
        />
      </el-scrollbar>
      <MenuBottom :is-narrow="isNarrow" @collapse="onCollapse(false)" />
    </div>
  </div>
</template>

<script>
import MenuBottom from "./comps/MenuBottom.vue";
import MenuTop from "./comps/MenuTop.vue";
import Wide from "./comps/Wide.vue";
import Narrow from "./comps/Narrow.vue";
import gsap, { TweenLite } from "gsap";
gsap.registerPlugin(TweenLite);

export default {
  name: "JsyMenu",
  components: {
    MenuBottom,
    MenuTop,
    Narrow,
    Wide,
  },
  props: {
    logo: {
      type: String,
      default: "",
    },
    styleType: {
      type: String,
      default: "default", // 可选择 light,default
    },
    name: {
      type: String,
      default: "",
    },
    defaultActive: {
      type: String,
      default: "home",
    },
    defaultOpeneds: {
      type: Array,
      default: () => [],
    },
    expandAll: {
      type: Boolean,
      default: false,
    },
    shrink: {
      // 是否收缩模式
      type: Boolean,
      default: false,
    },
    data: {
      type: Array,
      default: () => [],
    },
    dataProps: {
      type: Object,
      default: () => {
        return {
          label: "menuName",
          path: "url",
          icon: "icon",
          children: "children",
        };
      },
    },
  },
  data() {
    return {
      isNarrow: this.shrink,
      currentActive: this.defaultActive,
    };
  },
  provide() {
    return {
      dataProps: this.dataProps,
    };
  },
  watch: {
    defaultActive(v) {
      this.currentActive = v;
    },
  },
  computed: {
    currentOpeneds() {
      if (this.expandAll) {
        const openeds = [];
        const func = (children) => {
          if (children && children.length > 0) {
            children.forEach((item) => {
              openeds.push(item[this.dataProps.path]);
              func(item[this.dataProps.children]);
            });
          }
        };
        func(this.data);
        return openeds;
      }
      return this.defaultOpeneds;
    },
  },
  mounted() {
    if (this.isNarrow) {
      this.onCollapse(this.isNarrow);
    }
  },
  methods: {
    onMenuSelect(path) {
      this.currentActive = path;
      this.$emit("select", path);
    },

    onCollapse(isNarrow) {
      this.isNarrow = isNarrow;
      if (isNarrow) {
        TweenLite.to(".jsy-panel-wide", 0.4, {
          width: 0,
          opacity: 0,
        });
        TweenLite.to(".jsy-panel-narrow", 0.2, {
          width: 80,
          opacity: 1,
        });
      } else {
        TweenLite.to(".jsy-panel-narrow", 0.2, {
          width: 0,
          opacity: 0,
        });
        TweenLite.to(".jsy-panel-wide", 0.4, {
          width: 200,
          opacity: 1,
        });
      }
      // 主动触发resize事件，避免首页表格不刷新的问题
      setTimeout(() => {
        window.dispatchEvent(new Event("resize"));
      }, 401);
    },
  },
};
</script>

<style lang="stylus">
@import './style/index.styl'
</style>
