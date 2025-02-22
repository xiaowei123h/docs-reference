# 细节

## Icons

从 @element-plus/icons-vue 中导入所有图标并进行全局注册。

（main.ts）
```[main.ts]
import * as ElementPlusIconsVue from '@element-plus/icons-vue'

for (const [key, component] of Object.entries(ElementPlusIconsVue)) {
  app.component(key, component)
}
```

只注入单个图标供路由侧边栏菜单使用（可减少资源加载）
（main.ts）
```[main.ts]
import { DataBoard } from "@element-plus/icons-vue"

app.component("DataBoard", DataBoard)
```

## Element Plus 中文包

引用element组件时会显示英文（比如分页组件），使用中文包后显示即为中文

（App.vue）
```[App.vue]
// Element Plus 中文包
import zhCn from "element-plus/es/locale/lang/zh-cn"

<el-config-provider :locale="zhCn">
  <router-view></router-view>
</el-config-provider>
```