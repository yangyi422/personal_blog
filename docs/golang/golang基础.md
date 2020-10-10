# GO基础



> 此文档会涉及以下内容：项目创建，变量，类型，常量，函数，条件语句，循环语句，switch语句

## 1. 项目创建

创建hello world项目，这里只说明如何通过`goland`去创建一个项目，在`goland`的左上角点击`file`，然后选择New ->project，然后选择创建的目录和选择go的版本，最后点击create。

创建项目的目录取决于项目是否使用了go mod。

| 是否使用go mod | 创建项目的目录                                               |
| -------------- | ------------------------------------------------------------ |
| 使用了go mod   | 哪里都可以作为你的项目目录                                   |
| 没有使用go mod | 请在你的go path目录下创建`bin`,`pkg`,`src`三个目录，并将在`src`目录中创建你的项目 |


在创建的项目目录中，创建`hello_world.go`文件，并写入下列代码

```go
// 每一个go文件都应该有包文件声明，用于代码的封装和重用
package main

// 引入需要用到的包，此处引用的是打印到控制台需要的fmt包
import "fmt"

// main函数作为整个程序的一个入口，是很特殊的一个函数，它必须放在main包中，大括号表示函数的开始和结束
func main(){
    // fmt包的println函数将'hello world'写入标准输出，也就是打印在控制台
    fmt.println("hello world!")
}

```

## 2. 变量

> 变量指定了某存储单元（Memory Location）的名称，该存储单元会存储特定类型的值。可以理解为变量名就是房间号，房间就是储存的特定的值，变量可以更为方便找到所储存的特定值。

### 2.1 变量声明

> Go 是强类型（Strongly Typed）语言，因此不允许某一类型的变量赋值为其他类型的值。比较常用简短声明

```go
package main

import "fmt"

func main(){
    var age int // 变量声明
    age = 29 // 赋值
    
    var age int = 29 // 声明变量并初始化
    
    var age = 29 // 声明变量并初始化，可以推断类型
    
    var width, height int = 100, 50 // 声明并赋值多个变量
    
    // 声明多个不同类型的变量并赋值
    var (
        name   = "naveen"
        age    = 29
        height int
    )
    
    name, age := "naveen", 29 // 简短声明，简短声明要求 := 操作符左边的所有变量都有初始值,至少有一个变量是尚未声明的(不能重复声明)
}
```

## 3.类型

> `golang`的类型大致上可以分为3类，分别是布尔型，数字型，字符串型

### 3.1布尔型

> `bool` 类型表示一个布尔值，值为 true 或者 false。

和其他编程语言一样，布尔类型是个很简单的类型，赋值方式如下

```go
package main

import "fmt"

func main(){
    var a bool = true
    b := false
   	var c bool
    c = a && b
    
    fmt.Println("a:",a,"b:",b,"c:",c)
}
```

### 3.2整数类型

> `golang`整数类型大致可以分为有符号整型，无符号整型，浮点型，复数类型，其他数字类型

#### 3.2.1有符号整型(带有负值的整数)

`int8`：表示 8 位有符号整型
**大小**：8 位
**范围**：-128～127

`int16`：表示 16 位有符号整型
**大小**：16 位
**范围**：-32768～32767

`int32`：表示 32 位有符号整型
**大小**：32 位
**范围**：-2147483648～2147483647

`int64`：表示 64 位有符号整型
**大小**：64 位
**范围**：-9223372036854775808～9223372036854775807

`int`：根据不同的底层平台，表示 32 或 64 位整型。通常应该使用 *int* 表示整型，除非对整型的大小有特定的需求。
**大小**：在 32 位系统下是 32 位，而在 64 位系统下是 64 位。
**范围**：在 32 位系统下是 -2147483648～2147483647，而在 64 位系统是 -9223372036854775808～9223372036854775807。

#### 3.2.2有符号整型(不带有负值的整数)

`uint8`：表示 8 位无符号整型
**大小**：8 位
**范围**：0～255

`uint16`：表示 16 位无符号整型
**大小**：16 位
**范围**：0～65535

`uint32`：表示 32 位无符号整型
**大小**：32 位
**范围**：0～4294967295

`uint64`：表示 64 位无符号整型
**大小**：64 位
**范围**：0～18446744073709551615

`uint`：根据不同的底层平台，表示 32 或 64 位无符号整型。
**大小**：在 32 位系统下是 32 位，而在 64 位系统下是 64 位。
**范围**：在 32 位系统下是 0～4294967295，而在 64 位系统是 0～18446744073709551615。

#### 3.2.3浮点类型

`float32`：32 位浮点数

`float64`：64 位浮点数

#### 3.2.4复数类型

`complex64`：实部和虚部都是 `float32` 类型的的复数。

`complex128`：实部和虚部都是 `float64` 类型的的复数。

#### 3.2.5其他数字类型

> `byte`和`rune`常用于字符串中

`byte` 是 `uint8` 的别名。

`rune` 是 `int32` 的别名。

### 3.3字符串类型

> Go 语言中的字符串是一个字节切片。把内容放在双引号""之间，就可以创建一个字符串。

