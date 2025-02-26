# 面试题

## 什么是内存泄漏，前端开发容易产生内存泄漏的原因

&emsp;内存泄漏（Memory Leak） 是指程序中已动态分配的内存由于某种原因未能被释放，导致系统内存的浪费。随着时间的推移，内存泄漏会逐渐消耗可用内存，最终可能导致程序运行缓慢、崩溃或系统性能下降。

&emsp;在前端开发中，内存泄漏通常表现为页面长时间运行后，内存占用不断增加，甚至导致浏览器标签页崩溃。

**原因**

1. 未清理的定时器或回调函数

  &emsp; 如果设置了 setInterval 或 setTimeout，但在组件销毁时未清除，这些定时器会继续运行，并持有对组件或 DOM 元素的引用，导致内存泄漏。

  &emsp; 解决方法：
  在组件销毁时清除定时器。

2. 未解绑的事件监听器

  &emsp; 如果给 DOM 元素添加了事件监听器，但在组件销毁时未移除，这些监听器会继续持有对 DOM 元素的引用，导致内存泄漏。

  &emsp; 解决方法：
  在组件销毁时移除事件监听器。

3. 未释放的闭包

  &emsp; 闭包会捕获外部函数的变量，如果闭包未被释放，这些变量会一直存在于内存中。

  &emsp; 解决方法：
  确保不再需要时释放闭包。

4. 未清理的全局变量

  &emsp; 全局变量会一直存在于内存中，直到页面关闭。如果全局变量持有大量数据或 DOM 引用，会导致内存泄漏。

  &emsp; 解决方法：
  避免滥用全局变量，或在不再需要时手动释放。

5. 未销毁的第三方库实例

  &emsp; 某些第三方库（如 ECharts、Mapbox 等）会创建实例并持有对 DOM 元素的引用。如果未在组件销毁时销毁这些实例，会导致内存泄漏。

  &emsp; 解决方法：
  在组件销毁时销毁实例。

6. 未清理的 DOM 引用

  &emsp; 如果 JavaScript 中持有对 DOM 元素的引用，但未在组件销毁时释放，这些 DOM 元素会一直存在于内存中。

  &emsp; 解决方法：
  在组件销毁时释放 DOM 引用。

7. 未清理的 WebSocket 或 AJAX 请求

  &emsp; 如果 WebSocket 连接或 AJAX 请求未在组件销毁时关闭，这些连接会一直保持，导致内存泄漏。

  &emsp; 解决方法：
  在组件销毁时关闭连接。

8. 未清理的框架状态

  &emsp; 在某些框架（如 Vue、React）中，如果未正确清理组件状态或订阅，可能会导致内存泄漏。

  &emsp; 解决方法：
  在组件销毁时取消订阅。

**如何检测内存泄漏？**

1.Chrome DevTools

  &emsp; 使用 Memory 工具记录堆内存快照，分析内存占用。

  &emsp; 使用 Performance 工具检测内存泄漏。

2.Vue DevTools/React DevTools

  &emsp; 检查组件实例是否被正确销毁。

## 简述vue3相比vue2有哪些改进

1. 性能提升

&emsp;更快的渲染速度：Vue3 使用了基于 Proxy 的响应式系统，相比 Vue 2 的 Object.defineProperty，性能更高。

&emsp;更小的包体积：通过 Tree-shaking 支持，Vue3 的核心代码体积减少了约 40%。

&emsp;更好的编译优化：引入了编译时优化（如静态节点提升、补丁标志等），减少了运行时开销。

2. Composition API

&emsp;更好的逻辑复用：Composition API（如 setup、ref、reactive 等）解决了 Vue2 中 Options API 的逻辑复用和代码组织问题。

&emsp;更灵活的代码组织：可以将相关逻辑组织在一起，而不是分散在 data、methods、computed 等选项中。

3. 更好的 TypeScript 支持

&emsp;Vue3 完全使用 TypeScript 重写，提供了更好的类型推断和类型支持。

