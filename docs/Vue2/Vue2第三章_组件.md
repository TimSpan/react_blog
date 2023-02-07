---
sidebar_position: 3
---

# Vue2第三章_组件

.vue单组件文件

## 在ESM中全局注册

```html
App.vue

<template>
  <div id="app">
    <!-- 使用组件:组件名当做标签使用 -->
    <pannel />
  </div>
</template>
```

组件全局注册语法

```js
main.js

import Vue from 'vue'
import App from './App.vue'
import pannel from './components/pannel.vue'
Vue.component("pannel",pannel)
new Vue({
  render: h => h(App)
}).$mount('#app')

```



:::tip  scoped

**注册的组件  pannel.vue 里style标签 必须加上 scoped属性**

:::

:::tip 注意

记住**全局注册的行为必须在根 Vue 实例 (通过 `new Vue`) 创建之前发生**。

:::







## 在ESM中局部注册

```html
App.vue

<template>
  <div id="app">
    <pannel />
  </div>
</template>
<script>
import pannel from './components/pannel.vue'
export default {
  components: {
    "pannel": pannel
  }
}
</script>

```



使用组件

```html
<!-- 单双标签都一样 -->
<!-- 组件名当做标签使用 -->
<!-- <组件名 /> -->
<!-- <组件名></组件名> -->
<pannel />
<pannel></pannel>
```



组件局部注册语法

```js
import 组件对象 from 'vue文件路径'
export default {
    components: {
        "组件名": 组件对象
    }
}
```



:::tip  scoped

**注册的组件  pannel.vue 里style标签 必须加上 scoped属性**

:::

简写形式:

> key 和 value 相同 可以简写

```html
App.vue

<template>
  <div id="app">
    <pannel />
    <!-- <pannel></pannel> -->
  </div>
</template>
<script>
import pannel from './components/pannel.vue'
export default {
  components: {
    pannel
  }
}
</script>
```



## 组件通信

### 1_子组件通过props接收数据

```html
<!-- 父组件.vue -->
<template>
    <div>
        <Hello :message='msg' />
    </div>
</template>

<script>
import Hello from './子组件.vue'
export default {
    data() {
        return {
            msg: 'hello',
        };
    },
    components: {
        Hello
    }
}
</script>

```

```html
<!-- 子组件.vue -->
<template>
    <div>
        {{ message }}
    </div>
</template>
<script>
export default {
    props: ['message']
}
</script>
```



### 子传父

```html
<!-- 父组件 -->
<script>
import son from './父组件.vue'
export default {
	data() {
		return {
			message: ''
		}
	},
	components: {
		son

	},
	methods: {
		// value默认值就是传过来的值
		getChildMsg(value) {
			console.log(value);//hello
			this.message = value
		}
	},
}
</script>
<template>
	<div>
		<!-- 那到子组件son的数据,通过自定义事件 -->
		<!-- 2-在父组件中,通过v-on监听子组件自定义的事件 -->
		<son @injectMSG="getChildMsg"></son>
		<h1>{{ message }}</h1>
	</div>
</template>
```



```html
<!-- 子组件.vue -->
<template>
  <div>
    <button @click="sendParent">提交数据给父组件</button>
  </div>
</template>
<script>
export default {
  data() {
    return {
      msg: 'hello',
    };
  },
  methods: {
    sendParent: function () {
      // this.$emit('自定义事件的名称','发送的事件参数')
      this.$emit('injectMSG', this.msg)
    }
  },
}
</script>
```

### emit 的实现

```ts
  Vue.prototype.$emit = function (event: string): Component {
    const vm: Component = this
    if (__DEV__) {
      const lowerCaseEvent = event.toLowerCase()
      if (lowerCaseEvent !== event && vm._events[lowerCaseEvent]) {
        tip(
          `Event "${lowerCaseEvent}" is emitted in component ` +
            `${formatComponentName(
              vm
            )} but the handler is registered for "${event}". ` +
            `Note that HTML attributes are case-insensitive and you cannot use ` +
            `v-on to listen to camelCase events when using in-DOM templates. ` +
            `You should probably use "${hyphenate(
              event
            )}" instead of "${event}".`
        )
      }
    }
    let cbs = vm._events[event]
    if (cbs) {
      cbs = cbs.length > 1 ? toArray(cbs) : cbs
      const args = toArray(arguments, 1)
      const info = `event handler for "${event}"`
      for (let i = 0, l = cbs.length; i < l; i++) {
        invokeWithErrorHandling(cbs[i], vm, args, vm, info)
      }
    }
    return vm
  }
