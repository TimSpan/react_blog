# Vuex4

## 1_组合式API

可以通过调用 `useStore` 函数，来在 `setup` 钩子函数中访问 store。这与在组件中使用选项式 API 访问 `this.$store` 是等效的。

```js
import { useStore } from 'vuex'

export default {
  setup () {
    const store = useStore()
  }
}
```

### 访问 State 和 Getter

为了访问 state 和 getter，需要创建 `computed` 引用以保留响应性，这与在选项式 API 中创建计算属性等效。

```js
import { computed } from 'vue'
import { useStore } from 'vuex'

export default {
  setup () {
    const store = useStore()

    return {
      // 在 computed 函数中访问 state
      count: computed(() => store.state.count),

      // 在 computed 函数中访问 getter
      double: computed(() => store.getters.double)
    }
  }
}
```

### 访问 Mutation 和 Action

要使用 mutation 和 action 时，只需要在 `setup` 钩子函数中调用 `commit` 和 `dispatch` 函数。

```js
import { useStore } from 'vuex'

export default {
  setup () {
    const store = useStore()

    return {
      // 使用 mutation
      increment: () => store.commit('increment'),

      // 使用 action
      asyncIncrement: () => store.dispatch('asyncIncrement')
    }
  }
}
```



## 2_创建

### 3使用`new Vuex.Store(`)创建

首先使用`new Vuex.Store()`创建`store`实例。

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

const store = new Vuex.Store({
  state: {
    count: 0
  },
  mutations: {
    increment (state) {
      state.count++
    }
  }
})
```

然后在创建`Vue`实例的时候把`store`传递进去。

```js
new Vue({
  el: '#app',
  store: store,
})
```

### 4使用`createStore()`创建

首先使用`createStore()`创建`store`实例。

```js
import { createStore } from 'vuex'

// 创建一个新的 store 实例
const store = createStore({
  state () {
    return {
      count: 0
    }
  },
  mutations: {
    increment (state) {
      state.count++
    }
  }
})

```

然后再创建`Vue`实例，并将 `store` 实例作为插件安装。

```js
import { createApp } from 'vue'

const app = createApp({ /* 根组件 */ })

// 将 store 实例作为插件安装
app.use(store)
```




## 3_获取

`Vuex3`和`Vuex4`在获取方面有点差别，但是在使用方面并没有差别。

### 3使用`this.$store`获取store

`Vuex3`使用`this.$store`来获取`store`并进行操作。

```js
this.$store.state // 获取state
this.$store.getters // 获取getters
this.$store.commit // 提交mutation
this.$store.dispatch // 提交action
```

### 4使用`useStore`获取store

`Vuex4`使用`useStore()`来获取`store`并进行操作。

```js
import {useStore} from 'vuex'

const store = useStore()

store.state // 获取state
store.getters // 获取getters
store.commit // 提交mutation
store.dispatch // 提交action
```

虽然`Vuex4`推荐使用`useStore()`来获取`store`。但是并没有移除`this.$store`，但是在`<template>`和`Vue2`选项式写法中还是支持使用`$store`的。



### Vuex3和Vuex4都支持使用`$store`

在模板中使用

```html
<template>
  <div>{{$store.state.count}}</div>
</template>
复制代码
```

在选项式写法中使用

```js
export default {
  mounted() {
    console.log(this.$store);
  }
}
```



## 4_辅助函数

在`Vuex3`中是可以使用辅助函数`mapState、mapGetters、 mapMutations、mapActions`来简化我们`store`的操作的。

在`Vuex4`中并没有删除，还是可以使用，但是只能在`Vue2`的那种选项式写法中存在，如果想要使用组合式写法`setup`，是没办法使用的。



















