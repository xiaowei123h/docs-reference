# 条形码

生成条形码

安装

```sh
npm install jsbarcode
```

使用

（barcode.vue）
```[barcode.vue]
<script setup lang="ts">
import JsBarcode from 'jsbarcode'
import type { Options } from 'jsbarcode'

const text = 'Reference';

interface CodeConfig {
  id: string;
  title: string;
  text: string;
  options: Options;
}

const codes: CodeConfig[] = [
  {
    id: 'code39',
    title: '样式1',
    text: 'Hello',
    options: { format: 'code39' }
  },
  {
    id: 'code128',
    title: '样式2',
    text,
    options: {}
  },
  {
    id: 'ean-13',
    title: '样式3',
    text: '1234567890128',
    options: { format: 'ean13' }
  },
  {
    id: 'upc-a',
    title: '样式4',
    text: '123456789012',
    options: { format: 'upc' }
  },
  {
    id: 'barcode',
    title: '样式5',
    text: 'Hello',
    options: {
      height: 30,
      lineColor: '#9ca3af'
    }
  },
  {
    id: 'barcode1',
    title: '样式6',
    text,
    options: {
      background: '#9ca3af',
      lineColor: '#ffffff'
    }
  },
  {
    id: 'barcode2',
    title: '样式7',
    text,
    options: {
      fontSize: 40
    }
  },
  {
    id: 'barcode3',
    title: '样式8',
    text: 'Hi',
    options: {
      textMargin: 30,
      width: 4
    }
  },
  {
    id: 'barcode4',
    title: '样式9',
    text,
    options: {
      textPosition: 'top',
      fontOptions: 'bold'
    }
  }
];

function generateBarcode() {
  codes.forEach(code => {
    JsBarcode(`#${code.id}`, code.text, code.options)
  });
}

// generateBarcode()

onMounted(() => {
  generateBarcode()
})
</script>

<template>
  <div class="p-16 barcode-wrapper">
    <el-card header="条形码" shadow="never" class="card-w h-100%">
      <el-row :gutter="12" class="row-w">
        <el-col v-for="item in codes" :key="item.id" :lg="8" :md="12" :sm="24" class="m-b-24">
        <div class="flex-c d-c">
          <div class="w-50px">
            <h3>{{ item.title }}</h3>
          </div>
          <div>
            <svg :id="item.id" class="h-130px w-250px"></svg>
          </div>
        </div>
        </el-col>
      </el-row>
    </el-card>
  </div>
</template>

<style scoped>
.row-w {
  width: calc(100%-12px);
}
</style>
```