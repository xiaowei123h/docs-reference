# Netlify

**特点**

类似Vercel，支持自动部署、表单处理、Serverless函数。适用于静态网站、JAMStack项目。（速度更快访问体验更好）

同理进入[Netlify](https://app.netlify.com/)，登录-->接入github-->选择项目-->配置Deploy Setting（构建命令、输出目录）

**注意**

需要设置（.env.production）
```[.env.production]
VITE_PUBLIC_PATH = /
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

部署后非首页路由刷新会报错找不到页面，原因：如果你的网站是一个单页应用（例如使用 Vue、React 等框架），Netlify 默认不会处理客户端路由（即非首页的路由）。当用户直接访问非首页路由时，Netlify 会尝试在服务器上查找对应的文件，但找不到，因此返回 404。

解决办法，在根目录新建文件netlify.toml

```[netlify.toml]
[build]
  publish = "dist"  # 替换为你的构建输出目录
  functions = "functions"  # 如果有 Netlify Functions，指定目录

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

即可解决非首页路由刷新404问题（如果vitepress和vue项目在同一个文件夹下，分开部署vitepress会受到影响，建议分库存放）

**其他动态网站托管**

Render：支持Node.js、Python、Ruby等，免费版含数据库。适用于小型动态网站（如Express、Django）。

Railway：支持Docker、多种语言，每月5美元免费额度。适用于全栈应用、API服务。
