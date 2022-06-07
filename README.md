## 基于 element-ui 的一款菜单组件 dhjsy-menu

### 使用示例

```html
<dhjsy-menu
  :data="menuList"
  name="菜单名称"
  :logo="require('@/assets/images/logo.png')"
  expand-all
  :default-active="activeRouteName"
  @select="onMenuSelect"
/>
```

```js
export default {
  computed: {
    activeRouteName (): string {
      const { name } = this.$route
      return name
    }
  },
  methods: {
    onMenuSelect (path: string) {
      this.$router.push({ name: path })
    }
  }
}
```

### 使用说明

该插件基于 element-ui 进行封装，支持 普通菜单和缩略图 两种风格。

```bash
npm install dhjsy-menu
```

### 属性

| 参数 | 说明 | 类型 | 可选值 | 默认值  |
| ---- | ---- | ---- | ---- | ---- |
| logo | 项目图标 | string | - | - |
| name | 项目名称，如果不传入，则顶部栏目不显示 | string | - | - |
| defaultActive | 默认激活的菜单项 | string | - | home |
| defaultOpeneds | 默认展开的菜单 | string[] | - | - |
| expandAll | 是否展开所有 | boolean | - | false |
| shrink | 是否收缩模式 | boolean | - | false |
| data | 菜单数据 | Array | - | [] |
| dataProps | 数据属性值 | object | - | { label: 'menuName', path: 'url', icon: 'icon', children: 'children' }

### 事件

| 事件名称 | 说明 | 回调参数 |
| ---- | ---- | ---- |
| select | 选择菜单回调 | path |
