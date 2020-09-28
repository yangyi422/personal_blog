# 1.golang的下载

>由于国内的特殊环境，访问[golang](https://golang.org/)的官网会出现些许问题，所以推荐去[Golang的国内网站](https://golang.google.cn/)或者[golang中文网](https://studygolang.com/)下载golang的安装包，包括后面使用golang的一些官方包也需要走代理去获取。

下载golang安装包可以选择在[golang国内网站下载](https://studygolang.com/dl)或者是[golang中文网下载](https://studygolang.com/dl)

# 2.不同的系统安装

> 本人没用过mac，所以就不添加mac的安装了，以后有机会再添加

## 2.1window系统安装

### 2.1.1自动安装（推荐）

> 推荐使用此方法

下载后缀名msi的安装文件,用此方法安装后，会安装至c:/go，并且将该路径自动加入环境变量path中。

### 2.1.2手动安装（不推荐）

下载后缀名zip文件，需要自己配置相关环境变量，打开系统环境变量配置，新建系统变量

​	变量名：GOROOT	变量值：go安装/解压的路径（如：C:\go）

![](./images/golang/image1.PNG)

​	变量名：GOPATH	 变量值：存放go项目的路径（如：D:\WorkShop\GoSpace）

![](./images/golang/image2.PNG)

​	然后在系统变量中找到变量名为path的变量，点击编辑，然后点击新建，然后复制这个路径C:\Go\bin;%GOPATH%\bin;

![](./images/golang/image3.PNG)

配置完成后检查go版本

​		在终端输入

```bash
go version
```

​		如果如下显示，就说明安装成功

```bash
go version go1.15.1 windows/amd64
```

## 2.2linux下安装

### 2.2.1自动安装

> 自动安装存在一个问题，可能下载的版本不是最新的版本，所以不推荐这种方式安装。

可以使用以下语句自动安装golang

```bash
sudo apt install golang-go
```

### 2.2.2手动安装

​	1.首先我们卸载旧版本的golang，如果存在两个版本，在编译的时候报错，所以需要先卸载旧版本的golang，使用下述代码卸载：

```bash
apt remove golang-go
```

​	2.下载最新版本的golang(此处使用的是go语言中文网的下载路径)，使用下述代码下载：

```bash
wget https://studygolang.com/dl/golang/go1.15.2.linux-amd64.tar.gz
```

​	3.解压下载好的文件(此处解压到 /usr/local 路径，因为此路径是默认安装路径，建议解压到此处)，用下述代码解压：

```bash
tar -zxvf golang/go1.15.2.linux-amd64.tar.gz -C /usr/local
```

​	4.环境变量设置

​		首先在/etc/profile文件中写入环境变量，在文件最后方空白处加入条目（使用vim /etc/profile进行文件编辑）

> vim进入文件后按 i 进入编辑模式，就可以输入文本，文本输入完成后，按下esc键退出编辑模式，进入命令模式，使用 :wq 退出文件编辑（:q是退出不保存，:wq! 是强制退出保存，:q! 是强制退出，更加详细的vim教程请参考[此处](https://github.com/wsdjeg/vim-galore-zh_cn)）。

```bash
export GOPATH=/home/chen/gowork
export GOROOT=/usr/local/go
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
```

​		然后~/.bashrc文件最后方空白处增添一条（使用vim /etc/profile进行文件编辑，操作方式见上一条备注）

```bash
source /etc/priofile
```

​		最后在终端中输入 source /etc/profile 或重启终端后环境变量会开始生效。

​	5.检查go版本

​		在终端输入

```bash
go version
```

​		如果如下显示，就说明安装成功

```bash
go version go1.15.1 linux/amd64
```

