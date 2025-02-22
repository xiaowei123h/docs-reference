# SVG组件管理插件

‌unplugin-svg-component‌ 是一个用于优化前端SVG组件管理的插件，特别适用于Vue和React项目。该插件解决了其他SVG图标插件的一些痛点，例如自动生成组件、类型提示、tree-shaking支持以及热重载（HMR）等功能。

## 使用方法

**安装插件**

::: code-group

```sh [npm]
npm install unplugin-svg-component -D
```

```sh [yarn]
yarn add unplugin-svg-component -D
```

:::

**创建文件夹**

在跟目录下创建文件夹types/auto

**配置插件**
（vite.config.js/vite.config.ts）
```[vite.config.js]
// 这是 Node.js 的 path 模块中的一个方法，用于将路径或路径片段解析为绝对路径。
import { resolve } from "node:path"
import SvgComponent from "unplugin-svg-component/vite"

export default defineConfig({
  plugins: [
    // 自动生成 SvgIcon 组件和 SVG 雪碧图
    SvgComponent({
      // __dirname 表示当前执行脚本所在的目录。resolve 函数会将 __dirname 和 "types/auto" 拼接成一个完整的文件路径。
      // src/assets/icons icon图标存放位置
      iconDir: [resolve(__dirname, "src/assets/icons")],
      preserveColor: resolve(__dirname, "src/assets/icons/preserve-color"),
      dts: true,
      dtsDir: resolve(__dirname, "types/auto")
    }),
  ],
})
```

**全局注册**
（main.js/main.ts）
```[main.js]
import SvgIcon from "~virtual/svg-component"

// 注册 SvgIcon 组件
app.component("SvgIcon", SvgIcon)
```

**使用**
（.vue）
```[vue]
<!-- keyboard-down.svg 已存在于src/assets/icons目录中 -->
<SvgIcon name="keyboard-down" />
```

**TS注意事项**

安装@types/node解决node:path报错

```sh [npm]
npm install @types/node -D
```