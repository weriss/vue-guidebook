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
# then-catch vs async-await
省流： 都是处理异步操作的方式，推荐使用async-await，可读性高，加上用于捕获异常的try-catch，可以使异步代码看起来像同步代码；then-catch(Promise链)，用于处理Promise中的异步操作。

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
## try-catch + async-await
```javascript
async function getUserInfo() {
  try {
    const user = await fetchUserData();
    console.log('用户数据:', user);
    
    const posts = await fetchUserPosts(user.id);
    console.log('用户文章:', posts);
  } catch (error) {
    console.error('错误:', error);
  } finally {
    console.log('请求完成');
  }
}
```

## then-catch
```javascript
// Promise链式调用
fetchUserData()
  .then(user => {
    console.log('用户数据:', user);
    return fetchUserPosts(user.id);
  })
  .then(posts => {
    console.log('用户文章:', posts);
  })
  .catch(error => {
    console.error('错误:', error);
  })
  .finally(() => {
    console.log('请求完成');
  });

```