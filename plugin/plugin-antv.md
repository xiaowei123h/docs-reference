# AntV G6

[Antv G6官方文档](https://g6.antv.vision/)

## 安装

::: code-group

```sh [npm]
npm install @antv/g6 --save
```

```sh [pnpm]
pnpm add @antv/g6
```

```sh [yarn]
yarn add @antv/g6
```

:::

## 使用

**注意：请不要将 Vue 响应式数据直接传递给 G6 实例，这可能会导致 G6 无法正确渲染，甚至导致页面崩溃。**

```[.vue]
<script lang="ts" setup>
import { Graph } from '@antv/g6'

onMounted(() => {
  const div = document.getElementById('container') as HTMLElement
  const width = Number(window.getComputedStyle(div).width.replace('px', ''))
  const height = Number(window.getComputedStyle(div).height.replace('px', ''))
  const graph = new Graph({
    container: div,
    width: width,
    height: height,
    // data: {
    //   // 两个节点的，id，位置
    //   nodes: [
    //     {
    //       id: 'node-1',
    //       style: { x: 50, y: 100 },
    //     },
    //     {
    //       id: 'node-2',
    //       style: { x: 150, y: 100 },
    //     },
    //   ],
    //   // 边，连接source起始节点和target终止节点
    //   edges: [{ id: 'edge-1', source: 'node-1', target: 'node-2' }],
    // },
    // 布局算法，自动调整节点位置
    data: {
      nodes: Array.from({ length: 10 }).map((_, i) => ({ id: `node-${i}` })),
      edges: Array.from({ length: 9 }).map((_, i) => ({ source: `node-0`, target: `node-${i + 1}` })),
    },
    layout: {
      // 布局类型
      type: 'd3-force',
    },
    node: {
      // 节点类型
      // type: (datum) => datum.id === 'node-1' ? 'circle' : 'rect',
      // 节点样式
      style: {
        // 填充颜色
        // fill: 'pink',
        // 节点大小
        size: 20
      },
      // 便捷设置颜色
      palette: {
        field: 'category',
        color: 'tableau',
      },
    },
    edge: {
      // 边样式
      style: {
        // 描边颜色
        stroke: 'lightgreen',
      },
    },
    // 交互动作，拖拽，缩放画布，缩放节点
    behaviors: ['drag-canvas', 'zoom-canvas', 'drag-element']
  })

  graph.render()
})
</script>

<template>
  <div class="p-16">
    <el-card class="card-w">
      <div id="container"></div>
    </el-card>
  </div>
</template>
```