#### 3.3.1字符串按照字节输出

按`byte`类型输出（单字节的字符组成的字符串）

```go
package main

import (
    "fmt"
)

func main() {
    name := "Hello World"
    // 可以通过循环获取字符串中的每一个字节，len(name)获取字符串中字节的数量
    // %x 格式限定符用于指定 16 进制编码，打印出来的结果是"Hello World"以Unicode UTF-8的结果
    for i:= 0; i < len(name); i++ {
        fmt.Printf("%x ", name[i])
    }
    fmt.Println(name)
}
```

按`rune`类型输出（多字节的字符组成的字符串）

以上的操作只适用于字符串中都是单字节的字节才能使用，如果字符串中有中文或者其他的占多个字节的时候，就需要用到rune类型，rune代表一个代码点，不论占用多少个字节，都可以用一个rune表示

```go
package main

import (
    "fmt"
)

func main() {
    name := "你好，世界"
    // 转换成rune类型
    runes := []rune(name)
    // 可以通过循环获取字符串中的每一个字节，len(name)获取字符串中字节的数量
    // %x 格式限定符用于指定 16 进制编码，打印出来的结果是"Hello World"以Unicode UTF-8的结果
    for i:= 0; i < len(runes); i++ {
        fmt.Printf("%x ", runes[i])
    }
    fmt.Println(name)
}
```

用上述方式就可以正常输出非多字节的字符组成的字符串了。

## 4.常量

> "常量"用于表示固定的值，使用`const`关键字表示常量，赋值后不允许重新赋值，常量的值是在编译的时候就已经确定了的

```go
package main

func main() {  
    const a = 55 // 允许
    a = 89       // 不允许重新赋值
}
```

注：常量可以赋值给 “合适的” 类型，而不需要类型转换。

```go
package main

func main() {  
   const a = 0
   var b = 0

   var f1 float64 = a
   var f2 float64 = b	//编译出错

   fmt.Println(f1, f2)
}

```

## 5.函数

> 函数就是一段用于执行目标任务的代码块，在有输入变量的情况下，通过执行一系列算法，输出预期的结果。当然，函数的输入值和输出值并不是必须的，所以一个函数可以不包含输入值或者输出值，也可以两者都不包括。

示例函数，输入两个int类型的数，返回两者的和与差，其中差的返回值用空白符代替

```go
package main

import "fmt"

func main() {
	var (
		a = 1 
		b = 2
	)
	res1, _ := calculate(a, b) // 使用 _ 代替第二个返回值，可以忽略这个返回值
	fmt.Println(res1)
}

//calculate 计算加减，在返回值的括号可以直接声明变量
func calculate(a, b int) (result1, result2 int) {
	result1 = a + b // 相加
	result2 = a - b // 相减
	return
}
```

## 6.包

> 包用于提高go代码的可重用性和可读性，可重用性就是在代码的不同地方都需要使用一段代码，这样我们可以将这段代码封装成一个包，直接调用这个包就可以了，可读性是在代码量过大的时候需要将代码进行拆分，然后让代码更容易看懂，更有条理。

### 6.1包的简单介绍

下面代码中，第一行是的`package main`，是说明这段代码所处的包的哪个，`import "fmt"`是表示引入的包名称，如果引入的第三方包或者是自己写的包，则需要在包名前面加上对应的路径。


```go
package main

import "fmt"

func main() {
	fmt.Println("hello world!")
}
```

### 6.2自定义包并导入

自定义包的方法就是在一个文件目录下创建相应的go文件，然后所创建的go文件就隶属于这个包，包名就是这个文件目录的名字，例如下列代码，创建的就是一个calculate包，包里有一个Add方法（go中包和包之间的方法调用，需要将方法名首字母大写，表示全局方法，此外，包名应该采用单个单词的小写，简洁明了），在main文件中，import了多个包，第一个就是自己创建的`calculate`包，然后用包名点出对应的方法，还可以点出包里常量。

```go
package calculate

//Add 计算加，在返回值的括号可以直接声明变量
func Add(a, b int) (result1 int) {
	result1 = a + b // 相加
	return
}
```

```go
package main

import (
	"blogTest/calculate" // 导入自定义包
	"fmt"	// go的官方包
)

func main() {
	var (
		a = 1
		b = 2
	)
	res := calculate.Add(a, b) // 用包名点出方法
	fmt.Println(res)
}
```

### 6.3`init`函数

>每个包中都可以包含一个`init`函数，这个函数没有任何的接收参数和返回参数，也不能被调用，`init`函数的主要作用是执行一些程序运行时就需要的执行的初始化操作。包初始化的顺序是先初始化包级别的变量，也就是在方法外定义的变量，然后再执行`init`函数，此外一个包如果导入另一个包，那么先初始化的是被导入的那个包，每个包只会初始化一次。？

#### 6.3.1使用`init`函数

在如下代码中，声明了两个包级别的变量和一个`init`函数，直接运行程序会首先初始化定义的包级别的变量，然后执行`init`函数，`init`函数中是判断两个包级别的变量的和是否小于0，如果小于则通过`log.Fatal()`方法输出对应信息，并终止程序。

