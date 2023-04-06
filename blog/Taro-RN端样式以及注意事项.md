---
slug: Taro-RN端样式以及注意事项
title: Taro-RN端样式以及注意事项
authors:
  name: Kevin
  title: Taro-RN端样式以及注意事项
  url: https://github.com/timspan
  image_url: https://timspan.gitee.io/creative_website/assets/dog.e73586b8.jpg
tags: [hola, docusaurus]
---

## Taro RN端样式 以及注意事项

**Taro官网文档不够详细**

### 1、行内式高度

height 的 值必须是数值,而不是字符串

```html
<View style={{ height: 50 }}></View>
```

### 2、行内式报错 数字非字符串

String cannot be cast tojava.lang.Double

字符串不能转换为java.lang. double

![image-20230403101443482](/Users/kevin/Library/Application Support/typora-user-images/image-20230403101443482.png)

说明行内式 zIndex 发生错误



错误写法

```js
style={{ zIndex: '9999 '}}
```

正确写法

```js
style={{ zIndex: 9999 }}
```



### 2、事件冒泡

```
e.stopPropagation 不可用
```

使用处理封装过的 **stopPropagation(e)**

```js
import { useBoolean, baseTheme, stopPropagation } from '@/base/utils'
```

使用

```jsx
<View {...props} onClick={(e) => { stopPropagation(e); showAction.setTrue() }} />
stopPropagation(e); 
```



### 3、图片报错

![image-20230401173740732](/Users/kevin/Library/Application Support/typora-user-images/image-20230401173740732.png)

The  component cannot contain childrenlf you want to render content on top of the
image, consider using the 
component or absolute positioning

< image >组件不能包含子组件，如果你想在上面呈现内容
图像，考虑使用 

```
<lmageBackground> 
```

 组件或绝对定位     

```
soudianxia_gl/common/select_content_1
soudianxia_gl/shop/people


```



### 4、umberOfLines  报错

**Text**   **props**    **关键字** **numberOfLines** 会导致报错

```jsx
<Text  numberOfLines className='searchShop__item__card__title'>
                  512m² | {item.title}
                </Text>
```



### 5、样式支持度

**! important**  不支持

### 6、ScrollView 行内式

还是那个问题， height 只能是数字不能是字符串  这样写高度无效

```
	{/* style={{ height: '100%' }} */}
						<ScrollView  >
```

### 7、ModalFormItem 组件

高度有问题

### 8、Form

```
import { Form } from '@tarojs/components'  报错
```

### 9、组件要有名字，不然会重定向到首页



### 10、关于文字显示

很多时候文字必须 放在 Text 标签里面

```jsx
            {/* start_service */}
            <Picker mode='date' value={currentDate} start='2020-01-01' end={currentDate} onChange={onDateChange}>
              <View className='shangquan__box__item__top'>
                <View className='shangquan__box__item__top__left'>开始服务日期</View>
                <View className='shangquan__box__item__top__right' >
                  <Text className='shangquan__box__item__top__right__text'>{time || '请选择'}</Text>
                  <Icon name='you3' />
                </View>
              </View>
              <View className='shangquan__box__item__bottom'></View>
            </Picker>
```

### 11、Textarea

Textarea 得从 Taro 导入

封装的Textarea 在App 端会有高度显示不出来的问题
