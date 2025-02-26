# 富文本编辑器

[官方文导](https://www.wangeditor.com/)

**安装**

```[sh]
npm install @wangeditor/editor --save
```

```[sh]
npm install @wangeditor/editor-for-vue@next --save
```

**使用**

```[.ts]
import '@wangeditor/editor/dist/css/style.css' // 引入 css

import { onBeforeUnmount, ref, shallowRef, onMounted } from 'vue'
import { Editor, Toolbar } from '@wangeditor/editor-for-vue'

// 编辑器实例，必须用 shallowRef
const editorRef = shallowRef()

// 内容 HTML
const valueHtml = ref('<p>hello</p>')

const mode = ref('default')

// 模拟 ajax 异步获取内容
onMounted(() => {
  setTimeout(() => {
    valueHtml.value = '<p>模拟 Ajax 异步设置内容</p>'
  }, 1500)
})

const toolbarConfig = {}
const editorConfig = { placeholder: '请输入内容...' }

// 组件销毁时，也及时销毁编辑器
onBeforeUnmount(() => {
  const editor = editorRef.value
  if (editor == null) return
  editor.destroy()
})

const handleCreated = (editor: any) => {
  editorRef.value = editor // 记录 editor 实例，重要！
}
```

```[.vue]
<el-card class="card-w">
  <Toolbar
    style="border: 1px solid #ccc;border-bottom: none;"
    class="border"
    :editor="editorRef"
    :defaultConfig="toolbarConfig"
    :mode="mode"
  />
  <Editor
    style="border: 1px solid #ccc;height: 500px; overflow-y: hidden;"
    class="border"
    v-model="valueHtml"
    :defaultConfig="editorConfig"
    :mode="mode"
    @onCreated="handleCreated"
  />
</el-card>
```