&emsp;Composition API 的设计也更适合 TypeScript。

4. 新的响应式系统

&emsp;基于 Proxy 实现响应式，支持更多数据类型（如 Map、Set 等）。

&emsp;解决了 Vue2 中无法检测到对象属性新增/删除的问题。

5. Fragment（片段）

&emsp;Vue 3 支持多根节点组件，不再需要强制包裹一个根元素。

6. Teleport（传送）

&emsp;新增 \<Teleport\> 组件，可以将组件渲染到 DOM 中的任意位置，适合处理模态框、通知等场景。

7. Suspense（异步组件）

&emsp;新增 \<Suspense\> 组件，可以更好地处理异步组件的加载状态。

8. 自定义渲染器

&emsp;Vue 3 提供了自定义渲染器 API，可以更容易地将 Vue 用于非 DOM 环境（如小程序、Canvas 等）。

9. 更灵活的组件 API

&emsp;emits 选项：显式声明组件触发的事件，增强可读性和维护性。

&emsp;v-model 改进：支持多个 v-model 绑定，并可以自定义修饰符。

10. 更好的逻辑分离

&emsp;provide/inject 改进：支持在 Composition API 中使用 provide 和 inject，更适合跨组件状态管理。

11. 移除或调整了一些特性

&emsp;移除了 $on、$off 和 $once 等事件 API。

&emsp;移除了 filter 过滤器，推荐使用计算属性或方法替代。

&emsp;v-bind 的 .sync 修饰符被移除，改用 v-model。

12. 更好的 DevTools 支持

&emsp;Vue 3 的 DevTools 提供了更强大的调试功能，支持 Composition API 的调试。

## vue3的Composition API是什么

&emsp;Vue 3 的 Composition API 是一种新的组织和复用逻辑的方式，旨在解决 Vue 2 中 Options API 在复杂组件中逻辑分散和难以复用的问题。Composition API 提供了更灵活和强大的工具，使开发者能够更好地组织代码，尤其是在处理复杂组件时。

**Composition API 的核心概念**

Composition API 的核心是 setup 函数，它是组件的入口点，替代了 Vue 2 中的 data、methods、computed 等选项。在 setup 函数中，你可以定义响应式数据、计算属性、方法等，并将它们返回给模板使用。

Composition API 是 Vue 3 的核心特性之一，它提供了更灵活和强大的方式来组织和复用逻辑。虽然 Options API 仍然可以使用，但在复杂场景下，Composition API 是更推荐的选择。

## ref和reactive的区别

在 Vue 3 中，ref 和 reactive 是用于创建响应式数据的两个核心 API。它们的区别主要体现在使用场景、数据类型和访问方式上。以下是它们的详细对比：

1. 数据类型

ref：

- 适用于基本数据类型（如 string、number、boolean）和对象。

- 如果传入一个对象，Vue 会将其转换为 reactive 对象。

- 返回一个包含 .value 属性的对象。

reactive：

- 仅适用于对象（包括数组和复杂对象）。

- 直接返回一个响应式代理对象。

2. 访问方式

ref：

- 需要通过 .value 访问或修改值。

- 在模板中使用时，Vue 会自动解包，无需 .value。

reactive：

- 直接访问或修改对象的属性。

- 不需要 .value。

3. 使用场景

ref：

- 适合管理单个值（如计数器、标志位等）。

- 适合需要明确区分响应式数据和非响应式数据的场景。

- 适合在组合式 API 中传递基本类型数据。

reactive：

- 适合管理复杂对象或状态（如表单数据、配置对象等）。

- 适合需要将多个相关属性组织在一起的场景。

4. 解包行为

ref：

- 在模板中自动解包，无需 .value。

- 在 reactive 对象中也会自动解包。

reactive：

- 不需要解包，直接访问属性。

5. 性能

ref：

- 对于基本类型数据，性能开销较小。

