# Markdown编辑器

[github地址](https://github.com/Vanessa219/vditor)

**安装**

```[sh]
npm install vditor --save
```

**使用**

```[.js]
import Vditor from 'vditor'
import 'vditor/dist/index.css'

onMounted(() => {
  const vditor = new Vditor('md-editor', {
    minHeight: 400,
    theme: 'classic',
    icon: 'material',
    cache: { enable: false }
  })
})
```

```[.vue]
<div id="md-editor"></div>
```