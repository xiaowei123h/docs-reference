# pdf在线预览

**安装**

```[sh]
npm install vue-pdf-embed
```

**使用**

```[.ts]
import pdf from 'vue-pdf-embed'
```

引用本地pdf，文件在public文件夹下

```[.vue]
<el-card class="card-w">
  <pdf source="/sample.pdf"></pdf>
</el-card>
```