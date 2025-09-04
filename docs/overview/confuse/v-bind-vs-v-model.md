---
nav:
  title: 基础
  order: 1
group:
  title: 易混点
  order: 1
title: v-bind vs v-model
order: 1
---
# v-bind vs v-model

省流：都是数据绑定，`v-bind` 单向， `v-model`双向

## v-bind
`v-bind` 单向数据绑定，数据变化会影响视图，视图变化不会影响数据。

```html
<!-- 绑定单个属性 -->
<img v-bind:src="imageSrc" alt="Image">
<!-- 绑定多个属性 -->
<div v-bind="{ id: dynamicId, class: dynamicClass }"></div>
<!-- 简写形式 -->
<div :id="dynamicId" :class="dynamicClass"></div>
```


##### 提问： 为什么不直接用 `src="imageSrc"`？
因为 `src="imageSrc"` 会将 `imageSrc` 作为字符串字面量处理，而不是变量。

##### 提问： `v-bind` 绑定的属性会自动更新吗？
是的，`v-bind` 绑定的属性会随着 Vue 实例中对应数据的变化而自动更新。但因为其是单向的，所以数据变化会反映到视图上，但视图的变化不会影响数据。

##### 提问： `v-bind` 可以绑定哪些属性？可以绑定对象吗？
`v-bind` 可以绑定任何 HTML 属性、组件的 props 以及自定义属性。可以绑定对象，使用对象语法可以一次性绑定多个属性。

## v-model
`v-model` 双向数据绑定，视图变化会影响数据，数据变化也会影响视图。
```html
<input v-model="inputValue" placeholder="请输入内容">
```
##### 提问： `v-model` 可以绑定对象吗？数据会自动更新吗？
`v-model` 可以，但要更新需要通过modelValue接受，再emit出去。
```html
<!-- 父组件 -->
<HelloWorld v-model="formData" />
...下面定义formData
```
```javascript
// 子组件 HelloWorld.vue
<template>
  <div>
    <h1 >{{ modelValue.name }}</h1>
    <h2 >{{ modelValue.email }}</h2>
    <h3 >{{ modelValue.password }}</h3>

  </div>
</template>

<script setup>
defineProps({
  modelValue: {
    type: Object,
    required: true,
  },
})

const emit = defineEmits(['update:modelValue'])

function updateValue(newValue) {
  emit('update:modelValue', newValue)
}

setTimeout(() => {
  updateValue({
    name: 'new name',
    email: 'new email',
    password: 'new password'
  })
}, 2000)

</script>
```


