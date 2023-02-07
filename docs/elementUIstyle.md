# elementUI穿透样式

- 引入第三方组件后，如果需要局部修改第三方组件的样式，而又不想去除`scoped`属性造成组件之间的样式污染，这时候就可以用`>>>`穿透`scoped`了
- 如果vue的style使用的是css，那么则：

```css
<style scoped lang="css">
.menuItem {
	>>> .ant-input {
      border-radius: 50px;
      font-size: 14px;
      height: 30px;
    }
}
</style>

```

## /deep/

但是像`scss`等预处理器却无法解析`>>>`，这时候我们可以使用下面的方式

```css
<style scoped lang="scss">
.menuItem {
	/deep/ .ant-input {
      border-radius: 50px;
      font-size: 14px;
      height: 30px;
    }
}
</style>

```

## ::v-deep

但是有些开发者反应，在vue-cli3编译时，deep的方式会报错或者警告,这时候我们可以使用下面的方式.

```css
<style scoped lang="scss">
.menuItem {
	::v-deep .ant-input {
      border-radius: 50px;
      font-size: 14px;
      height: 30px;
    }
}
</style>

```

```css
::v-deep .el-input__inner{
  border: 0;
  // border: 1px solid red;
}
```

## :deep()

> vue3用:deep()

如果你使用的是`css`，没有使用css预处理器，则可以使用`>>>`，`/deep/`，`::v-deep`。

如果你使用的是`less`或者`node-sass`，那么可以使用`/deep/`，`::v-deep`都可以生效。

如果你使用的是`dart-sass`，那么就不能使用`/deep/`，而是使用`::v-deep`才会生效。

但是如果你是使用`vue2.7`以上版本以及包括`vue3`，`::v-deep`也会生效，但是会有警告⚠️

总结一下：

- `css`可以使用`>>>`，`/deep/`，`::v-deep`
- `less`和`node-sass`可以使用`/deep/`，`::v-deep`
- `dart-sass`可以使用`::v-deep`
- `vue2.7`以上版本以及包括`vue3`，应该使用`:deep()`

```css
:deep(.is-leaf) {
    font-size: 16px;
    color: #000000;
    font-weight: bold;
}
```



