# 高德地图

## 效果

![image-20220808232352910](./assets/image-20220808232352910.png)



## 用法

```vue
<template>
  <div ref="wrapRef" :style="{ height, width }"></div>
</template>
<script lang="ts">
  import { defineComponent } from 'vue'

  import { useScript } from '@/hooks/useScript'

  const A_MAP_URL = 'https://webapi.amap.com/maps?v=2.0&key=0731a251568d2f64284dd681385563ce'

  export default defineComponent({
    name: 'AMap',
    props: {
      width: {
        type: String,
        default: '100%'
      },
      height: {
        type: String,
        default: 'calc(100vh - 78px)'
      }
    },
    setup() {
      const wrapRef = ref<HTMLDivElement | null>(null)
      const { toPromise } = useScript({ src: A_MAP_URL })

      async function initMap() {
        await toPromise()
        await nextTick()
        const wrapEl = unref(wrapRef)
        if (!wrapEl) return
        const AMap = (window as any).AMap
        new AMap.Map(wrapEl, {
          zoom: 11,
          center: [116.397428, 39.90923],
          viewMode: '3D'
        })
      }

      onMounted(() => {
        initMap()
      })

      return { wrapRef }
    }
  })
</script>

```



## 属性

```ts
// 地图展示区域的宽
width: {
  	type: String,
    default: '100%'
},
// 地图展示区域的高
height: {
    type: String,
    default: 'calc(100vh - 78px)'
}
```

