---
nav:
  title: 基础
  order: 1
group:
  title: 易混点
  order: 1
title:  computed vs watch
order: 3
---
# computed vs watch

省流： 都是基于响应式数据变化来更新视图，vue内部的派生状态用computed，异步、开销大、脱离vue的交互用watch，不要滥用watch

## computed
`computed` 用于创建基于响应式数据的派生状态。它们会根据其依赖的响应式数据自动更新，并且只有在相关数据发生变化时才会重新计算。
```javascript
import { ref, computed } from 'vue';
const count = ref(0);
const doubleCount = computed(() => count.value * 2);
```
在这个例子中，`doubleCount` 是一个计算属性，它依赖于 `count`。每当 `count` 变化时，`doubleCount` 会自动更新。
##### 提问： 为什么不直接用 `count.value * 2`？
因为 `count.value * 2` 是一个普通的表达式，不具备响应式特性，无法自动更新视图。
##### 提问： `computed` 什么时候会重新计算？
`computed` 只有在其依赖的响应式数据发生变化时才会重新计算，这使得它们非常高效，避免了不必要的计算开销。
##### 提问： `computed` 可以是异步的吗？
`computed` 本身不支持异步操作，因为它们设计用于同步计算派生状态。如果需要处理异步逻辑，应该使用 `watch`。

##### computed的同步
```javascript
const count = ref(0);
const doubleCount = computed(() => {
  console.log('计算 doubleCount');
  return count.value * 2;
});
console.log(doubleCount.value); // 计算 doubleCount  输出 0
console.log(doubleCount.value); // 输出 0，没有重新计算
count.value++;
console.log(doubleCount.value); // 计算 doubleCount  输出 2 能立即拿到值
``` 
##### computed的异步
```javascript
const count = ref(0)
const double1 = computed(() => {
  setTimeout(() => {
        return count.value * 2
      }, 1000) // 实际返回undefined
})

// 你换async的方式也不起效
const double2 = computed(async () => {
  await new Promise(resolve => setTimeout(resolve, 1000)); // 模拟请求
  return count.value * 2; //实际返回Promise
})

// Promise的方式也不行
const double3 = computed(() => {
  Promise.resolve().then(() => {
    return count.value * 2; // 实际返回undefined
  });
})
``` 
## watch

`watch` 用于观察和响应响应式数据的变化。它们适用于需要在数据变化时执行副作用操作的场景，例如异步请求、手动更新 DOM 或其他非响应式逻辑。
```javascript
import { ref, watch } from 'vue';
const count = ref(0);
watch(count, (newValue, oldValue) => {
  console.log(`count 从 ${oldValue} 变为 ${newValue}`);
});


```