# goland的相关配置

> 没有使用vscode的原因是，vscode偶尔会出现工具包版本需求的问题，以及我使用的时候出现gomod提示报错，不知道是什么原因，还是建议使用goland进行开发。此外，采用的是破解版的goland，但还是建议有能力的支持正版软件。

## 1.goland下载

> 这里放的是自己的百度云链接，里面包含jetbrains的全家桶和一个破解的jar包，版本为2020.1版本，破解方式是安装好软件后，将jar包拖入软件界面，然后按照提示进行操作。

​		链接：https://pan.baidu.com/s/1QkNSqLgLYYgiJhmCXuuo5w

​		提取码：lz3n

## 2.goland基本设置

> 打开goland新建一个项目，然后在最上面可以看到file选项卡，点击后的下拉框中可以看到seting，点击就可以打开设置功能，常用设置如下：	

### 2.1.GO

> 这个选项主要用来设置go的版本，所处的gopath路径，以及项目的gomod的开启和代理设置

### 2.2.keymap

> 这个选项主要用来设置快捷键

### 2.3.Editor

> HighlightBracketPair这个选项主要用来设置编辑页面，例如，字体，字号，主题等等都是这个地方设置

### 2.4.plugins

> 这个选项主要是搜索插件和安装插件的地方，下列是部分插件推荐（个人比较常用），后续会添加。如果在goland的plugins加载不出插件市场，可以去[官方插件网页](https://plugins.jetbrains.com/go)下载对应的插件。

#### 2.4.1 HighlightBracketPair

​	让你光标所处的括号对高亮，便于开发时清晰的看到代码块

#### 2.4.2 Rainbow Brackets

​	让各种括号对的颜色不一样，便于开发时清晰的看到代码块（和上面的一起使用，效果很nice）

#### 2.4.3 Material Theme UI

​	一套主题插件，也是目前使用最多的插件，安装完成后在setting->Appearance&Behavior->Appearance中选择Theme中选择自己喜欢的主题

#### 2.4.4 Key Promoter X

​	快捷键提示，当你用鼠标进行某项操作时，此插件会在屏幕的右下角弹出提示，告诉你这个鼠标操作可以通过对应的快捷键完成，久而久之，开发时就会习惯的使用快捷键，避免频繁的右手离开键盘，降低开发效率。

#### 2.4.5 CodeGlance

​	安装后重启idea会在代码编辑页面右侧出现一个迷你代码块，可以快速实现代码编辑页面的跳转。

### 2.5.Tools

> 这个选项主要用于设置go官方提供的一些工具，例如自动整理代码，自动设置导入包的格式，自动检测代码合理性等等

​	选择Tools下列的File Watchers的，然后选择右边的加号就可以看到`go fmt`（代码格式整理），`goimports`（导入包格式设置），`golangci-lint`（静态代码质量检测工具）这三个工具，通过goland添加就可以自动获取使用的，其中`goimports`如果安装失败的话，可以使用下列步骤安装

#### 2.5.1 goimports手动安装

​	1.手动安装方式如下

```bash
# 创建文件夹  
mkdir $GOPATH/src/golang.org/x/ 
# 进入文件夹 
cd  $GOPATH/src/golang.org/x/
# 下载源码 
git clone https://github.com/golang/tools.git
# 安装
go install golang.org/x/tools/cmd/goimports		
```

​	2.安装完成后，进入Tools下列的File Watchers点击加号，添加`goimports`，然后选择gopath目录下的bin文件里的`goimports.exe`（windows版本）或者`goimports`（Linux版本）文件		

#### 2.5.2 golint手动安装

​	1.手动安装方式如下

```bash
# 创建文件夹
mkdir -p $GOPATH/src/golang.org/x/
# 进入文件夹 
cd $GOPATH/src/golang.org/x/
# 下载源码
git clone https://github.com/golang/lint.git
git clone https://github.com/golang/tools.git
# 进入文件夹
cd $GOPATH/src/golang.org/x/lint/golint
# 安装
go install
```

​	2.安装完成后，进入Tools下列的File Watchers点击加号，添加`go fmt`，然后将修改`Name`为`golint`, `Program`修改为`golint`, `Arguments`修改为`-set_exit_status $FilePath$`，

​	3.平时在写代码的时候随手保存就可以触发这些工具了。

​	4.另外如果觉得这些工具比较好用的话，可以在File Watchers添加完成后的工具列表内将工具的`level`由`Project`换为`Global`，这样每次新建项目就不用再次设置了。

## 3.gomod的使用

> 用于解决Go项目的包管理及依赖，更加详细的信息，请参考[官方文档](https://github.com/golang/go/wiki/Modules)：https://github.com/golang/go/wiki/Modules，下列的操作皆是针对在goland中使用gomod，如果是在vscode中使用，请自行百度，因为本人自己也没弄清楚。

### 3.1 关于gomod

> `go.mod`是Go项目的依赖描述文件，该文件主要用来描述两个事情

	1. 当前项目名（`module`）是什么？每个项目都应该有一个名字，这样此项目中的包（`package`）可以使用该名称相互调用
 	2. 当前项目所依赖的第三方包的名称。项目在运行的时候会自动分析项目中的代码，生成一份go.sum文件（依赖分析结果），然后go的编译器回去下载这些第三方包，然后再编译运行。

### 3.2 gomod使用

1. 在控制台输入以下命令来开启gomod以及设置gomod的代理

```bash
#windows
# 开启gomod
set GO111MODULE=on;
# 设置gomod代理
set GOPROXY=https://goproxy.cn

#linux
# 开启gomod
export GO111MODULE=on;
# 设置gomod代理
export GOPROXY=https://goproxy.cn
```

2. 生成gomod初始文件，可以自己手动创建一个go.mod文件（也可以在控制台使用go mod init 项目名 来生成此文件），然后再朝里面添加如下内容

```bash
module my-hello
```

3. 进入setting->GO->Go Modules中，勾选上`Enable Go Modules integration`选项，在Environment中添加`GOPROXY=https://goproxy.io,direct`，然后点击apply。（每个项目使用gomod都需要设置这一步，目前没发现全局使用的方法）

4. 使用`go get 第三方包的地址` 获取第三方包，然后在使用第三方包的文件内import对应的第三方包，go.mod文件中会自动添加对应的文件，也可以直接在使用第三方包的文件内import对应的第三方包，然后使用`go get .`获取第三方包，然后就可以使用第三方包了。