```

emit用来发射组件的自定义事件,当使用该组件时,我们可以监听emit函数发射的自定义事件

在具体实现上,发射自定义事件的本质就是根据事件名称去props数据对象种寻找相对应的事件处理函数并执行

vue2.0:

当执行 `vm.$emit(event)` 的时候，根据事件名 `event` 找到所有的回调函数 `let cbs = vm._events[event]`，然后遍历执行所有的回调函数

所以对于用户自定义的事件添加和删除就是利用了这几个事件中心的 API。需要注意的事一点，`vm.$emit` 是给当前的 `vm` 上派发的实例，之所以我们常用它做父子组件通讯，是因为它的回调函数的定义是在父组件中，对于我们这个例子而言，当子组件的 `button` 被点击了，它通过 `this.$emit('select')` 派发事件，那么子组件的实例就监听到了这个 `select` 事件，并执行它的回调函数——定义在父组件中的 `selectHandler` 方法，这样就相当于完成了一次父子组件的通讯

























## props的基本用法

### 1_props类型

上面看到的是以字符串数组形式列出的 prop：

```
props: ['message']
```

但是，通常你希望每个 prop 都有指定的值类型。这时，你可以以对象形式列出 prop，这些 property 的名称和值分别是 prop 各自的名称和类型：

```js
props: {
  title: String,
  likes: Number,
  isPublished: Boolean,
  commentIds: Array,
  author: Object,
  callback: Function,
  contactsPromise: Promise // 或任何其他构造函数
}
```

### 打印props

```js
export default {
  props: ['foo'],
  created() {
    // props 会暴露到 `this` 上
    console.log(this.foo)
  }
}
```



### 单向数据流

所有的 prop 都遵循着**单向绑定**原则，prop 因父组件的更新而变化，自然地将新的状态向下流往子组件，而不会逆向传递。这避免了子组件意外修改了父组件的状态，不然应用的数据流就会变得难以理解了。

另外，每次父组件更新后，所有的子组件中的 props 都会被更新到最新值，这意味着你**不应该**在子组件中去更改一个 prop。若你这么做了，Vue 会在控制台上向你抛出警告：

```js
export default {
  props: ['foo'],
  created() {
    // ❌ 警告！prop 是只读的！
    this.foo = 'bar'
  }
}
```

### 2_更改对象 / 数组类型的 props

当对象或数组作为 props 被传入时，虽然子组件无法更改 props 绑定，但仍然**可以**更改对象或数组内部的值。这是因为 JavaScript 的对象和数组是按引用传递，而对 Vue 来说，禁止这样的改动虽然可能，但有很大的性能损耗，比较得不偿失。

这种更改的主要缺陷是它允许了子组件以某种不明显的方式影响父组件的状态，可能会使数据流在将来变得更难以理解。在最佳实践中，你应该尽可能避免这样的更改，除非父子组件在设计上本来就需要紧密耦合。在大多数场景下，子组件应该**抛出一个事件**来通知父组件做出改变。

- `props` 是受组件数据影响的
- 如果是普通数据(数字、字符串、布尔值)，绝对不能修改，即使改了也不会传导给父组件
- 如果是引用类型(数组、对象)，可以修改，但是不能够直接赋值



##  $nextTick和$refs

### $refs

ref 和 $refs 可以用于获取 dom 元素

```html
<h1 id="h" ref="hello">hello</h1>
```

```js
console.log(this.$refs.hello); // h1
```



###  $nextTick

作用:

**处理vue中的异步更新**

简单的理解:

**当数据更新时,在dom渲染之后,会自动执行callback函数**

```html
<template>
  <div>
    <p ref="msg_p">{{msg}}</p>
    <button @click="changeMSG">change</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      msg:'hello'
    };
  },
  methods: {
    changeMSG() {
      this.msg = '222'    
      console.log(this.$refs.msg_p.innerHTML);//hello
      //此时真实DOM里面已经变成了222,但是打印出来的依旧是hello
      //那为什么打印的还是之前的值呢?
      //原因:vue执行dom更新是异步的,不是同步的
      //vue监测数据更新。开启一个DOM 更新队列，
    //不会立刻更新DOM，而是等待主线程完成
      //vue将dom的更新缓存在一个事件循环里面
    }
  },
};
</script>

```

Vue中的数据更新是异步的，意味着我们在修改完Data之后并不能立刻获取修改后的DOM元素。

```js
this.$nextTick(function () {
  console.log(this.$refs.msg_p.innerHTML)//222
  //此时就可以获取到真实的dom元素了
  //用箭头函数更好
});
```

:::tip tip

nextTick 只是单纯通过Promise、setTimeout等方法模拟的异步任务。

:::

总结：vue异步更新的原理

1. 修改 Vue 中的 Data 时，就会触发所有和这个 Data 相关的 Watcher 进行更新。
2. 首先，会将所有的 Watcher 加入队列 Queue。
3. 然后，调用 nextTick 方法，执行异步任务。
4. 在异步任务的回调中，对 Queue 中的 Watcher 进行排序，然后执行对应的 DOM 更新。

### 回调函数

:::tip 来自Google的解释

A callback is a function that is passed as an argument to another function and is executed after its parent function has completed.

**回调函数是作为参数传递给另一个函数并在其父函数完成后执行的函数。**

:::

作为JS的核心，回调函数和异步执行是紧密相关的，也是必须跨过去的一道个门槛。

callback也是Node.js三大核心之一。

在JavaScript中，回调函数具体的定义为：**函数A作为参数(函数引用)传递到另一个函数B中**，并且这个**函数B执行函数A**。我们就说函数A叫做回调函数。如果没有名称(函数表达式)，就叫做匿名回调函数。

其实回调函数并不复杂，明白两个重点即可：

1. 函数可以作为一个参数在传递到另一个函数中。

2. JS是异步编程语言。

```js
this.$nextTick(callback)
```



















