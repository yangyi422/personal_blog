# golang命令行

> 此文档主要是用来介绍golang自带的相关命令行，例如比较常用的go version,go build,go run等等。

## GO命令
配置好环境后可以在控制台输入`go`命令，可以看到官方给的go命令的相关提示，如下图
![](./images/golang/go命令.png)

## go build
这个命令主要作用是用来测试编译，在编译过程中，同时也会编译与之关联的包。

| 包内main函数是否存在 | 结果                   |
| -------------------- | ---------------------- |
| 存在（main包）       | 当前目录生成对应的文件（windows下是`目录名.exe`,linux下是`目录名`） |
| 不存在（普通包）     | 不会生成文件 |

注:`go build`默认编译当前目录下所有的go文件（但不会编译以_和.开头的go文件），如果只编译单个文件，可以在go build后加上文件名。

## go run

编译项目后并运行项目

## go get

这个命令是用来动态获取远程代码包的，目前支持的有BitBucket、GitHub、Google Code和Launchpad。

这个命令在内部实际上分成了两步操作：第一步是下载源码包，第二步是执行go install。

## go install

这个命令在内部实际上分成了两步操作：第一步是生成结果文件(可执行文件或者.a包)，第二步会把编译好的结果移到$GOPATH/pkg或者$GOPATH/bin。

## go version

用于查看使用的go的版本

## go env 

用于查看go的环境配置，可以看到自己配置的go root，go path，gomod相关配置内容

## go clean

这个命令是用来移除当前源码包里面编译生成的文件。这些文件包括：

```bash
_obj/            旧的object目录，由Makefiles遗留
_test/           旧的test目录，由Makefiles遗留
_testmain.go     旧的gotest文件，由Makefiles遗留
test.out         旧的test记录，由Makefiles遗留
build.out        旧的test记录，由Makefiles遗留
*.[568ao]        object文件，由Makefiles遗留
DIR(.exe)        由go build产生
DIR.test(.exe)   由go test -c产生
MAINFILE(.exe)   由go build MAINFILE.go产生
```

注：一般都是利用这个命令清除编译文件，然后github递交源码，在本机测试的时候这些编译文件都是和系统相关的，但是对于源码管理来说没必要。

## go fmt

这个命令的作用就是格式化go代码，但是在实际开发中基本不用，我们会使用编译自带的代码格式整工具来整理代码格式，但实际上，这些工具本身大多数底层调用的依旧是这个命令

## go test

执行这个命令，会自动读取源码目录下面名为*_test.go的文件，生成并运行测试用的可执行文件。

## go doc

如何查看相应package的文档呢？ 例如builtin包，那么执行go doc builtin 如果是http包，那么执行go doc net/http 查看某一个包里面的函数，那么执行godoc fmt Printf 也可以查看相应的代码，执行godoc -src fmt Printf
 　通过命令在命令行执行 godoc -http=:端口号 比如godoc -http=:8080。然后在浏览器中打开127.0.0.1:8080，你将会看到一个golang.org的本地copy版本，通过它你可以查询pkg文档等其它内容。如果你设置了GOPATH，在pkg分类下，不但会列出标准包的文档，还会列出你本地GOPATH中所有项目的相关文档，这对于经常被墙的用户来说是一个不错的选择。

## go list

列出当前安装的package

## go fix

用来修复以前的老版本的代码到新代码



