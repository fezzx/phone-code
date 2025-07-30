# PhoneCode 验证码输入组件使用文档

## 组件简介
PhoneCode 是一个美观易用的验证码输入组件，支持多种边框样式：1-下边框，2-全边框，3-无边框

## 组件截图
<img width="658" height="1096" alt="123456" src="https://github.com/user-attachments/assets/dcb7a638-f2c6-4483-b829-eabbb7284855" />


## 基本用法

```vue
<template>
  <phone-code ref="phoneCodeRef" 
              @code-completed="handleInputCompleted"
              @input-change="handleInputChange">
  </phone-code>
</template>

<script>
export default {
  methods: {
    handleInputCompleted(completeCode) {
      // 验证码输入完成时触发
      console.log('完整验证码:', completeCode)
    },
    handleInputChange(partialCode) {
      // 验证码输入变化时触发
      console.log('当前输入:', partialCode)
    }
  }
}
</script>
````

## 属性说明

| 属性名                | 类型     | 默认值       | 可选值                        | 说明                     |
| ------------------ | ------ | --------- | -------------------------- | ---------------------- |
| borderType         | Number | 1         | 1/2/3                      | 边框类型：1-下边框，2-全边框，3-无边框 |
| borderDefaultColor | String | '#aaaaaa' | 任何合法颜色值                    | 默认边框颜色                 |
| borderFocusColor   | String | '#2f6df5' | 任何合法颜色值                    | 聚焦时边框颜色                |
| digitLength        | Number | 6         | 正整数                        | 验证码位数                  |
| inputType          | String | 'number'  | 'number'/'text'/'password' | 输入类型                   |

## 事件说明

| 事件名            | 返回值      | 触发时机                    |
| -------------- | -------- | ----------------------- |
| code-completed | 完整验证码字符串 | 当输入位数达到 digitLength 时触发 |
| input-change   | 当前输入内容   | 每次输入内容变化时触发             |

## 样式示例

### 1. 默认样式（下边框）

```vue
<phone-code></phone-code>
```

### 2. 全边框样式

```vue
<phone-code :borderType="2"></phone-code>
```

### 3. 自定义颜色全边框样式

```vue
<phone-code :borderType="2" 
           borderDefaultColor="#000000" 
           borderFocusColor="#70DB93"
           inputType="text">
</phone-code>
```

### 4. 无边框样式

```vue
<phone-code :borderType="3"></phone-code>
```

## 方法说明

通过 ref 可以调用组件方法：

| 方法名     | 说明    |
| ------- | ----- |
| focus() | 聚焦输入框 |
| blur()  | 失焦输入框 |
| clear() | 清空输入  |

使用示例：

```javascript
this.$refs.phoneCodeRef.focus()  // 聚焦输入框
this.$refs.phoneCodeRef.clear()  // 清空输入
```

## 注意事项

1.  当 inputType="number" 时，组件会自动过滤非数字字符
2.  生产环境建议移除 console.log 调试代码
3.  如需自定义样式，可通过覆盖 CSS 变量实现

## 版本记录

*   v1.0.0 (2025-08-01): 首次发布

