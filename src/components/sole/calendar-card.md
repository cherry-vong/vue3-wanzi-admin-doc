# 日历卡片

封装了`el-calendar`组件，可以设置小组件显示的布局、文字的大小、阴影与是否在行内显示。

## 效果

![几种日历效果](https://static.www.toimc.com/blog/picgo/2022/08/30/image-20220830002615061-cf3ae6.png)

## 用法

示例用法：

```vue
<div class="p-4">
  <div class="pb-4">行内</div>
  <calendar-card layout="left" width="200" class="mb-2 mr-4" inline></calendar-card>
  <calendar-card layout="left" width="200" class="mb-2" inline shadow></calendar-card>
  <div class="pb-4">居右</div>
  <calendar-card layout="right" class="mb-2"></calendar-card>
  <calendar-card r-card class="mb-2"></calendar-card>
  <div class="pb-4">设置字体大小</div>
  <calendar-card width="600" font-size="30" height="300"></calendar-card>
</div>
```



## 属性

```typescript
// 卡片宽度
width: {
  type: [Number, String],
  default: 350
},
// 卡片高度
height: {
  type: [Number, String],
  default: null
},
// 卡片布局
layout: {
  type: String as PropType<'left' | 'right' | 'all'>,
  default: 'all'
},
// 卡片文字大小
fontSize: {
  type: [Number, String],
  default: 22
},
// 是否为行内组件
inline: {
  type: Boolean,
  default: false
},
// 是否显示阴影
shadow: {
  type: Boolean,
  default: false
}
```