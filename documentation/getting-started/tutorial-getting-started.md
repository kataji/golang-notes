# Tutorial: Getting started

Hello World Example

go里有module，package，function的概念。其中package是一种组织function的方式，package属于module。

go有一个和npm registry类似的东西，[https://pkg.go.dev/](https://pkg.go.dev/)

也有一种类似于package.json的东西：go.mod，用来列出本地没有的module。如果没这个文件，跑go的时候它会去本地$GOROOT和$GOPATH里找，没找到就报错。要创建这个文件，就

```bash
go mod init <modulepath>
```

创建完基本是空的，就一个名字和go版本。

```text
module modulepath

go 1.15
```

不过没关系，只要有这个文件，go就知道找不着的文件都去外面下载。

这个hello world例子是这样的：

```go
package main

import "fmt"

import "rsc.io/quote"

func main() {
    fmt.Println(quote.Go())
}
```

会打印一句小机灵语言。

其中package main声明了这个叫main的package，然后引入了两个package，一个是标准库，另一个是registry里找的。然后定义了一个叫main的函数打印了quote.Go\(\)的结果。入口函数叫main这个和C一样。quote.Go\(\)这个函数可以去registry上看文档。感觉go.dev比npm registry先进一点，上面文档还是蛮全的。

然后运行

```bash
go run filename.go
```

啊，跑的时候发现rsc.io/quote下不下来，是因为那个吧，众所周知的great f\*\*\* wall的原因。已经有好心的前辈搭了镜像，只要设下proxy就行了：

```bash
go env -w GOPROXY=
https://goproxy.cn,https://proxy.golang.org,direct
```

这玩意儿是个逗号分隔列表，后面俩是原来的值，我在前面加了个中国的镜像。它好像是依次尝试，不行就fallback的设定。

然后就：

```text
go: finding module for package rsc.io/quote
go: downloading rsc.io/quote v1.5.2
go: found rsc.io/quote in rsc.io/quote v1.5.2
go: downloading rsc.io/sampler v1.3.0
go: downloading golang.org/x/text v0.0.0-20170915032832-14c0d48ead0c
Don't communicate by sharing memory, share memory by communicating.
```

再摸摸就会发现go.mod文件最后多了一行：

```text
require rsc.io/quote v1.5.2 // indirect
```

把依赖的package和版本记下来了，就像package.json一样。不过发现没有，它不用手工install的耶，它看到import然后发现没有就自己去download了，绝赞。

然后包包好像down到$GOPATH/pkg/mod/rsc.io/quote@vd.d.d里了。

$GOPATH下面一共三个dir：bin，pkg，src。bin里都是.exe文件，pkg应该就是上面这样的包，src是.go源文件？

好的，今天的表演到此结束。

