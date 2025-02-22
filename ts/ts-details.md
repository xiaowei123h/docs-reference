# TS

## 引入vue文件时提示找不到该模块

component: () => import("@/views/elementPlus/elementTable.vue"),提示找不到vue文件

在根目录添加types/shims-vue.d.ts

（shims-vue.d.ts）
```[shims-vue.d.ts]
declare module '*.vue' {
  import type { DefineComponent } from 'vue'
  const component: DefineComponent<{}, {}, any>
  export default component
}
```

确保ts配置文件中include 或 files 包含类型文件路径

（tsconfig.json）
```[tsconfig.json]
{
  // 需要被编译的文件列表
  "include": ["**/*.d.ts"],
}
```