```go
package calculate

import (
	"log"
)

// 定义包级别的变量
var (
	a = -13
	b = 1
)

func init() {
	if Add(a, b) <= 0 {
		log.Fatal("相加后的结果小于0")
	}
}

//Add 计算加，在返回值的括号可以直接声明变量
func Add(a, b int) (result1 int) {
	result1 = a + b // 相加
	return
}
```

#### 6.3.2空白标识符

在go语言中，是不允许使用导入了包，却不使用包中的内容，这种做法的，原因是为了防止导入了过多没有使用的包，导致程序的编译时间过长。但是在我们的开发过程中，常常会先导入这个包，暂时不使用或者是只是为了确保这个包能进行初始化的时候，我们可以使用空白标识符，来避免编译出错。

```go
package main

import (
	_ "blogTest/calculate" // 使用空白标识符，没有使用这个包，但是还是对其进行了初始化
	"fmt"
)

func main() {
	var (
		a = 1
		b = 2
	)
	//res := calculate.Add(a, b)
	fmt.Println(a + b)
}
```

## 7.条件语句

>go中的条件语句可以分为两种，一种是`if.. else ..`语句，另外一种是`switch`语句，前者多用于少量条件时，后者多用于大量条件时。

### 7.1 `if.. else ..`语句

在go中，if语句后即使只有一条语句，大括号也是必须存在的，基础语法为

```go
// condition代表判断条件，如果condition为真，则执行代码块中的内容。
if condition {  
}
```

下面是一个实例，在demo函数中判断传入的参数在哪个大小范围内，自上向下进行条件判断

```go
package main

import (
	"fmt"
)

func main() {
	var a = 86
	demo(a)
}

func demo(num int) {
	if num <= 50 {
		fmt.Println("数字小于或等于50")
	} else if num >= 51 && num <= 100 {
		fmt.Println("数字大于或等于51 小于或等于100")
	} else {
		fmt.Println("数字大于100")
	}
}
```

### 7.2`switch`语句

switch 是一个条件语句，用于将表达式的值与可能匹配的选项列表进行比较，并根据匹配情况执行相应的代码块。它可以被认为是替代多个 `if else` 子句的常用方式。

如下面的实例所示，`switch a`会从上到下的将a的值和case的每个值进行比较，并执行和case值相同的代码逻辑，如果每个case值都不匹配，就会执行default对应的代码逻辑。

```go
package main

import (
	"fmt"
)

func main() {
	var a = 6
	switch a {
	case 0:
		fmt.Println("今天是周日")
	case 1:
		fmt.Println("今天是周一")
	case 2:
		fmt.Println("今天是周二")
	case 3:
		fmt.Println("今天是周三")
	case 4:
		fmt.Println("今天是周四")
	case 5:
		fmt.Println("今天是周五")
	case 6:
		fmt.Println("今天是周六")
	default:
		fmt.Println("条件参数错误....")
	}
}
```

在case后面可以包含多个值，使用逗号隔开。

`switch`后面不包含值，等同于`switch true`，不过这种情况出现的时候会执行所有的case。

可以使用`fallthrough`语句，在一个case执行完毕后，继续执行后续的case，`fallthrough`语句必须放在case语句的最后一行。

```go
package main

import (
	"fmt"
)

func main() {
	var a = 5
    // case后包含多个值
	switch a {
	case 0, 6:
		fmt.Println("今天是休息日")
	case 1, 2, 3, 4, 5:
		fmt.Println("今天是工作日")
	default:
		fmt.Println("条件参数错误....")
	}
    // switch后面不包含值
	switch {
	case a == 0:
		fmt.Println("今天是休息日")
	case a > 0:
		fmt.Println("今天是工作日")
	default:
		fmt.Println("条件参数错误....")
	}
    // fallthrough语句
	switch a {
	case 0:
		fmt.Println("今天是休息日")
	case 1:
		fmt.Println("今天是工作日")
	case 2:
		fmt.Println("今天是工作日")
	case 3:
		fmt.Println("今天是工作日")
	case 4:
		fmt.Println("今天是工作日")
	case 5:
		fmt.Println("今天是工作日")
        fallthrough
	case 6:
		fmt.Println("今天也是工作日")
	default:
		fmt.Println("条件参数错误....")
	}
}
```

## 8.循环语句

> go的循环语句只有for循环，没有`while` 和 `do while` 循环

在循环语句中，`i := 1`这个初始化语句只执行一次，初始化完成后，进行`i <= 10`条件判断，如果判断为true则直接代码块中的语句，反之则退出循环，最后执行`i++`post语句，重复这个顺序，直到退出循环。使用`continue`可以跳过本次循环，直接开始下一个循环，使用`break`可以退出整个循环。

```go
package main

import (
	"fmt"
)

func main() {
	for i := 1; i <= 10; i++ {
		if i == 3 {
			continue
		}
		if i == 5 {
			break
		}
		fmt.Printf(" %d", i)
	}
}
```

如果需要使用无限循环，则可以采用下面的语句

```go
package main

import "fmt"

func main() {  
    for {
        fmt.Println("Hello World")
    }
}
```

