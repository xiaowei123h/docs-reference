# dhtmlx甘特图

[官网文档](https://docs.dhtmlx.com/gantt/desktop__install_with_bower.html)

**安装**

```[sh]
npm install dhtmlx-gantt
```

**使用**

```[.ts]
import { gantt } from 'dhtmlx-gantt'
import type { GanttConfigOptions, ZoomLevel, Task } from 'dhtmlx-gantt'
import 'dhtmlx-gantt/codebase/dhtmlxgantt.css'

const ganttTasks: Task[] = [
  {
    id: 11,
    text: 'Soybean 架构设计',
    type: 'project',
    progress: 0,
    open: true,
    start_date: new Date('2024-01-10 00:00'),
    duration: 12,
    parent: 0
  },
  {
    id: 12,
    text: '测试版本',
    start_date: new Date('2024-03-20 00:00'),
    type: 'project',
    duration: 5,
    render: 'split',
    parent: '11',
    progress: 0,
    open: true
  },
  {
    id: 99,
    text: '测试版本1 发布',
    start_date: new Date('2024-03-20 00:00'),
    end_date: new Date('2024-03-25 00:00'),
    parent: '12',
    progress: 0,
    open: true
  },
]

onMounted(() => {
  // 设置中文
  gantt.i18n.setLocale('cn')

  gantt.init('dhtmlx-gantt')

  gantt.parse({data: ganttTasks})
})
```

```[.vue]
<el-card class="card-w h-100%">
  <div id="dhtmlx-gantt" class="h-100%"></div>
</el-card>
```

```[.css]
:deep(.el-card__body) {
  height:100%
}
```

适配移动端，移动端任务栏太宽导致看不到后面内容，所以修改任务栏只显示一个任务名

```[.ts]
onMounted(() => {
  const div = document.querySelector('div')
  // @ts-ignore
  const computedStyle = window.getComputedStyle(div)

  // 适配移动端，移动端只显示任务名
  if (Number(computedStyle.width.replace("px", "")) < 650) {
    gantt.config.columns = [
      { name: "text", label: "任务名", width: 100 }, // 只显示任务名称
      { name: "add", label: "", width: 40 }, // 空列，用于显示添加任务按钮
    ]
  }
})
```

**注意**

dhtmlx-gantt如果动态设置高度，在页面添加其他组件及内容容易引起内存泄漏，会因为高度改变导致甘特图一直动弹获取高度。

解决办法，固定高度，或通过计算固定高度，或不添加其他组件内容。