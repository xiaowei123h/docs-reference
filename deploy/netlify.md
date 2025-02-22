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

**其他动态网站托管**

Render：支持Node.js、Python、Ruby等，免费版含数据库。适用于小型动态网站（如Express、Django）。

Railway：支持Docker、多种语言，每月5美元免费额度。适用于全栈应用、API服务。
