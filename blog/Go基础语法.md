---
slug: Go基础语法
title: Go基础语法
authors:
  name: Kevin
  title: Go基础语法
  url: https://github.com/timspan
  image_url: https://timspan.gitee.io/creative_website/assets/dog.e73586b8.jpg
tags: [hola, docusaurus]
---
# Go基础语法

## 定义变量

```go
package main

import (
	"fmt"
)

func main() {
	var a int
	var text string
	fmt.Printf("%d %q\n", a, text) //这样就可以打印出空字符串
	// 定义的变量必须使用掉
	fmt.Println(
		a, text, // 空字符串打印不出来
	)
	test()
	varShort()
}

func test() {
	//不固定类型可以写在一行
	var a, b, c, d = 3, 4, true, "def"
	fmt.Println(
		a, b, c, d,
	)
}

func varShort() { //更简洁的定义变量
	a, b, c := 1, 2, 3
	b = 10
	fmt.Println(
		a, b, c,
	)
}

```

