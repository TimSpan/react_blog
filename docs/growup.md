# 笔记

文字不可复制

```css
<style scoped type="text/css">
* {
    -webkit-user-select: none;
    user-select: none;
}

p {
    font-family: 'Microsoft Yahei';
    font-size: 28px;
}

input {
    width: 80%;
    padding: 10px 20px;
}
```

```
 		oncut="return false" 
        onpaste="return false" 
        oncopy="return false"
```

## append-to-body

```
当两个元素都有 append-to-body 时，设置优先显示哪个元素，需要都给两个元素设置 z-index


```

饿了么表格

```js
scope.$index 可以传递下标
```

## element-plus里的el-table获取表格数据索引下标



```html
<template>
    <div style="height: 100%;position: relative;">
        <div style="display: flex;">
            <myTitle :title="title" />
            <span class="addRoleButton" @click="routerPush">添加角色</span>
        </div>
        <div style="width: 1000;">
            <el-table :data="tableData.list" stripe style="width: 100%">
                <el-table-column prop="role_name" label="角色名称" min-width="20%" />
                <el-table-column prop="dept_name" label="类型" min-width="20%" />
                <el-table-column prop="number" label="人员数量" min-width="20%" />
                <el-table-column fixed="right" label="操作" min-width="40%" type="index">
                    <template #default="scope">
                        <el-button link type="primary" size="small" @click="handleClick">编辑</el-button>
                        <el-button link type="primary" size="small">折扣</el-button>
                        <el-button link type="primary" size="small" @click="openDetails(tableData.list[scope.$index].id)">详情</el-button>
                        <el-button link type="danger" size="small">删除</el-button>
                    </template>
                </el-table-column>
            </el-table>
        </div>
        <viewDetails :visibleState="visible" @close="close" />
        <el-pagination background layout="prev, pager, next" :total="total" style="position: absolute; bottom: 50px;" />
    </div>
</template>
```

## vue-router4编程式导航使用注意

跳转

```js
    router.push({
        path: '/discountSettings',
        query: { id: id },
    })
```

接收参数

```js
const route = useRoute()
console.log(route.query.id)
```

> 如果提供了 `path`，`params` 会被忽略
>
> `params` 不能与 `path` 一起使用



## vue3 watch使用

```js
watch(
    () => discountData.agent,
    (newValue, oldValue) => {
        console.log(newValue, oldValue)
    },
    { deep: true, immediate: true }
)
```

```js
watch(
    () => discountData.agent,
    (newValue, oldValue) => {
        console.log('代理费新值', newValue)
        newData.agent = newValue
    },
    { deep: true, immediate: true }
)
watch(
    () => discountData.hard_ware,
    (newValue, oldValue) => {
        console.log('硬件新值', newValue)
        newData.hard_ware = newValue
    },
    { deep: true, immediate: true }
)
watch(
    () => discountData.soft_ware,
    (newValue, oldValue) => {
        console.log('软件新值', newValue)
        newData.soft_ware = newValue
    },
    { deep: true, immediate: true }
)
// watch(
//     () => [discountData.agent, discountData.hard_ware, discountData.soft_ware],
//     ([agent_new, agent_old], [hardware_new, hardware_old], [software_new, software_old]) => {
//         console.log('代理费新值', agent_new)
//         console.log('硬件新值', hardware_new)
//         console.log('软件新值', software_new)
//     },
//     { deep: true, immediate: true }
// )
```

## git回退上一个版本

```bash
git reset --hard HEAD^
```

## git回退到指定版本

```bash
 git reset --hard 指定版本号
```

## echarts 和 u-charts

```
orient : 确定方位
horizontal : 水平的
circle : 圆形
```

```
:eopts="{
                        legend: {
                            orient: 'vertical',
                            top: 'center',
                            right: 0,
                            icon: 'circle',
                        },
                        tooltip: {
                            show: true,
                        },
                    }"
```

