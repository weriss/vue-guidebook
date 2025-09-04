---
nav:
    title: 基础
    order: 1
group:
    title: 代码审查
    order: 1
title: 代码审查清单
order: 1
---

## 代码审查清单

### 1. 缩进与样式

- 检查自闭合标签是否规范
- 模板与脚本缩进是否正确，避免排版错误
- 减少 `if` 等嵌套层级
- `import` 顺序：第三方库在上，内部组件在下

### 2. 命名规范

- 变量名：使用具体名词，布尔类型建议 `isXXX`、`hasXXX` 或 `XXXable`
- 函数名：动宾结构（如 `getList`、`loadList`），事件处理用 `onXXXChange`
- 组件事件监听：如 `@click`、`@select-change`
- 组件绑定变量名需清晰

### 3. 删除冗余配置

### 4. 异步处理

- 优先使用 `async-await`（可读性好），并行请求用 `Promise.all`

### 5. 响应式处理

- 优先使用 `ref` 替代 `reactive`，对象赋值用 `ref.value`
- 使用 `?` 进行短路链式调用，`??` 进行空值合并

### 6. 函数声明

- 使用 `function` 声明函数以获得作用域提升

### 7. Vue 特性检查

- `nextTick` 是否必要
- `watch` 是否必要
- 避免重复枚举、重复获取值
- 尽量将命令式代码（如 `watch` 后调用 API 手动更改）改为 `computed` 等自动依赖更新
