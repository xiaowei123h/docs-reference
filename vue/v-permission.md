# v-permission

自定义权限指令

## permission-directive

创建（permission-directive.ts）文件
```[permission-directive.ts]
import type { App, Directive } from "vue"
// 从pinia状态管理库中获取用户角色
import { useUserStore } from "@/store/modules/user"
import { isArray } from "@/utils/validate"

const permission: Directive = {
  mounted(el, binding) {
    const { value: permissionRoles } = binding
    const { roles } = useUserStore()
    if (isArray(permissionRoles) && permissionRoles.length > 0) {
      const hasPermission = roles.some(role => permissionRoles.includes(role))
      hasPermission || el.parentNode?.removeChild(el)
    } else {
      throw new Error(`参数必须是一个数组且长度大于 0，参考：v-permission="['admin','editor']"`)
    }
  }
}

export function installPermissionDirective(app: App) {
  app.directive("permission", permission)
}
```

（validate.ts）
```[validate.ts]
// 判断是否为数组
export function isArray<T>(arg: T) {
  return Array.isArray ? Array.isArray(arg) : Object.prototype.toString.call(arg) === "[object Array]"
}
```

全局注册（main.ts）
```[main.ts]
import { installPermissionDirective } from "@/common/permission-directive"

// 自定义权限指令
installPermissionDirective(app)
```

使用（.vue）
```[.vue]
<div v-permission="['editor', 'admin']">按钮</div>
```

**开发环境修改v-permission不会热更新需手动刷新**

## v-if + checkPermission

Element Plus 的 el-tab-pane 和 el-table-column 以及其它动态渲染 DOM 的场景不适合使用 v-permission 这种情况下你可以通过 v-if + checkPermission 来实现。

（checkPermission.ts）
```[checkPermission.ts]
import { useUserStore } from "@/store/modules/user"
import { isArray } from "@/utils/validate"

/** 全局权限判断函数，和权限指令 v-permission 功能类似 */
export function checkPermission(permissionRoles: string[]): boolean {
  if (isArray(permissionRoles) && permissionRoles.length > 0) {
    const { roles } = useUserStore()
    return roles.some(role => permissionRoles.includes(role))
  } else {
    console.error("参数必须是一个数组且长度大于 0，参考：checkPermission(['admin','editor'])")
    return false
  }
}

```

**使用**

（.vue）
```[.vue]
import { checkPermission } from "@/common/checkPermission"

<div v-if="checkPermission(['editor', 'admin'])">按钮</div>
```

