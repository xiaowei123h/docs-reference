# GitHub Pages

**特点**

与GitHub仓库直接绑定，支持自定义域名，自动部署（通过Git提交）。适用于静态网站（如VuePress、React、Hexo等）。

**方法一**

首先打包本地文件生成dist文件
```sh
npm run build
```

进入github要部署的项目，按图片顺序

[![githubPages](/githubPages.jpg)](/githubPages.jpg)

**方法二**

::: details ‌gh-pages是什么
‌gh-pages‌是GitHub提供的一个功能，允许用户将仓库中的静态网站内容部署到GitHub的服务器上，并通过自定义域名或GitHub提供的子域名进行访问。gh-pages是一个分支，用于托管静态网站。用户可以将HTML、CSS、JavaScript等静态文件推送到这个分支，GitHub会自动将其部署为一个可访问的网站‌。
:::

安装gh-pages
```sh
npm install gh-pages --save-dev
```

配置gh-pages(package.json)
```json [package.json]
{
  "scripts": {
    "deploy": "gh-pages -d dist"
  }
}
```

运行
```sh
npm run deploy
```

**注意**

如果生成的网站地址https://github用户名.github.io/项目名/
带有/项目名/

需要设置（.env.production）
```[.env.production]
VITE_PUBLIC_PATH = /项目名/
```

（vite.config.js/vite.config.ts）
```[vite.config.js]
export default defineConfig(({mode}) => {
  return {
    // 开发或打包时用到的公共基础路径
    base: VITE_PUBLIC_PATH,
  }
})
```

（router/index.js / router/index.ts）
```[index.js]
import { createWebHashHistory } from 'vue-router'

const router = createRouter({
  history: createWebHashHistory()
})
```