---
sidebar_position: 1
---

# 使用手册

Docusaurus 支持 **[Markdown](https://daringfireball.net/projects/markdown/syntax)** 和一些 **附加功能**.

## Front Matter

Markdown 文档顶部的数据称为 [Front Matter](https://jekyllrb.com/docs/front-matter/):

```text title="my-doc.md"
// highlight-start
---
id: my-doc-id
title: My document title
description: My document description
slug: /my-custom-url
---
// highlight-end

## Markdown heading

Markdown text with [links](./hello.md)
```

## 链接

支持常规 Markdown 链接，使用 url 路径或相对文件路径

```md
Let's see how to [grid 布局](/grid布局.md).
```

```md
Let's see how to [grid 布局](./grid布局.md).
```

**Result:** Let's see how to [grid 布局](./grid布局.md).

## 图像

支持常规 Markdown 图像。

您可以使用绝对路径来引用静态目录 ( static/img/docusaurus.png) 中的图像： (`static/img/docusaurus.png`):

```md
![Docusaurus logo](/img/docusaurus.png)
```

![Docusaurus logo](/img/docusaurus.png)

## 代码块

语法高亮支持 Markdown 代码块。

    ```jsx title="src/components/HelloDocusaurus.js"
    function HelloDocusaurus() {
        return (
            <h1>Hello, Docusaurus!</h1>
        )
    }
    ```

```jsx title="src/components/HelloDocusaurus.js"
function HelloDocusaurus() {
  return <h1>Hello, Docusaurus!</h1>;
}
```

## 警告

Docusaurus 有一种特殊的语法来创建警告和标注：

    :::tip My tip

    Use this awesome feature option

    :::

    :::danger Take care

    This action is dangerous

    :::

:::tip My tip

Use this awesome feature option

:::

:::danger Take care

This action is dangerous

:::


