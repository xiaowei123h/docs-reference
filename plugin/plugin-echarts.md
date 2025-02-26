# Echarts

[Echarts官网](https://echarts.apache.org/zh/index.html)

## 使用

**安装**

```[sh]
npm install echarts
```

具体使用可直接参考官网用例

**注意**

vue在onMounted中使用document.getElementById('echarts')

配合以下代码自适应窗口大小使用更优

```[.js]
// ResizeObserver 实例
let resizeObserver: ResizeObserver | null = null;

let chartDom: HTMLElement | null = null

onMounted(() => {
  // 使用 ResizeObserver 监听容器大小变化
  resizeObserver = new ResizeObserver(() => {
    myChart.resize();
  });
  resizeObserver.observe(chartDom);
})

// 在组件销毁时取消监听
onBeforeUnmount(() => {
  resizeObserver.unobserve(chartDom);
});
```