# Vue GuideBook

基于 [dumi@1](https://v1.d.umijs.org/zh-CN/guide) 搭建的 Vue 知识图谱，内容涵盖 Vue 基础用法、组件化、响应式原理、编译原理以及生态等方面，旨在帮助前端开发者夯实 Vue 相关基础，提供一本从概念学习过渡到实际开发的指南书。

node 14
npm 6
vue 2

- **易混淆点**
  - [v-bind vs v-model](docs/overview/confuse)
  - [watch vs computed](overview/basic/watch-vs-computed.md)
  - [ref vs reactive](docs/overview/confuse/ref-vs-reactive.md)
  - [props vs state](overview/component/props-vs-state.md)
  - [组件通信方式](overview/component/component-communication.md)
- **基本概念**
  - [指令](concept/directive.md)
  - [事件](concept/event.md)
  - [插槽](concept/slot.md)
  - [生命周期钩子函数](reactivity/lifecycle.md)
- **组件化**
- **响应式原理**
  - [生命周期](reactivity/lifecycle.md)
  - [响应式原理](reactivity/reactivity.md)
  - [批量异步更新策略](reactivity/async-update.md)
  - [nextTick](reactivity/next-tick.md)
  - [虚拟 DOM](reactivity/virtual-dom.md)
- **编译**
  - [代码编译](compiler/introduction.md)
  - parse
  - optimize
  - codegen
- **扩展**
  - event
  - v-model
  - slot
  - keep-alive
  - transition
- **生态**
  - Vue Router
  - Vuex
  - Vue Query
  - Vue Store
  - Pinia
  - Nuxt
