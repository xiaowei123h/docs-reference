# 快速开始 {#getting-started}

## 官方文档 {#official-documents}
[VitePress](https://vitejs.cn/vitepress/)

## 安装 {#installation}
VitePress 可以单独使用，也可以安装到现有项目中。在这两种情况下，都可以使用以下方式安装它：

::: code-group

```sh [npm]
npm add -D vitepress
```

```sh [pnpm]
pnpm add -D vitepress
```

```sh [yarn]
yarn add -D vitepress
```

```sh [yarn (pnp)]
yarn add -D vitepress vue
```

```sh [bun]
bun add -D vitepress
```

:::

启动向导：

::: code-group

```sh [npm]
npx vitepress init
```

```sh [pnpm]
pnpm vitepress init
```

```sh [yarn]
yarn vitepress init
```

```sh [bun]
bun vitepress init
```

:::

如果正在构建一个独立的 VitePress 站点，可以在当前目录 (`./`) 中搭建站点。但是，如果在现有项目中与其他源代码一起安装 VitePress，建议将站点搭建在嵌套目录 (例如 `./docs`) 中，以便它与项目的其余部分分开。

将以下 npm 脚本注入到 `package.json` 中：
```json [package.json]
{
  ...
  // 注意必填，否则打包会报错
  "type": "module",
  "scripts": {
    "docs:dev": "vitepress dev docs",
    "docs:build": "vitepress build docs",
    "docs:preview": "vitepress preview docs"
  },
  ...
}
```

`docs:dev` 脚本将启动具有即时热更新的本地开发服务器。使用以下命令运行它：

::: code-group

```sh [npm]
npm run docs:dev
```

```sh [pnpm]
pnpm run docs:dev
```

```sh [yarn]
yarn docs:dev
```

```sh [bun]
bun run docs:dev
```

:::

除了 npm 脚本，还可以直接调用 VitePress：

::: code-group

```sh [npm]
npx vitepress dev docs
```

```sh [pnpm]
pnpm vitepress dev docs
```

```sh [yarn]
yarn vitepress dev docs
```

```sh [bun]
bun vitepress dev docs
```

:::

开发服务应该会运行在 `http://localhost:5173` 上。

## 配置 {#configuration}

配置文件 (`.vitepress/config.js`)  配置标题，简介，导航，侧边栏菜单：
```js [.vitepress/config.js]
export default {
  // 标题
  title: 'Vue Admin Reference',
  // 描述
  description: 'Reference site',

  themeConfig: {
    // 标题前logo
    logo: { src: '/logo.png', width: 24, height: 24 },
    // 导航
    nav: [
      { text: '首页', link: '/' }
    ],
    // 侧边导航
    sidebar: [
      {
        text: 'VitePress',
        // 是否折叠导航
        collapsed: false,
        items: [
          { text: '快速开始', link: '/vitepress/started' }
        ]
      },
    ],
    // 上一页下一页标签名
    docFooter: {
      prev: '上一页',
      next: '下一页'
    },
    // 页面导航标签
    outline: {
      label: '页面导航'
    },
  }
}
```

## 本地构建与测试 {#build-and-test-locally}

可以运行以下命令来构建文档：

```sh
npm run docs:build
```

构建文档后，通过运行以下命令可以在本地预览它：

```sh
npm run docs:preview
```