---
nav:
  title: 基础
  order: 1
group:
  title: 易混点
  order: 1
title: ref vs reactive
order: 2
---
# ref vs reactive

省流： 都用于创建响应式对象，推荐使用ref而不是reactive

## ref
`ref` 用于创建一个包含单个值的响应式引用对象。它可以包装任何类型的值，包括基本类型（如字符串、数字、布尔值）和复杂类型（如对象、数组）。

```javascript
import { ref } from 'vue';
const formData = ref({
  name: 'weriss',
  email: 'weriss@example.com',
  password: 'password123'
})
```
通过`formData.value` 访问和修改其值：

```javascript
console.log(formData.value.name); // 访问属性
formData.value.name = 'newName'; // 修改属性
```

## reactive
`reactive` 用于创建一个响应式对象，适用于包含多个属性的复杂对象。它只能包装对象类型，不能直接包装基本类型。

```javascript
import { reactive } from 'vue';
const formData = reactive({
  name: 'weriss',
  email: 'weriss@example.com',
  password: 'password123'
})
```
通过直接访问和修改其属性：

```javascript
console.log(formData.name); // 访问属性
formData.name = 'newName'; // 修改属性
```

##### 为什么推荐使用 `ref` 而不是 `reactive`？
ref也能包装复杂数据，而且重置对象时，ref更方便

考虑这样一个场景，你有一个包含多个属性的表单对象 `formData`，当用户提交表单后，你希望将表单重置为默认值。
你有一个默认值对象 `defaultFormData`：

```javascript
const defaultFormData = { name: 'weriss', email: '', password: '' };
```
然而你为了渲染的方便，给表单的数据对象添加了额外的属性，例如 `isSubmitting` 用于表示表单是否正在提交：

```javascript
const formData = ref({
  name: 'weriss',
  email: 'weriss@example.com',
  password: 'password123',
  isSubmitting: false
});
```
当你想要重置 `formData` 时，如果使用 `ref`，你可以直接将其值设置为一个新的对象：

```javascript
// 使用 ref
formData.value = defaultFormData
```
如果使用 `reactive`，你直接赋值会导致响应式丢失：

```javascript
// 使用 reactive
formData = defaultFormData // 这样会丢失响应式
```

若想保证响应式，你可能会用Object.assign：

```javascript
Object.assign(formData, defaultFormData) // 需要手动合并属性
```
但这样formData中的isSubmitting属性仍会保存下来，多余的属性清不干净。

因此，使用 `ref` 可以更方便地重置整个对象，同时保持响应式特性。
