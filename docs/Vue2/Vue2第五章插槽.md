---
sidebar_position: 5
---
# Vue2第五章_动态组件和插槽

## 基本使用

![](https://staging-cn.vuejs.org/assets/slots.dbdaf1e8.png)

插槽：就是挖个坑

```html
<!-- 父组件 -->
<template>
  <div>
    <h1>hello</h1>
    <Child>
      <button> 插槽</button>
      <!-- 插槽单标签不能用 -->
    </Child>
  </div>
</template>

<script>
import Child from './子组件.vue'
export default {
  components: {
    Child
  }
};
</script>
```

```html
<!-- 子组件 -->
<template>
  <div>
    <slot></slot>
  </div>
</template>

```



## 具名插槽

顾名思义:就是有名字的插槽

```html
<template>
  <el-card class="page-tools">
    <el-row type="flex" justify="space-between" align="middle">
      <el-col>
          // highlight-next-line
         <!-- showBefore控制 插槽的显示 -->
        <div v-if="showBefore" class="before">
          <i class="el-icon-info" />
		// highlight-start
          <!-- 前插槽--挖了一个坑 -->
          <!-- 有名字的叫具名插槽，没名字叫匿名插槽 -->
          <!-- 具名插槽起个名叫before -->
          <slot name="before" />
            // highlight-end
        </div>
      </el-col>
      <el-col>
        <el-row type="flex" justify="end">
          <!-- 后插槽--挖了一个坑  -->
          <!-- 具名插槽起个名叫before -->
          <slot name="after" />
        </el-row>
      </el-col>
    </el-row>
  </el-card>
</template>
```

```js
  props: {
    showBefore: {
      type: Boolean,
      default: false,
    },
  },
```

使用插槽：

```html
<template>
  <div class="dashboard-container">
    <div class="dashboard-text">name: {{ name }}</div>
    <PageTools :show-before="true">
      <template v-slot:before>
        <span>共166条记录</span>
      </template>
      <template v-slot:after>
        <el-button type="primary">导入excel</el-button>
      </template>
    </PageTools>
  </div>
</template>
```



```html
<!-- 父组件 -->
<template>
  <div>
    <Child>
      <template v-slot:button>
        <button> 插槽-按钮 {{msg}}</button>
      </template>

      <template v-slot:h1>
        <h1> 插槽-h1</h1>
      </template>

      <template v-slot:h2>
        <h2> 插槽-h2</h2>
      </template>
    </Child>
  </div>
</template>

<script>
import Child from './子组件.vue'
export default {
  data() {
    return {
      msg:'hello'
    }
  },
  components: {
    Child
  }
};
</script>
```



```html
<!-- 子组件 -->
<template>
  <div>
    <slot name="button"></slot>
    <slot name="h1"></slot>
    <slot name="h2"></slot>
  </div>
</template>

```

### 渲染作用域



插槽内容可以访问到父组件的数据作用域，**因为插槽内容本身是在父组件模板中定义的**。举个例子：

插槽内容**无法访问**子组件的数据，请牢记一条规则：

> 任何父组件模板中的东西都只被编译到父组件的作用域中；而任何子组件模板中的东西都只被编译到子组件的作用域中。



