```
:opts="{
                        legend: {
                            show: false,
                        },
                        extra: {
                            tooltip: {
                                showBox: false,
                            },
                            markline: {
                                type: solid,
                            },
                        },
                    }"
```



```js
option = {
  formatter: function (name) {
    return name + '30%';
  },
  title:{
    text:'卡类型占比'
  },
  tooltip: {
    trigger: 'item',
    formatter:'{b}:{c}%'
  },
  series: [
    {
      name: ['金卡占比','银卡占比','铜卡占比','黑卡占比'],
      type: 'pie',
      radius: ['30%', '40%'],
      avoidLabelOverlap: false,
      label: {
        normal:{
          show:true
        },
        show: true,
        position: 'center'
      },
    labelLine: {
          normal: {
            show: true
        }
    },
      data: [
        { value: 30, name: '金卡占比' },
        { value: 30, name: '银卡占比' },
        { value: 20, name: '铜卡占比' },
        { value: 20, name: '黑卡占比' }
      ]
    }
  ]
};
```

```
:chartData="iconList"
:tooltipShow="false"
```



## vue3------watch监听多个数据

```js
    const state = reactive({
      province: '',// 省份
      country: '', // 城市
      detailedAdress: '', // 详细地址
      countries: [], // 城市列表
      allCity: [], // 所有省份及城市数据
    });
    // 写两个watch太麻烦，现用watch监听省份和城市两个数据
    // 第一个参数() => [state.province, state.country] 监听的两个数据
    // 第二个参数回调函数，其中参数分别代表更改后与更改前的值，([newprovince,newcountry],[oldprovince,oldcountry]) ，第一个参数依次代表更改后的值，第二个参数依次代表更改前的值
      watch(() => [state.province, state.country], ([newprovince,newcountry],[oldprovince,oldcountry]) => {
        console.log(oldprovince,'省份---', newprovince);
        console.log(newcountry,'cs---', oldcountry);
        // 判断是不是省份发生的变化
        if(oldprovince !== newprovince) {
        const arr = state.allCity.filter((item) => item.province == state.province);
        state.countries = arr[0].cities;
        console.log(arr);
        state.country = "";
        }
        state.detailedAdress = "";
        console.log(state.countries);
      }
    ); 


```





## 快速清除对象属性的键值

```js
const ruleForm = reactive({
    sort: '', //序号
    name: '', // 名称
    cost_price: '', // 成本价
    seller_price: '', // 销售价
    stock_num: '', //库存数量
    type: 2, //这是硬件
})
function add_hardware() {
    Object.keys(ruleForm).forEach(key => (ruleForm[key] = '')) //快速清除对象属性的键值
    
}
```




## 饿了么表单自定义校验

> 自定义验证表单时，切记不管什么情况都要执行callback函数！！！

```js
const validateRegion = (rule, value, callback) => {
    console.log(value)
    if (value === '') {
        callback(new Error('请选择角色'))
    } else {
        // 自定义验证表单时，切记不管什么情况都要执行callback函数！！！
        callback()
    }
}
const validateRemark = (rule, value, callback) => {
    if (ruleForm.remark.length >= 100) {
        callback(new Error('备注长度不能超过100'))
    } else {
        // 自定义验证表单时，切记不管什么情况都要执行callback函数！！！
        callback()
    }
}
```

## 饿了么动态表单

数据格式

> 注意点：
>
> 需要注意给prop绑定时的名称要保持一致（一级属性+索引+二级属性名称 **:prop="'soft_ware.' + index + '.price'"**）

```html
<el-form-item
    label-width="250px"
    v-for="(item, index) in ruleForm.soft_ware"
    :key="index"
    :label="item.ware_name + '原价:' + item.discount_price + '元'"
    :prop="'soft_ware.' + index + '.price'"
    :rules="RMB_Rules"
>
    折后
    <el-input class="input_witdh" v-model="item.price" />
    元
</el-form-item>
```

```js
const RMB_Rules = [{ required: true, trigger: ['change', 'blur'], validator: validate_three, message: '元输入框不能超过7位数' }]

```









