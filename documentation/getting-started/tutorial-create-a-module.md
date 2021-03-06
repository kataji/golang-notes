# Tutorial: Create a module

> [https://golang.org/doc/tutorial/create-module](https://golang.org/doc/tutorial/create-module)

go里面module是用来组织package的，package是用来组织function的。module会有一个类似package.json的文件：go.mod，用来描述module的名字、go版本、依赖列表和依赖的版本。

通过module，go就天然有了模块化的属性。可以写module然后被自己或者其他人引用。

这个tutorial就是教你怎么做一个module。

首先建一个dir，在里面跑`go mod init <modulepath>`来初始化go.mod，modulepath可以是`a/b/c/d`这样的路径，写模块的时候就是存放代码的路径，production环境里是可以下到module的路径（？）。这里就假设是`whatever/path/greetings`吧。

在文件系统里，module给我的感觉是对应了一个目录（？）。

然后可以新建.go文件，在里面写代码声明package，实现function。

```go
package mypackage

import "fmt"

// return a message with the name
func Hello(name string) string {
    message := fmt.Sprintf("hello, %v", name)
    return message 
}
```

试了下文件名和package名无关，以后用的时候只认package名。

go里面大写字母开头的函数可以被外面的代码调用，称为exported Name。

一个含有一个package，which含有一个函数，的module就定义好了。下一节，让我们来康康怎么在别的module里调这个module里的package里的function。

