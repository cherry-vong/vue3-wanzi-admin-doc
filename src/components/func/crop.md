# 图片裁剪

封装了`cropper.js`，一个兼容性非常好的裁剪库，官网地址：[cropper.js](https://fengyuanchen.github.io/cropperjs/)，二次封装的基础组件：

- [Cropper.vue](https://github.com/toimc-team/vue3-toimc-admin/blob/main/src/components/Cropper/Cropper.vue)：裁剪基础组件
- [CropperAvatar.vue](https://github.com/toimc-team/vue3-toimc-admin/blob/main/src/components/Cropper/CropperAvatar.vue)：头像裁剪
- [CropperModal.vue](https://github.com/toimc-team/vue3-toimc-admin/blob/main/src/components/Cropper/CropperModal.vue)：裁剪模态框（裁剪选择器）



## 用例

![cropper](./assets/cropper.gif)



## 头像裁剪

### 示例代码

代码路径：[Cropper.vue](https://github.com/toimc-team/vue3-toimc-admin/blob/main/src/views/components/cropper/index.vue#L7)

```vue
<el-row>
  <el-col :span="12">
    <cropper-avatar :image="img"></cropper-avatar>
  </el-col>
  <el-col :span="12">
    <cropper-avatar :image="img">
      <template #trigger>
        <el-button>自定义trigger</el-button>
      </template>
    </cropper-avatar>
  </el-col>
</el-row>
```

使用的是基础组件`CropperAvatar.vue`



### 基础属性

```js
props: {
  image: {
    type: String,
    default: ''
  },
  shape: {
    type: String as PropType<'circle' | 'square'>,
    default: 'circle'
  },
  size: {
    type: [Number, String] as PropType<number | 'large' | 'default' | 'small'>,
    default: 200
  },
  alt: {
    type: String,
    default: ''
  },
  fit: {
    type: String as PropType<'fill' | 'contain' | 'cover' | 'none' | 'scale-down'>,
    default: 'cover'
  },
  showBtn: {
    type: Boolean,
    default: true
  }
},
```

说明：

- `image`为被裁剪的图片源；
- `shape`指定裁剪的形状，支持圆形/方形；
- `size`设置裁剪的区域，可以设置`large|default|small`，或者设置`number`像素点，默认200px；
- `alt`图片加载失败之后显示的内容；
- `fit`图片填充的模式；
- `showBtn`是否显示按钮；



## 开关裁剪&预览

### 示例代码

```vue
<template>
  <div class="p-4">
    <el-card header="图片裁剪">
      <div class="pb-4">矩形裁剪</div>
      <el-row>
        <el-col :span="12" class="px-10">
          <cropper
            v-if="img"
            :src="img"
            height="300px"
            :options="{ aspectRatio: 1 }"
            @cropend="handleCropend"
            @ready="handleReady"
          ></cropper>
        </el-col>
        <el-col :span="12">
          <img
            v-if="previewSource"
            class="h-[300px] w-[300px]"
            :src="previewSource"
            alt="预览图片"
          />
        </el-col>
        <p class="pt-4">裁剪后图片信息：{{ info }}</p>
      </el-row>
      <el-divider></el-divider>
      <div class="pb-4">圆形裁剪</div>
      <el-row>
        <el-col :span="12" class="px-10">
          <cropper
            v-if="img"
            :src="img"
            circled
            height="300px"
            :options="{ aspectRatio: 1 }"
            @cropend="handleCropendCircle"
            @ready="handleReadyCircle"
          ></cropper>
        </el-col>
        <el-col :span="12">
          <img
            v-if="previewSourceCircle"
            class="h-[300px] w-[300px]"
            :src="previewSourceCircle"
            alt="预览图片"
          />
        </el-col>
        <p class="pt-4">裁剪后图片信息：{{ infoCircle }}</p>
      </el-row>
    </el-card>
  </div>
</template>

<script lang="ts">
  import { defineComponent } from 'vue'
  import { CropendResult, Cropper } from '@/components/Cropper/typing'
  import img from '@/assets/images/brian.jpg'
  export default defineComponent({
    setup() {
      const cropper = ref<Cropper>()
      const previewSource = ref('')
      const info = ref()

      const cropperCircle = ref<Cropper>()
      const previewSourceCircle = ref('')
      const infoCircle = ref()

      function handleCropend({ imgBase64, imgInfo }: CropendResult) {
        info.value = imgInfo
        previewSource.value = imgBase64
      }

      function handleReady(cropperInstance: Cropper) {
        cropper.value = cropperInstance
      }

      function handleCropendCircle({ imgBase64, imgInfo }: CropendResult) {
        infoCircle.value = imgInfo
        previewSourceCircle.value = imgBase64
      }

      function handleReadyCircle(cropperInstance: Cropper) {
        cropperCircle.value = cropperInstance
      }
      return {
        img,
        previewSource,
        info,
        previewSourceCircle,
        infoCircle,
        handleCropend,
        handleReady,
        handleCropendCircle,
        handleReadyCircle
      }
    }
  })
</script>

<style scoped></style>
```



### 基础属性

组件定义：[Cropper.vue](https://github.com/toimc-team/vue3-toimc-admin/blob/main/src/components/Cropper/Cropper.vue#L44)

```js
src: { type: String, required: true },
alt: { type: String },
circled: { type: Boolean, default: false },
realTimePreview: { type: Boolean, default: true },
height: { type: [String, Number], default: '360px' },
crossorigin: {
type: String as PropType<'' | 'anonymous' | 'use-credentials' | undefined>,
default: undefined
},
imageStyle: { type: Object as PropType<CSSProperties>, default: () => ({}) },
options: { type: Object as PropType<Options>, default: () => ({}) }
```

属性说明：

- `src`图片源；
- `alt`图片加载失败之后显示的内容；
- `circled`是否是圆形裁剪，默认是方形；
- `realTimePreview`是否支持实时预览，默认为`true`;
- `height`裁剪图片的高度，默认`360px`；
- `crossorigin`图片跨域设置；
- `imageStyle`图片的css属性；
- `options`传递给`cropper.js`的属性；

