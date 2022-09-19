# 日历

丰富了`el-calendar`，并提供了丰富的定制化的配置，比如：星座、干支、阴历等。



## 效果

![image-20220901012712858](https://static.www.toimc.com/blog/picgo/2022/09/01/image-20220901012712858-99eb02.png)



## 用法

可以使用的参数一览：

```vue
<t-calendar
  v-model:value="value"
  :show-tool="form.showTool"
  :tool-list="toolList"
  :format="format"
  :position="form.position"
  :show-astro="form.showAstro"
  :show-gz-day="form.showGzDay"
  :show-day-cn="form.showDayCn"
  :border="form.border"
  :size="form.size"
  :inline="form.inline"
  @cell-click="onCellClick"
>
</t-calendar>
```



## 属性

| 属性名    | 说明                   | 类型                 | 可选值                                       | 默认值                                                       |
| --------- | ---------------------- | -------------------- | -------------------------------------------- | ------------------------------------------------------------ |
| showTool  | 是否显示默认工具条     | boolean              | -                                            | false                                                        |
| toolList  | 工具列表               | IToolType[]          | -                                            | ['prev-year', 'prev-month', 'today', 'next-month', 'next-year'] |
| value     | 默认日期数据           | Date, Number, String | -                                            | new Date()                                                   |
| format    | 格式化日期的自定义方法 | FormatterFuncType    | -                                            | null                                                         |
| showDayCn | 是否显示农历           | Boolean              | -                                            | false                                                        |
| showGzDay | 是否显示干支纪年法     | Boolean              | -                                            | false                                                        |
| showAstro | 是否显示星座           | Boolean              | -                                            | false                                                        |
| position  | 日历显示位置           | String               | center/left/right/left-between/right-between | ''                                                           |
| size      | 大小                   | String               | small/large/default                          | 'default'                                                    |
| border    | 是否有边框             | Boolean              | -                                            | false                                                        |
| inline    | 是否行内               | Boolean              | -                                            | false                                                        |

其他说明：

```typescript
type FormatterFuncType = (val: any) => string

const defaultTools = {
  'prev-year': '上一年',
  'prev-month': '上一月',
  today: '今天',
  'next-month': '下一月',
  'next-year': '下一年'
}

export type IToolType = keyof typeof defaultTools
```

