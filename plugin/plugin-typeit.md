# 打字机

**安装**

```[sh]
npm i typeit
```

**使用**

```[.ts]
import TypeIt from 'typeit';
import type { Options } from 'typeit';

function init() {
  const text = document.getElementById('text')
  if (!text) return;

  const options: Options = {
    strings: 'Vue Admin Reference是个人使用中整理的前端工具手册，旨在帮助自己在日常开发中快速查阅和使用各种工具，提升工作效率和代码质量。同时将这份手册分享给其他开发者，希望能为大家提供一些实用的参考和帮助。',
    lifeLike: true,
    speed: 120,
    loop: true
  };

  const initTypeIt = new TypeIt(text, options);

  initTypeIt.go();
}

onMounted(() => {
  init();
});
```

```[.vue]
<el-card class="card-w">
  <div id="text" class="h-400px"></div>
</el-card>
```