- 对于对象类型，内部会转换为 reactive，性能与 reactive 相同。

reactive：

- 对于复杂对象，性能开销与 ref 相同。

- 对于基本类型数据，不能直接使用 reactive。

6. 如何选择

使用 ref：

- 当需要管理单个基本类型数据时。

- 当需要在组合式 API 中传递响应式数据时。

- 当需要明确区分响应式数据和非响应式数据时。

使用 reactive：

- 当需要管理复杂对象或状态时。

- 当需要将多个相关属性组织在一起时。

## vue3中watch和watcheffect有何不同

在 Vue 3 中，watch 和 watchEffect 都是用于监听响应式数据变化的 API，但它们的用途和行为有一些关键区别。以下是它们的详细对比：

1.  **功能概述**

-   **`watch`**：
    
    -   用于监听特定的响应式数据源，并在数据变化时执行回调函数。
        
    -   可以监听单个或多个数据源。
        
    -   提供旧值和新值。
        
-   **`watchEffect`**：
    
    -   自动追踪其回调函数中使用的响应式数据，并在这些数据变化时重新执行回调。
        
    -   不需要显式指定监听的数据源。
        
    -   不提供旧值，只关注当前值。

2.  **使用方式**

2.1  **`watch`**

```[.js]
import { ref, watch } from "vue";

const count = ref(0);

watch(count, (newValue, oldValue) => {
  console.log(`count 从 ${oldValue} 变为 ${newValue}`);
});

// 修改 count
count.value++;
```

特点：

-   需要显式指定监听的数据源（如  `count`）。
    
-   回调函数接收两个参数：`newValue`  和  `oldValue`。

2.2 watchEffect

```[.js]
import { ref, watchEffect } from "vue";

const count = ref(0);

watchEffect(() => {
  console.log(`count 的值是 ${count.value}`);
});

// 修改 count
count.value++;
```

 特点：

-   不需要显式指定监听的数据源，自动追踪回调函数中使用的响应式数据。
    
-   回调函数没有参数，无法直接获取旧值。

3.  **使用场景**

3.1  **`watch`  的适用场景**

-   需要监听特定数据的变化，默认不立即执行。
    
-   需要获取变化前后的值（`newValue`  和  `oldValue`）。
    
-   需要控制监听的行为（如  `immediate`、`deep`  等选项）。

3.2  **`watchEffect`  的适用场景**

-   需要自动追踪多个响应式数据的变化。
    
-   不需要旧值，只关注当前值。
    
-   需要立即执行副作用。

4.  **高级用法**

4.1  **`watch`  的  `deep`  选项**

如果需要监听对象或数组的内部变化，可以使用  `deep: true`。

```[.js]
const state = reactive({ user: { name: "Alice" } });

watch(
  () => state.user,
  (newValue, oldValue) => {
    console.log("user 发生变化");
  },
  { deep: true } // 深度监听
);
```

4.2  **`watchEffect`  的清理副作用**

`watchEffect`  的回调函数可以返回一个清理函数，用于在重新运行副作用之前执行清理操作。

```[.js]
watchEffect((onCleanup) => {
  const timer = setTimeout(() => {
    console.log("执行副作用");
  }, 1000);

  onCleanup(() => {
    clearTimeout(timer); // 清理副作用
  });
});
```

5.  **总结**

-   **`watch`**：
    
    -   适合监听特定数据源，提供旧值和新值。
        
    -   支持  `immediate`  和  `deep`  等选项。
        
    -   适用于需要精确控制监听行为的场景。
        
-   **`watchEffect`**：
    
    -   自动追踪依赖，无需显式指定数据源。
        
    -   默认立即执行，适合执行副作用。
        
    -   适用于需要自动追踪多个响应式数据的场景。
        

根据具体需求选择合适的 API：

-   如果需要监听特定数据并获取旧值，使用  `watch`。
    
-   如果需要自动追踪依赖并执行副作用，使用  `watchEffect`。