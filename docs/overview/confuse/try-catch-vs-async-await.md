---
nav:
  title: 基础
  order: 1
group:
  title: 易混点
  order: 1
title: try-catch vs async-await
order: 4
---
# try-catch vs async-await
省流： 都是处理异步操作的方式，推荐使用async-await，可读性高；try-catch用于捕获异常

## try-catch
`try-catch` 用于捕获和处理代码块中的异常。
```javascript
try {
  // 可能抛出异常的代码
  let result = riskyOperation();
  console.log(result);
  return result; // 可以返回一个值
} catch (error) {
  console.error('捕获到错误:', error);
  return 'default value'; // 可以返回一个默认值
} finally {
  console.log('清理工作');
  return 'default value'; // 可以返回一个默认值，但会覆盖try中的返回值
}
```
## async-await

```javascript
async function asyncFunction() {
  let result = await riskyOperation();
  console.log(result);
}

```

##### ※可以把async-await和try-catch结合使用，语法上没问题，但为了提高可读性，一般不混用
