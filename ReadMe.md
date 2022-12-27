[Go官网](https://go.dev/)    [Go语言圣经](https://studygolang.com/book/42)  



## 一、安装

> windows 32位安装:go***.windows-386.zip
>
> windows 64位安装:go***.windows-amd64.zip

配置:

| 环境变量 | 说明                       |
| -------- | -------------------------- |
| GOROOT   | 指定SDK的安装目录          |
| PATH     | 添加SDK的bin目录           |
| GOPATH   | 工作目录，go项目的工作路径 |

>  命令go env -w GO111MODULE=auto

## 二、概述

运行:

> go run **.go

编译运行:

> go bulid **.go     //go build -o 目的exe文件 源main包
>
> ./main.exe

Golang程序编写的规则:

1 ) go文件的后缀 .go

2.) go程序区分大小写

3 ) go的语句后，不需要带分号

4 ) go定义的变量，或者import 包，必须使用，如果没有使用就会报错

5 ) go中，不要把多条语句放在同一行。否则报错

6 ) go中的大括号成对出现

## 三、变量
变量相当于内存中一个数据存储空间的表示，可以把变量看做是一个房间的门牌号，通过门牌号我们可以找到房间，同样的道理，通过变量名可以访问到变量(值)。

Golang的变量如果没有赋初值，编译器会使用默认值, 比如 int 默认值 0 string默认值为空串， 小数默认为 0

声明变量:

```go
//基本语法： var 变量名 数据类型
var a int//这就是声明了一个变量，一个变量名是a
var num1 float32 //这也声明了一个变量，表示一个单精度类型的小数，变量名是num1初始变量
```

初始变量:

```go
//在声明变量的时候，就给值。
var a int = 45 //这就是初始化变量a
var b = 400 //如果声明时就直接赋值，可省略数据类型
b := 400 //类型推导
```

变量赋值:

```go
var num int //默认0
num = 780 //给变量赋值
```


### 3.1 整形
1 ) Golang各整数类型分：有符号和无符号，int，uint 的大小和系统有关。

2 ) Golang的整型默认声明为 int 型

```go
//整型的使用细节
var n1 = 100 // ? n1 是什么类型
//查看某个变量的数据类型
//fmt.Printf() 可以用于做格式化输出。
fmt.Printf("n1 的 类型 %T \n", n1) //n1 的 类型 int
```

3 ) 查看某个变量的字节大小和数据类型 （使用较多）

```go
//如何在程序查看某个变量的占用字节大小和数据类型 （使用较多）
var n2 int64 = 10
//unsafe.Sizeof(n1) 是unsafe包的一个函数，可以返回n1变量占用的字节数
fmt.Printf("n2 的 类型 %T  n2占用的字节数是 %d ", n2, unsafe.Sizeof(n2)) //n2 的 类型 int64  n2占用的字节数是 8
```

4 ) Golang程序中整型变量在使用时，遵守保小不保大的原则，即：在保证程序正确运行下，尽量 使用占用空间小的数据类型。【如：年龄】

```go
var age byte = 90
```

5 ) 浮点型常量有两种表示形式

十进制数形式：如： 5.12 . 512 (必须有小数点）

科学计数法形式:如： 5. 1234 e 2 = 5. 12 * 10 的 2 次方 5. 12 E- 2 = 5. 12 / 10 的 2 次方

```go
package main
import (
	"fmt"
)

//演示golang中小数类型使用
func main() {
    var price float32 = 89.12
	fmt.Println("price=", price) //price= 89.12
	var num1 float32 = -0.00089
	var num2 float64 = -7809656.09
	fmt.Println("num1=", num1, "num2=", num2)//num1= -0.00089 num2= -7.80965609e+06 

	//尾数部分可能丢失，造成精度损失。 -123.0000901
	var num3 float32 = -123.0000901
	var num4 float64 = -123.0000901
	fmt.Println("num3=", num3, "num4=", num4) //num3= -123.00009 num4= -123.0000901 

	//Golang 的浮点型默认声明为float64 类型
	var num5 = 1.1
	fmt.Printf("num5的数据类型是 %T \n", num5) //num5的数据类型是 float64 
    //十进制数形式：如：5.12       .512   (必须有小数点）
    num6 := 5.12
    num7 := .123 //=> 0.123
    fmt.Println("num6=", num6, "num7=", num7)

    //科学计数法形式
    num8 := 5.1234e2 // ? 5.1234 * 10的2次方 
    num9 := 5.1234E2 // ? 5.1234 * 10的2次方 shift+alt+向下的箭头
    num10 := 5.1234E-2 // ? 5.1234 / 10的2次方 0.051234

    fmt.Println("num8=", num8, "num9=", num9, "num10=", num10)//num8= 512.34 num9= 512.34 num10= 0.051234
    var c1 rune = '北'
    fmt.Println("c1=", c1, unsafe.Sizeof(c1))//c1= 21271 4
}
```

通常情况下，应该使用 float 64 ，因为它比float 32 更精确。推荐使用 float 64

### 3.2 字符类型
1 ) 字符型 存储到 计算机中，需要将字符对应的码值（整数）找出来

存储：字符—>对应码值---->二进制–>存储

读取：二进制----> 码值 ---->字符 --> 读取

2 ) 字符和码值的对应关系是通过字符编码表决定的(是规定好)

3 )Go语言的编码都统一成了utf- 8 。非常的方便，很统一，再也没有编码乱码的困扰了

注意：

1 ) Go语言的字符串的字节使用UTF- 8 编码标识Unicode文本，这样Golang统一使用UTF- 8 编码,中文 乱码问题不会再困扰程序员。

2 ) 字符串一旦赋值了，字符串就不能修改了：在Go中字符串是不可变的。

### 3.3 数据类型转换
Golang 和java/c 不同，Go 在不同类型的变量之间赋值时需要显式转换。也就是说Golang中数据类型不能**自动转换**。

#### 3.3.1 基本语法
表达式 T(v) 将值 v 转换为类型 T

> T : 就是数据类型，比如 int 32 ，int 64 ，float 32 等等
>
> v : 就是需要转换的变量

被转换的是变量存储的数据(即值)，变量本身的数据类型并没有变化！

```go
//演示golang中基本数据类型的转换
func main() {

	var i int32 = 100
	//希望将 i => float
	var n1 float32 = float32(i)
	var n2 int8 = int8(i)
	var n3 int64 = int64(i) //低精度->高精度

	fmt.Printf("i=%v n1=%v n2=%v n3=%v \n", i ,n1, n2, n3)//i=100 n1=100 n2=100 n3=100
	
	//被转换的是变量存储的数据(即值)，变量本身的数据类型并没有变化
	fmt.Printf("i type is %T\n", i) // i type is int32

	//在转换中，比如将 int64  转成 int8 【-128---127】 ，编译时不会报错，
	//只是转换的结果是按溢出处理，和我们希望的结果不一样
	var num1 int64 = 999999
	var num2 int8 = int8(num1) 
	fmt.Println("num2=", num2)//num2= 63 
}
```
在转换中，比如将 int 64 转成 int 8 【- 128 - – 127 】 ，编译时不会报错，只是转换的结果是按**溢出处理**，和我们希望的结果不一样。 因此在转换时，需要考虑范围.
