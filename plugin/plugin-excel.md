# Excel导出

**安装**

```[sh]
npm i xlsx
```

**使用**

```[.ts]
import { utils, writeFile } from 'xlsx'
import { Folder } from "@element-plus/icons-vue"

interface User {
  id: number
  date: string
  name: string
  address: string
}

// 表格数据
const tableData: User[] = [
  {
    id: 1,
    date: '2016-05-02',
    name: 'wangxiaohu',
    address: 'No. 189, Grove St, Los Angeles',
  },
  {
    id: 2,
    date: '2016-05-04',
    name: 'wangxiaohu',
    address: 'No. 189, Grove St, Los Angeles',
  },
  {
    id: 3,
    date: '2016-05-01',
    name: 'wangxiaohu',
    address: 'No. 189, Grove St, Los Angeles',
  },
  {
    id: 4,
    date: '2016-05-03',
    name: 'wangxiaohu',
    address: 'No. 189, Grove St, Los Angeles',
  },
]

// 自定义中文表头
const headers = {
  id: 'id',
  name: '姓名',
  date: '日期',
  address: '地址',
};

function exportExcel() {
  // 创建工作簿
  const workBook = utils.book_new()

  // 创建sheet对象，每一个sheet对象都是一个表格
  const workSheet = utils.json_to_sheet(tableData, {
    header: Object.keys(headers), // 使用原始字段名
    skipHeader: true, // 跳过自动生成表头
  })

  // 手动设置中文表头
  utils.sheet_add_aoa(workSheet, [Object.values(headers)], { origin: 'A1' });

  // 将sheet对象加到工作簿
  utils.book_append_sheet(workBook, workSheet, '用户列表')

  // 下载表格
  writeFile(workBook, '用户数据.xlsx')
}
```

```[.vue]
<el-card class="card-w">
  <el-button type="primary" :icon="Folder" class="m-b-20" style="float: right;" @click="exportExcel">导出Excel</el-button>
  <el-table
  :data="tableData"
    style="width: 100%"
    row-key="id"
    border
    lazy
  >
    <el-table-column prop="date" label="日期" />
    <el-table-column prop="name" label="姓名" />
    <el-table-column prop="address" label="地址" />
  </el-table>
</el-card>
```