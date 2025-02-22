# UnoCSS

UnoCSS‌是一个即时的原子CSS引擎，它允许开发者通过简短的类名来控制元素的样式，而不需要编写复杂的CSS代码。

[UnoCSS中文文档](https://unocss.jiangruyi.com/)

## 使用

**安装**

::: code-group

```sh [npm]
npm install -D unocss
```

```sh [pnpm]
pnpm add -D unocss
```

```sh [yarn]
yarn add -D unocss
```
:::

**安装插件**
（vite.config.ts）
```[vite.config.ts]
import UnoCSS from 'unocss/vite'

export default defineConfig({
  plugins: [
    UnoCSS(),
  ],
})
```

根目录创建 uno.config.ts 文件

（uno.config.ts）
```[uno.config.ts]
import { defineConfig } from 'unocss'

export default defineConfig({
  // 自定义规则
  rules: [
    // margin: 20  m-20
    [/^m-([\.\d]+)$/, ([_, num]) => ({ margin: `${num}px` })],
    [/^p-([.\d]+)$/, ([_, num]) => ({ padding: `${num}px` })],
  ],
  // 自定义快捷方式
  shortcuts: {
    "m-p-20": "m-20 p-20",
  }
})
```

**注意**

如果安装完unocss后自定义规则使用发现样式没有热更新，可以按ctrl+f5强刷新浏览器再次尝试。

如果还不可以就删除node_modules后重新npm i安装依赖，再次ctrl+f5强刷新浏览器即可。

同样自定义预设后不生效需要重新 npm run dev，然后再ctrl+f5。

## 定义自己的预设

创建文件unocss/my-preset.ts

（my-preset.ts）
```[my-preset.ts]
import { Preset } from 'unocss'

export const myPreset: Preset = {
  name: 'my-preset',
  rules: [/* ... */],
  variants: [/* ... */],
  shortcuts: [/* ... */],
}
```

（uno.config.ts）
```[uno.config.ts]
import { myPreset } from './my-preset'

export default defineConfig({
  presets: [
    myPreset, // 您自己的预设
  ],
})
```

## 自定义预设使用说明

**box-shadow样式：** shadow1 - shadow5

**margin样式：** m- 支持1、2、4个参数，参数可为负 m--20 = margin: -20px，m-t-10 = margin-top: 10px

**padding：** 同margin p-

**display样式：** flex = display: flex ，flex-c水平垂直居中， flex-c-x水平居中，flex-c-y垂直居中，flex-a = space-around，flex-b = space-between，flex-e = flex-end

**max-width、min-width、max-height、min-height：** max-w-100% = max-width: 100%，min-h-100vh = min-height: 100vh，单位rem px em % vh vw

**文本超出省略号：** ellipsis单行超出，ellipsis-3 三行超出

**font-size：** f-3 = font-size: 3px

**width、height** w-100px h-10%， 单位rem px em % vh vw


