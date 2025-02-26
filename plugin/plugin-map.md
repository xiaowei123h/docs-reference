# 地图

首先注册地图开发者账号，获取apikey

[腾讯位置服务](https://lbs.qq.com/)、[百度地图开放平台](https://lbsyun.baidu.com/)、[高德开放平台](https://lbs.amap.com/)任选其一即可

以下例子为腾讯地图

```[sh]
npm i @vueuse/core
```

```[.ts]
import { useScriptTag } from '@vueuse/core'

// tencent sdk url
const TENCENT_MAP_SDK_URL = 'https://map.qq.com/api/gljs?v=1.exp&key=A6DBZ-KXPLW-JKSRY-ONZF4-CPHY3-K6BL7'

const { load } = useScriptTag(TENCENT_MAP_SDK_URL)

// const map = ref(null)

async function renderMap() {
  const map = document.getElementById('map')
  await load(true);
  if (!map) return;
  // @ts-ignore
  new TMap.Map(map, {
    // @ts-ignore
    center: new TMap.LatLng(39.98412, 116.307484),
    zoom: 11,
    viewMode: '3D'
  });
}

onMounted(() => {
  renderMap();
})
```

```[.vue]
<el-card class="card-w">
  <div id="map"></div>
</el-card>
```