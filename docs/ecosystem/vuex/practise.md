---
nav:
  title: 生态
  order: 4
group:
  title: Vuex
  order: 2
title: 最佳实践
order: 3
---

```js
import { computed } from 'vue';
import { useStore } from 'vuex';

const module = 'myModule';

export default {
  setup() {
    const store = useStore();

    return {
      // getter
      one: computed(() => store.getters[`${module}/myStateVariable`]),
      // state
      two: computed(() => store.state[module].myStateVariable),
    };
  },
};
```
