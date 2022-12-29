[Go官网](https://go.dev/)    [Go语言圣经](https://studygolang.com/book/42)  

[API文档](http://doc.golang.ltd/)

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

//默认GoPROXY配置是：GOPROXY=https://proxy.golang.org,direct

>  设置代理go env -w GOPROXY=https://goproxy.cn,direct

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

## 四、运算符



## 五、程序流程控制



## 六、函数,包和错误处理

### 6.1 函数概念
不用函数的弊端

1）写法可以完成功能, 但是代码冗余

2 ) 同时不利于代码维护

**概念**：为完成某一功能的程序指令(语句)的集合,称为函数。

在Go中,函数分为: 自定义函数、系统函数

基本语法

```go
//函数的基本语法
func 函数名（形参列表）（返回值列表）{ // 形参名在前 形参类型在后
    执行语句..
    return 返回值列表
}
```

- 形参列表：表示函数的输入
- 函数中的语句：表示为了实现某一功能代码块
- 函数可以有返回值，也可以没有

```go
package main
import (
	"fmt"
)

func cal(n1 float64, n2 float64, operator byte) float64 {
	var res float64
	switch operator {
		case '+':
			res = n1 + n2
		case '-':
			res = n1 - n2
		case '*':
			res = n1 * n2
		case '/':
			res = n1 / n2
		default:
			fmt.Println("操作符号错误...")
	}
	return res
}

func main() {
	//输入两个数,再输入一个运算符(+,-,*,/)，得到结果.。
	var n1 float64 = 1.2
	var n2 float64 = 2.3
	var operator byte = '+'
	result := cal(n1, n2 , operator) 
	fmt.Println("result~=", result)//result~= 3.5 
}
```

### 6.2 包的概念
包的本质实际上就是创建不同的文件夹，来存放程序文件。

说明：go的每一个文件都是属于一个包的，也就是说go是以包的形式来管理文件和项目目录结构的

**包的三大作用:**

- 区分相同名字的函数、变量等标识符
- 当程序文件很多时,可以很好的管理项目
- 控制函数、变量等访问范围，即作用域

**打包基本语法:**

```go
package 包名
```

**引入包的基本语法:**

```go
//方式一
import "包的路径"
//方式二
import (
	"包名"
	"包名"
)
```

**注意事项:**

1 ) 在给一个文件打包时，该包对应一个文件夹，比如这里的 utils 文件夹对应的包名就是utils,文件的包名通常和文件所在的文件夹名一致，一般为小写字母。

2 ) 当一个文件要使用其它包函数或变量时，需要先引入对应的包

- package 指令在 文件第一行，然后是 import 指令。
- 在import 包时，路径从 `$GOPATH`的 `src` 下开始，不用带`src`, 编译器会自动从`src`下开始引入

3 ) 为了让其它包的文件，可以访问到本包的函数，则该函数名的首字母需要大写，类似其它语言的public,这样才能跨包访问。比如 utils.go 的

```go
//将计算的功能，放到一个函数中，然后在需要使用，调用即可
//为了让其它包的文件使用Cal函数，需要将C大小类似其它语言的public
var Num1 int = 300
func Cal(n1 float64, n2 float64, operator byte) float64 {}
```

4 ) 在访问其它包函数，变量时，其语法是 `包名.函数名`， 比如这里的 main.go文件中

```go
package main
import (
	"fmt"
	"go_code/chapter06/fundemo01/utils"
)
func main() {
	fmt.Println("utils.go Num~=", utils.Num1)//utils.go Num~= 300
	//输入两个数,再输入一个运算符(+,-,*,/)，得到结果.。
	var n1 float64 = 1.2
	var n2 float64 = 2.3
	var operator byte = '+'
	result := utils.Cal(n1, n2 , operator) 
	fmt.Println("result~=", result)//result~= 3.5 
}
```

5 ) 如果包名较长，Go支持给包取别名， 注意细节：取别名后，原来的包名就不能使用了

```go
package main
import (
	"fmt"
	util "go_code/chapter06/fundemo01/utils"
)
```

**说明**: 如果给包取了别名，则需要**使用别名来访问该包的函数和变量**。

6.) 在同一包下，不能有相同的函数名（也不能有相同的全局变量名），否则报重复定义

7 ) 如果你要编译成一个可执行程序文件，就需要将这个包声明为 main, 即 `package main`，这个就 是一个语法规范，如果你是写一个库 ，包名可以自定义
### 6.3 函数的调用机制
( 1 ) 在调用一个函数时，会给该函数分配一个新的空间，编译器会通过自身的处理让这个新的空间和其它的栈的空间区分开来

( 2 ) 在每个函数对应的栈中，数据空间是独立的，不会混淆

( 3 ) 当一个函数调用完毕(执行完毕)后，程序会销毁这个函数对应的栈空间。

### 6.4 return
基本语法和说明

```go
// Go函数支持返回多个值，这一点是其他编程语言没有的
func 函数名(形参列表)(返回值类型列表){
    语句
    return 返回值列表
}
```

1.如果返回多个值，在接收时，希望忽略某个返回值，则使用_符号表示占位忽略

2.如果返回值只有一个，返回值类型列表可以不写()

### 6.5 函数递归调用
一个函数在函数体内又调用了本身，我们称为递归调用

**函数递归需要遵守的重要原则:**

1 ) 执行一个函数时，就创建一个新的受保护的独立空间(新函数栈)

2 ) 函数的局部变量是独立的，不会相互影响

3 ) 递归必须向退出递归的条件逼近，否则就是无限递归

4 ) 当一个函数执行完毕，或者遇到return，就会返回，遵守谁调用，就将结果返回给谁，同时当函数执行完毕或者返回时，该函数本身也会被系统销毁

题1 ：斐波那契数

请使用递归的方式，求出斐波那契数 1 , 1 , 2 , 3 , 5 , 8 , 13

给你一个整数n，求出它的斐波那契数是多少？
```go
package main
import (
	"fmt"
)
//请使用递归的方式，求出斐波那契数1,1,2,3,5,8,13...
//给你一个整数n，求出它的斐波那契数是多少？
func fbn(n int) int {
	if (n == 1 || n == 2) {
		return 1
	} else {
		return fbn(n - 1) + fbn(n - 2)
	}
}

func main() {
	res := fbn(3)
	fmt.Println("res=", res)// res= 2
	fmt.Println("res=", fbn(4)) // 3
	fmt.Println("res=", fbn(5)) // 5 
	fmt.Println("res=", fbn(6)) // 8 
}
```

### 6.6 函数注意事项
1 ) 函数的形参列表可以是多个，返回值列表也可以是多个。

2 ) 形参列表和返回值列表的数据类型可以是值类型和引用类型。

3 ) 函数的命名遵循标识符命名规范，首字母不能是数字，首字母**大写**该函数可以被本包文件和其它包文件使用，类似public, 首字母**小写**，只能被本包文件使用，其它包文件不能使用，类似privat

4 ) 函数中的变量是局部的，函数外不生效

```go
package main
import (
	"fmt"
)
//函数中的变量是局部的，函数外不生效
func test(){
    //n1 是 test函数的局部变量，只能在test中使用
    var n1 int = 10
}

func main() {	
	fmt.Println("n1=", n1) //报错，这里不能使用n1
}
```


5 ) 基本数据类型和数组默认都是值传递的，即进行值拷贝。在函数内修改，不会影响到原来的值。

```go
package main
import (
	"fmt"
)

func test02(n1 int){
	n1 = n1 + 10
	fmt.Println("test02() n1=", n1)//30
}

func main() {	
	num := 20
	test02(num)
	fmt.Println("main() num=", num)//20
}
```


6 ) 如果希望函数内的变量能修改函数外的变量(指的是默认以值传递的方式的数据类型)，可以传入变量的地址&，函数内以指针的方式操作变量。从效果上看类似引用 。

```go
package main
import (
	"fmt"
)

// n1 就是 *int 类型
func test03(n1 *int) {
	fmt.Printf("n1的地址 %v\n",&n1)//n1的地址 0xc000180018
	*n1 = *n1 + 10
	fmt.Println("test03() n1= ", *n1) // 30  
}

func main() {
	num := 20
	fmt.Printf("num的地址=%v\n", &num)//num的地址=0xc000186018
	test03(&num)
	fmt.Println("main() num= ", num) // 30
}
```

7 ) Go函数不支持函数重载

```go
package main
import (
	"fmt"
)
//有两个test02不支持重载
func test02(n1 int) {	
	n1 = n1 + 10
	fmt.Println("test02() n1= ", n1)
}
//有两个test02不支持重载
func test02(n1 int , n2 int) {
}

func main() {
}
```


8 ) 在Go中，函数也是一种数据类型，可以赋值给一个变量，则该变量就是一个函数类型的变量了。通过该变量可以对函数调用

```go
package main
import (
	"fmt"
)

//在Go中，函数也是一种数据类型，
//可以赋值给一个变量，则该变量就是一个函数类型的变量了。通过该变量可以对函数调用
func getSum(n1 int, n2 int) int {
	return n1 + n2
}

func main() {
	a := getSum
    fmt.Printf("a的类型%T, getSum类型是%T\n", a, getSum)
    //a的类型func(int, int) int, getSum类型是func(int, int) int

    res := a(10, 40) // 等价  res := getSum(10, 40)
    fmt.Println("res=", res)
}
```


9 ) 函数既然是一种数据类型，因此在Go中，函数可以作为形参，并且调用

```go
package main
import (
	"fmt"
)

//在Go中，函数也是一种数据类型，
//可以赋值给一个变量，则该变量就是一个函数类型的变量了。通过该变量可以对函数调用
func getSum(n1 int, n2 int) int {
	return n1 + n2
}

//函数既然是一种数据类型，因此在Go中，函数可以作为形参，并且调用
func myFun(funvar func(int, int) int, num1 int, num2 int ) int {
	return funvar(num1, num2)
}

func main() {
	//看案例
	res2 := myFun(getSum, 50, 60)
	fmt.Println("res2=", res2)
}
```


10 ) 为了简化数据类型定义，Go支持自定义数据类型

> 基本语法：type 自定义数据类型名 数据类型 // 理解: 相当于一个别名

```go
package main
import (
	"fmt"
)

//在Go中，函数也是一种数据类型，
//可以赋值给一个变量，则该变量就是一个函数类型的变量了。通过该变量可以对函数调用

func getSum(n1 int, n2 int) int {
	return n1 + n2
}

//函数既然是一种数据类型，因此在Go中，函数可以作为形参，并且调用
func myFun(funvar func(int, int) int, num1 int, num2 int ) int {
	return funvar(num1, num2)
}

//这时 myFun 就是 func(int, int) int类型
type myFunType func(int, int) int

//函数既然是一种数据类型，因此在Go中，函数可以作为形参，并且调用
func myFun2(funvar myFunType, num1 int, num2 int ) int {
	return funvar(num1, num2)
}

func main() {
    // 给int取了别名，在go中 myInt 和 int 虽然都是int类型，但是go认为myInt和int两个类型
    type myInt int 

    var num1 myInt 
    var num2 int
    num1 = 40
    num2 = int(num1) //注意这里依然需要显示转换,go认为myInt和int两个类型
    fmt.Println("num1=", num1, "num2=",num2)

    res3 := myFun2(getSum, 500, 600)
    fmt.Println("res3=", res3)
}
```

11 )支持对函数返回值命名

```go
package main
import (
	"fmt"
)

//支持对函数返回值命名
func getSumAndSub(n1 int, n2 int) (sum int, sub int){
	sub = n1 - n2
	sum = n1 + n2
	return
}

func main() {
    a1, b1 := getSumAndSub(1, 2)
    fmt.Printf("a=%v b=%v\n", a1, b1)
}
```

12 ) 使用 _ 标识符，忽略返回值

13 ) Go支持可变参数

```go
//支持0到多个参数,args是slice切片，通过args[index]可以访问到各个值
//如果一个函数的形参列表中有可变的参数，则可变参数需要放到形参列表的最后
func sum(args...int){
}
//支持1到多个参数
func sum(n1 int,args... int) sum int{
     sum := n1 
	//遍历args 
	for i := 0; i < len(args); i++ {
		sum += args[i]  //args[0] 表示取出args切片的第一个元素值，其它依次类推
	}
	return sum
}
```

### 6.7 init()函数
每一个源文件都可以包含一个 init 函数，该函数会在main函数执行前，被Go运行框架调用，也就是说init会在main函数前被调用。

**注意事项：**

1 ) 如果一个文件同时包含**全局变量定义**， **init 函数**和 **main 函数**，则执行的流程**全局变量定义 - >init函数 - >main 函数**

2 ) init函数最主要的作用，就是完成一些**初始化的工作**

```go
package utils
import "fmt"
var Age int
var Name string

//Age 和 Name 全局变量，我们需要在main.go 使用,但是我们需要初始化Age 和 Name
//init 函数完成初始化工作
func init() {
	fmt.Println("utils 包的  init()...")
	Age = 100
	Name = "tom~"
}
```

```go
package main
import (
	"fmt"
	//引入包
	"go_code/chapter06/funcinit/utils"
)

var age = test()

//为了看到全局变量是先被初始化的，我们这里先写函数
func test() int {
	fmt.Println("test()") //1
	return 90
}

//init函数,通常可以在init函数中完成初始化工作
func init() {
	fmt.Println("init()...") //2
}

func main() {
	fmt.Println("main()...age=", age) //3
	fmt.Println("Age=", utils.Age, "Name=", utils.Name)
}
/*
utils 包的  init()...
test()
init()...
main()...age= 90     
Age= 100 Name= tom~ 
*/
```

![init执行顺序](imag/init执行顺序.png)

### 6.8 匿名函数

Go支持匿名函数，匿名函数就是没有名字的函数，如果我们某个函数只是希望使用一次，可以考 虑使用匿名函数，匿名函数也可以实现多次调用。

**匿名函数使用方式 1**

在定义匿名函数时就直接调用，这种方式匿名函数只能调用一次。

```go
package main
import (
	"fmt"
)
func main() {
	//在定义匿名函数时就直接调用，这种方式匿名函数只能调用一次
	//求两个数的和， 使用匿名函数的方式完成
	res1 := func (n1 int, n2 int) int {
		return n1 + n2
	}(10, 20)
	fmt.Println("res1=", res1)//res1= 30
}
```

**匿名函数使用方式 2**

将匿名函数赋给一个变量(函数变量)，再通过该变量来调用匿名函数

```go
package main
import (
	"fmt"
)

func main() {
	//将匿名函数func (n1 int, n2 int) int赋给 a变量
	//则a 的数据类型就是函数类型 ，此时,我们可以通过a完成调用
	a := func (n1 int, n2 int) int {
		return n1 - n2
	}
	res2 := a(10, 30)
	fmt.Println("res2=", res2)//res2= -20
	res3 := a(90, 30)
	fmt.Println("res3=", res3)//res3= 60
}
```

**全局匿名函数**

如果将匿名函数赋给一个全局变量，那么这个匿名函数，就成为一个全局匿名函数，可以在程序有效。

```go
package main
import (
	"fmt"
)

var (
	//fun1就是一个全局匿名函数
	Fun1 = func (n1 int, n2 int) int {
		return n1 * n2
	}
)

func main() {
	//全局匿名函数的使用
	res4 := Fun1(4, 9)
	fmt.Println("res4=", res4)//res4= 36
}
```

### 6.9 闭包

基本介绍：闭包就是一个函数和与其相关的引用环境组合的一个整体(实体)

**闭包让你可以在一个内层函数中访问到其外层函数的作用域。**

可简单理解为：**有权访问另一个函数作用域内变量的函数都是闭包。**

```go
package main
import (
	"fmt"
)

//累加器,AddUpper 是一个函数，返回的数据类型是 fun(int)int
func AddUpper() func (int) int {
    //返回的是一个匿名函数, 但是这个匿名函数引用到函数外的n,因此这个匿名函数就和n形成一个整体，构成闭包。
	var n int = 10 
	return func (x int) int {
		n = n + x
		return n
	}
}

func main() {
	f := AddUpper()
	fmt.Println(f(1))// 11 
	fmt.Println(f(2))// 13
	fmt.Println(f(3))// 16

}
```

#### 6.9.1使用案例

闭包的好处，如果使用传统的方法，也可以轻松实现这个功能，但是传统方法需要每次都传入后缀名，比如 .jpg,而闭包因为可以保留上次引用的某个值，所以我们传入一次就可以反复使用。

以面向对象思想理解闭包，外部整体像一个类，先传入的.jpg 像设置类里的一个public属性，再向返回函数传参像调用类的成员函数，此时成员函数可以调用类里已设置的属性。

```go
package main
import (
	"fmt"
	"strings"
)

// 1)编写一个函数 makeSuffix(suffix string)  可以接收一个文件后缀名(比如.jpg)，并返回一个闭包
// 2)调用闭包，可以传入一个文件名，如果该文件名没有指定的后缀(比如.jpg) ,则返回 文件名.jpg , 如果已经有.jpg后缀，则返回原文件名。
// 3)使用闭包的方式完成
// 4)strings.HasSuffix , 该函数可以判断某个字符串是否有指定的后缀。

//返回的匿名函数和 makeSuffix(suffixstring) 的 suffix 变量 组合成一个闭包,因为 返回的函数引用到suffix这个变量
func makeSuffix(suffix string) func (string) string {
	return func (name string) string {
		//如果 name 没有指定后缀，则加上，否则就返回原来的名字
		if !strings.HasSuffix(name, suffix) {
			return name + suffix
		}
		return name
	}
}

func makeSuffix2(suffix string, name string)  string {
	//如果 name 没有指定后缀，则加上，否则就返回原来的名字
	if !strings.HasSuffix(name, suffix)  {
		return name + suffix
	}
	return name
}

func main() {
	//返回一个闭包
	f2 := makeSuffix(".jpg") //如果使用闭包完成，好处是只需要传入一次后缀。
	fmt.Println("文件名处理后=", f2("winter")) // winter.jgp
	fmt.Println("文件名处理后=", f2("bird.jpg")) // bird.jpg

	fmt.Println("文件名处理后=", makeSuffix2("jpg", "winter")) // winter.jgp
	fmt.Println("文件名处理后=", makeSuffix2("jpg", "bird.jpg")) // bird.jpg
}
```

#### 6.9.2 闭包经典使用场景
1、return一个内部函数，读取内部函数的变量

2、函数作为参数

3、IIFE（自执行函数）

5、使用回调函数就是在使用闭包

6、将外部函数创建的变量值始终保持在内存中；（会出现内存泄漏）

#### 6.9.3 使用闭包注意点
因为使用闭包会包含其他函数的作用域，会比其他函数占据更多的内存空间，不会在调用结束之后被垃圾回收机制（简称GC机制）回收，多度使用闭包会过度占用内存，造成内存泄漏。

#### 6.9.4 闭包相关面试题
1、简述什么是闭包，闭包的作用是什么？写出一个简单的闭包例子。

2、闭包会造成内存泄漏吗？

会，因为使用闭包会包含其他函数的作用域，会比其他函数占据更多的内存空间，不会在调用结束之后被垃圾回收机制回收，多度使用闭包会过度占用内存，造成内存泄漏。

3、for循环和闭包(必刷题)

### 6.10 defer

在函数中，程序员经常需要创建资源(比如：数据库连接、文件句柄、锁等) ，为了在**函数执行完毕后，及时的释放资源**，Go的设计者提供defer(延时机制)。defer 最主要的价值是在，当函数执行完毕后，可以及时的释放函数创建的资源。看下模拟代码。

```go
package main
import (
	"fmt"
)

func sum(n1 int, n2 int) int {
	//当执行到defer时，暂时不执行，会将defer后面的语句压入到独立的栈(defer栈)
	//当函数执行完毕后，再从defer栈，按照先入后出的方式出栈，执行
	defer fmt.Println("ok1 n1=", n1) //defer 3. ok1 n1 = 10
	defer fmt.Println("ok2 n2=", n2) //defer 2. ok2 n2= 20

	res := n1 + n2 // res = 30
	fmt.Println("ok3 res=", res) // 1. ok3 res= 30
	return res
}

func main() {
	res := sum(10, 20)
	fmt.Println("res=", res)  // 4. res= 30
}
//-------结果--------
ok3 res= 30
ok2 n2= 20
ok1 n1 = 10
res= 30
```

**注意事项**

1 ) 当go执行到一个defer时，不会立即执行defer后的语句，而是将defer 后的语句压入到一个栈中[我为了讲课方便，暂时称该栈为defer栈],然后继续执行函数下一个语句。

2 ) 当函数执行完毕后，在从defer栈中，依次从栈顶取出语句执行(注：遵守栈 先入后出的机制)，所以同学们看到前面案例输出的顺序。

3 ) 在defer 将语句放入到栈时，也会将相关的值拷贝同时入栈。

**defer使用**

1 ) 在golang编程中的通常做法是，创建资源后，比如(打开了文件，获取了数据库的链接，或者是锁资源)， 可以执行 defer file.Close() defer connect.Close()

2 ) 在defer后，可以继续使用创建资源.

3 ) 当函数完毕后，系统会依次从defer栈中，取出语句，关闭资源.

4 ) 这种机制，非常简洁，程序员不用再为在什么时机关闭资源而烦心。
### 6.11 函数传递方式
**传递方式分类**

1 ) 值传递

2 ) 引用传递

其实，不管是值传递还是引用传递，传递给函数的都是变量的副本，不同的是，值传递的是值的拷贝，引用传递的是地址的拷贝，一般来说，地址拷贝效率高，因为数据量小，而值拷贝决定拷贝的数据大小，数据越大，效率越低。

**值类型和引用类型**

1 ) 值类型：基本数据类型 int 系列，float 系列，bool，string ，数组和结构体struct

2 ) 引用类型：指针，slice切片，map，管道chan，interface 等都是引用类型

**特点**

1 ) 值类型默认是值传递:变量直接存储值，内存通常在**栈**中分配。

2 ) 引用类型默认是引用传递：变量存储的是一个地址，这个地址对应的空间才真正存储数据（值），内存通常在**堆**上分配，当没有任何变量引用这个地址时，改地址对应的数据空间就成为一个垃圾，由GC来回收。

3 ) 如果希望函数内的变量能修改函数外的变量，可以传入变量的地址&，函数内以指针的方式操作变量。从效果上看类似引用 。

### 6.12 变量作用域
1 ) 函数内部声明/定义的变量叫局部变量，作用域仅限于函数内部

2 ) 函数外部声明/定义的变量叫全局变量，作用域在整个包都有效，如果其首字母为大写，则作用域在整个程序有效

3 ) 如果变量是在一个代码块，比如 for/if中，那么这个变量的的作用域就在该代码块

### 6.13 字符串常用系统函数
1 ) 统计字符串的长度，按字节 len(str)

```go
func main(){
    //统计字符串的长度，按字节 len(str)
	////golang的编码统一为utf-8 (ascii的字符(字母和数字) 占一个字节，汉字占用3个字节)
	str := "hello北" 
	fmt.Println("str len=", len(str)) // 8
}
```

2 ) 字符串遍历，同时处理有中文的问题 r:=[]rune(str)
```go
func main(){
    str2 := "hello北京"
	//字符串遍历，同时处理有中文的问题 r := []rune(str)
	r := []rune(str2)
	for i := 0; i < len(r); i++ {
		fmt.Printf("字符=%c\n", r[i])
	}
}
```

3 ) 字符串转整数: n,err:=strconv.Atoi(" 12 ")
```go
func main(){
    //字符串转整数:	 n, err := strconv.Atoi("12")
	n, err := strconv.Atoi("123")
	if err != nil {
		fmt.Println("转换错误", err)
	}else {
		fmt.Println("转成的结果是", n)//转成的结果是 123
	}
}
```

4 ) 整数转字符串 str=strconv.Itoa( 12345 )
```go
func main(){
    //整数转字符串  str = strconv.Itoa(12345)
	str = strconv.Itoa(12345)
	fmt.Printf("str=%v, str=%T\n", str, str)//str=12345, str=string 
}
```

5 ) 字符串 转 []byte: varbytes=[]byte(“hello go”)
```go
func main(){
    //字符串 转 []byte:  var bytes = []byte("hello go")
	var bytes = []byte("hello go")
	fmt.Printf("bytes=%v\n", bytes)//bytes=[104 101 108 108 111 32 103 111]
}
```

6.) []byte 转 字符串:str=string([]byte{ 97 , 98 , 99 })
```go
func main(){
    //[]byte 转 字符串: str = string([]byte{97, 98, 99})
	str = string([]byte{97, 98, 99}) 
	fmt.Printf("str=%v\n", str)//str=abc
}
```
7 ) 10 进制转 2 , 8 , 16.进制: str=strconv.FormatInt( 123 , 2 )// 2 - > 8 , 16
```go
func main(){
    //10进制转 2, 8, 16进制:  str = strconv.FormatInt(123, 2),返回对应的字符串
	str = strconv.FormatInt(123, 2)
	fmt.Printf("123对应的二进制是=%v\n", str)//123对应的二进制是=1111011
	str = strconv.FormatInt(123, 16)
	fmt.Printf("123对应的16进制是=%v\n", str)//123对应的16进制是=7b
}
```
8 ) 查找子串是否在指定的字符串中:strings.Contains(“seafood”,“foo”)//true
```go
func main(){
    //查找子串是否在指定的字符串中: strings.Contains("seafood", "foo") //true
	b := strings.Contains("seafood", "mary")
	fmt.Printf("b=%v\n", b) //b=false
}
```
9 ) 统计一个字符串有几个指定的子串 ： strings.Count(“ceheese”,“e”)// 4
```go
func main(){
    //统计一个字符串有几个指定的子串 ： strings.Count("ceheese", "e") //4
	num := strings.Count("ceheese", "e")
	fmt.Printf("num=%v\n", num)//num=4
}
```
10 ) 不区分大小写的字符串比较(==是区分字母大小写的):fmt.Println(strings.EqualFold(“abc”,“Abc”))//true
```go
func main(){
    //不区分大小写的字符串比较(==是区分字母大小写的): fmt.Println(strings.EqualFold("abc", "Abc")) // true
	b = strings.EqualFold("abc", "Abc")
	fmt.Printf("b=%v\n", b) //true
	fmt.Println("结果","abc" == "Abc") // false //区分字母大小写
}
```
11 )返回子串在字符串第一次出现的index值，如果没有返回- 1 :strings.Index(“NLT_abc”,“abc”)// 4
```go
func main(){
    //返回子串在字符串第一次出现的index值，如果没有返回-1 : 
	//strings.Index("NLT_abc", "abc") // 4
	index := strings.Index("NLT_abcabcabc", "abc") // 4
	fmt.Printf("index=%v\n",index)
}
```
12 ) 返回子串在字符串最后一次出现的index，如没有返回- 1 :strings.LastIndex(“gogolang”,“go”)
```go
func main(){
    //返回子串在字符串最后一次出现的index，
	//如没有返回-1 : strings.LastIndex("go golang", "go")

	index = strings.LastIndex("go golang", "go") //3
	fmt.Printf("index=%v\n",index)

}
```
13 ) 将指定的子串替换成 另外一个子串:strings.Replace(“gogohello”,“go”,“go语言”,n)n可以指定你希望替换几个，如果n=- 1 表示全部替换
```go
func main(){
    //将指定的子串替换成 另外一个子串: strings.Replace("go go hello", "go", "go语言", n) 
	//n可以指定你希望替换几个，如果n=-1表示全部替换

	str2 = "go go hello"
	str = strings.Replace(str2, "go", "北京", -1)
	fmt.Printf("str=%v str2=%v\n", str, str2)//str=北京 北京 hello str2=go go hello
}
```
14 ) 按照指定的某个字符，为分割标识，将一个字符串拆分成字符串数组：strings.Split(“hello,wrold,ok”,“,”)
```go
func main(){
    //按照指定的某个字符，为分割标识，将一个字符串拆分成字符串数组： 
	//strings.Split("hello,wrold,ok", ",")
	strArr := strings.Split("hello,wrold,ok", ",")
	for i := 0; i < len(strArr); i++ {
		fmt.Printf("str[%v]=%v\n", i, strArr[i])
	} 
	fmt.Printf("strArr=%v\n", strArr)//strArr=[hello wrold ok] 
}
```
15 ) 将字符串的字母进行大小写的转换:strings.ToLower(“Go”)//gostrings.ToUpper(“Go”)//GO
```go
func main(){
    //将字符串的字母进行大小写的转换: 
	//strings.ToLower("Go") // go strings.ToUpper("Go") // GO

	str = "goLang Hello"
	str = strings.ToLower(str) 
	str = strings.ToUpper(str) 
	fmt.Printf("str=%v\n", str) //str=GOLANG HELLO
}
```
16.) 将字符串左右两边的空格去掉： strings.TrimSpace("tnalonegopherntrn ")
```go
func main(){
    //将字符串左右两边的空格去掉： strings.TrimSpace(" tn a lone gopher ntrn   ")
	str = strings.TrimSpace(" tn a lone gopher ntrn   ")
	fmt.Printf("str=%q\n", str)//str="tn a lone gopher ntrn"
}
```
17 ) 将字符串左右两边指定的字符去掉 ： strings.Trim(“!hello!”,“!”) //[“hello”]//将左右两边! 和 ""去掉

```go
func main(){
    //将字符串左右两边指定的字符去掉 ： 
	//strings.Trim("! hello! ", " !")  // ["hello"] //将左右两边 ! 和 " "去掉
	str = strings.Trim("! he!llo! ", " !")
	fmt.Printf("str=%q\n", str)//str="he!llo"
}
```
18 ) 将字符串左边指定的字符去掉 ： strings.TrimLeft(“!hello!”,“!”) //[“hello”]//将左边! 和 " "去掉

```go
func main(){
    str = strings.TrimLeft("! he!llo! ", " !")
	fmt.Printf("str=%q\n", str)//str="he!llo! "
}
```
19 ) 将字符串右边指定的字符去掉 ：strings.TrimRight(“!hello!”,“!”) //[“hello”]//将右边! 和 " "去掉

```go
func main(){
    str = strings.TrimRight("! he!llo! ", " !")
	fmt.Printf("str=%q\n", str)//str="! he!llo"
}
```
20 ) 判断字符串是否以指定的字符串开头:strings.HasPrefix("ftp:// 192. 168. 10. 1 ",“ftp”)//true
```go
func main(){
    //判断字符串是否以指定的字符串开头: 
	b = strings.HasPrefix("ftp://192.168.10.1", "hsp") 
	fmt.Printf("b=%v\n", b)//b=false
}
```

21 ) 判断字符串是否以指定的字符串结束:strings.HasSuffix(“NLT_abc.jpg”,“abc”)//false

```go
func main(){
    //判断字符串是否以指定的字符串结束
    b = strings.HasSuffix("ftp://192.168.10.1", "10.1") //true
	fmt.Printf("b=%v\n", b)
}
```

### 6.14 时间和日期相关函数
1 ) 时间和日期相关函数，需要导入 time包

2 ) time.Time 类型，用于表示时间

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	//看看日期和时间相关函数和方法使用
	//获取当前时间
	now := time.Now()
	fmt.Printf("now=%v now type=%T\n", now, now)
    //now=2022-12-29 10:55:38.068575 +0800 CST m=+0.012695601 now type=time.Time
}
```

3 ) 如何获取到部分的日期信息

```go
package main
import (
	"fmt"
	"time"
)
func main() {
	//看看日期和时间相关函数和方法使用
	//1. 获取当前时间
	now := time.Now()
	fmt.Printf("now=%v now type=%T\n", now, now)
    //now=2022-12-29 10:55:38.068575 +0800 CST m=+0.012695601 now type=time.Time

	//2.通过now可以获取到年月日，时分秒
	fmt.Printf("年=%v\n", now.Year())//年=2022
	fmt.Printf("月=%v\n", now.Month())//月=December
	fmt.Printf("月=%v\n", int(now.Month()))//月=12
	fmt.Printf("日=%v\n", now.Day())//日=29
	fmt.Printf("时=%v\n", now.Hour())//时=10
	fmt.Printf("分=%v\n", now.Minute())//分=55
	fmt.Printf("秒=%v\n", now.Second())//秒=38
}
```

4 ) 格式化日期时间

方式 1 : 就是使用Printf 或者 SPrintf

```go
package main
import (
	"fmt"
	"time"
)

func main() {
    now := time.Now()
	//格式化日期时间    
	fmt.Printf("当前年月日 %d-%d-%d %d:%d:%d \n", now.Year(), 
	now.Month(), now.Day(), now.Hour(), now.Minute(), now.Second())//当前年月日 2022-12-29 10:55:38

    //fmt.Sprintf 来格式化字符串
	dateStr := fmt.Sprintf("当前年月日 %d-%d-%d %d:%d:%d \n", now.Year(), 
	now.Month(), now.Day(), now.Hour(), now.Minute(), now.Second())//

	fmt.Printf("dateStr=%v\n", dateStr)//dateStr=当前年月日 2022-12-29 10:55:38
}
```

方式二: 使用 time.Format() 方法完成:

```go
package main
import (
	"fmt"
	"time"
)

func main() {
    now := time.Now()
	//格式化日期时间的第二种方式
	fmt.Printf(now.Format("2006-01-02 15:04:05"))//2022-12-29 10:55:38
	fmt.Println()
	fmt.Printf(now.Format("2006-01-02"))//2022-12-29
	fmt.Println()
	fmt.Printf(now.Format("15:04:05"))//10:55:38
	fmt.Println()
	fmt.Printf(now.Format("2006"))//2022
	fmt.Println()
}
```

5 ) 时间的常量

```go
const(
     Nanosecond Duration= 1 //纳秒
     Microsecond = 1000 *Nanosecond //微秒
     Millisecond = 1000 *Microsecond//毫秒
     Second = 1000 *Millisecond//秒
     Minute = 60 *Second//分钟
     Hour = 60 *Minute//小时
)
```

常量的作用:**在程序中可用于获取指定时间单位的时间，比如想得到 100 毫秒**

```go
100 *time.Millisecond
```

6 ) 使用Sleep测量时间

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	i := 0
	for {
		i++
		fmt.Println(i)
		//休眠
		//time.Sleep(time.Second)//每隔1秒中打印一个数字，打印到100时就退出
		time.Sleep(time.Millisecond * 100)//每隔0.1秒中打印一个数字，打印到100时就退出
		if i == 100 {
			break
		}
	}
}
```

7 ) time的Unix和UnixNano的方法

![image-20221229111046694](imag/image-20221229111046694.png)

```go
package main
import (
	"fmt"
	"time"
)

func main() {
	// 获取当前时间
	now := time.Now()
	//Unix和UnixNano的使用
	fmt.Printf("unix时间戳=%v unixnano时间戳=%v\n", now.Unix(), now.UnixNano())
    //unix时间戳=1672282538 unixnano时间戳=1672282538068575000
}
```

可以用来统计时间

```go
package main
import (
	"fmt"
	"time"
	"strconv"
)

func test() {
	str := ""
	for i := 0; i < 100000; i++ {
		str += "hello" + strconv.Itoa(i)
	}
}

func main() {
	//在执行test前，先获取到当前的unix时间戳
	start := time.Now().Unix()
	test()
	end := time.Now().Unix()
	fmt.Printf("执行test()耗费时间为%v秒\n", end-start)//执行test()耗费时间为7秒
}
```

### 6.15 系统函数(内置函数builtin)

1 ) len：用来求长度，比如string、array、slice、map、channel

2 ) new：用来分配内存，主要用来分配值类型，比如int、float 32 ,struct返回的是指针

```go
package main
import (
	"fmt"
)

func main() {
	num1 := 100
	fmt.Printf("num1的类型%T , num1的值=%v , num1的地址%v\n", num1, num1, &num1)
    //num1的类型int , num1的值=100 , num1的地址0xc0000140c8
    
	num2 := new(int) // *int
	//num2的值 = 地址 0xc000014100 （这个地址是系统分配）
	//num2的地址%v = 地址 0xc000006030  (这个地址是系统分配)
	*num2  = 100
	fmt.Printf("num2的类型%T , num2的值=%v , num2的地址%v\n num2这个指针，指向的值=%v", 
		num2, num2, &num2, *num2)
    //num2的类型*int , num2的值=0xc000014100 , num2的地址0xc000006030  num2这个指针，指向的值=100
}
```

![image-20221229120441856](imag/image-20221229120441856.png)

3 ) make：用来分配内存，主要用来分配引用类型，比如channel、map、slice。

### 6.16 错误处理

```go
package main

import (
	"fmt"
)

func test() {
	num1 := 10
	num2 := 0
	res := num1 / num2
	fmt.Println("res=", res)
}

func main() {
	test()
	fmt.Println("main()下面的代码...")
}
//结果
//panic: runtime error: integer divide by zero
```

1 ) 在默认情况下，当发生错误后(panic)，程序就会退出（崩溃）

2 ) 如果我们希望：当发生错误后，可以捕获到错误，并进行处理，保证程序可以继续执行。还可以在捕获到错误后，给管理员一个提示(邮件,短信。。。）

**基本说明**

1 ) Go语言追求简洁优雅，所以，Go语言不支持传统的 `try-catch-finally` 这种处理。

2 ) Go中引入的处理方式为： defer , panic , recover

3 ) 这几个异常的使用场景可以这么简单描述：Go中可以抛出一个panic的异常，然后在defer中通过**recover捕获这个异常**，然后正常处理

```go
package main
import (
	"fmt"
	"time"
)

func test() {
	//使用defer + recover 来捕获和处理异常
	defer func() {
		err := recover()  // recover()内置函数，可以捕获到异常
		if err != nil {  // 说明捕获到错误
			fmt.Println("err=", err)
		}
	}()
	num1 := 10
	num2 := 0
	res := num1 / num2
	fmt.Println("res=", res)
}

func main() {
	test()
	for {
		fmt.Println("main()下面的代码...")
		time.Sleep(time.Second)
	}
}
/*结果
err= runtime error: integer divide by zero
发送邮件给admin@sohu.com~
main()下面的代码...
*/
```

**自定义错误**

Go程序中，也支持自定义错误， 使用errors.New 和 panic 内置函数。

1 ) errors.New(“错误说明”), 会返回一个error类型的值，表示一个错误

2 ) panic内置函数 ,接收一个interface{}类型的值（也就是任何值了）作为参数。可以接收error类型的变量，输出错误信息，并退出程序.

```go
package main
import (
	"fmt"
	_ "time"
	"errors"
)
//函数去读取以配置文件init.conf的信息
//如果文件名传入不正确，我们就返回一个自定义的错误
func readConf(name string) (err error) {
	if name == "config.ini" {
		//读取...
		return nil
	} else {
		//返回一个自定义错误
		return errors.New("读取文件错误..")
	}
}

func test02() {
	err := readConf("config2.ini")
	if err != nil {
		//如果读取文件发送错误，就输出这个错误，并终止程序
		panic(err)
	}
	fmt.Println("test02()继续执行....")
}
	
func main() {
	test02()
	fmt.Println("main()下面的代码...")
}
//--------------------------------
//正确输出
test02()继续执行....
main()下面的代码...

//错误输出
panic: 读取文件错误..                                             
                                                                  
goroutine 1 [running]:                                            
main.test02()                                                     
        E:/goprojects/src/go_code/chapter06/error/main.go:42 +0x49
main.main()                                                       
        E:/goprojects/src/go_code/chapter06/error/main.go:58 +0x19

```



## 七、数组与切片

数组可以存放多个同一类型数据。数组也是一种数据类型，在Go中，数组是值类型。

### 7.1 数组的定义

```go
var 数组名 [数组大小]数据类型
var a [5]int// 数组名 [长度]数据类型
赋初值 a[0]= 1 a[1]= 30 
```

### 7.2 数组内存布局,地址连续

![image-20221229142357572](imag/image-20221229142357572.png)

1 ) 数组的地址可以通过数组名来获取 &intArr

2 ) 数组的第一个元素的地址，就是数组的首地址

3 ) 数组的各个元素的地址间隔是依据数组的类型决定，比如int 64 - > 8， int 32 - > 4

### 7.3 初始化数组的方式

```go
package main
import (
	"fmt"
)

func main() {
	//初始化数组的方式
	var numArr01 [3]int = [3]int{1, 2, 3}
	fmt.Println("numArr01=", numArr01)

	var numArr02 = [3]int{5, 6, 7}
	fmt.Println("numArr02=", numArr02)
    
	//这里的 [...] 是规定的写法由go推导数组大小
	var numArr03 = [...]int{8, 9, 10}
	fmt.Println("numArr03=", numArr03)

	var numArr04 = [...]int{1: 800, 0: 900, 2:999}
	fmt.Println("numArr04=", numArr04)//numArr04= [900 800 999]
    
    f := [...] int{0: 1, 4: 1, 9: 1} // [1 0 0 0 1 0 0 0 0 1]
  	fmt.Println(f)

    e := [5] int{4: 100} // [0 0 0 0 100]
    fmt.Println(e)
    
    //类型推导:=
	strArr05 := [...]string{1: "tom", 0: "jack", 2:"mary"}
	fmt.Println("strArr05=", strArr05)//strArr05= [jack tom mary]
}
```

### 7.4 数组遍历

1）方式1：for（；；；）遍历数组

```go
package main

import (
	"fmt"
)

func main() {
	//for-range遍历数组
	heroes := [...]string{"宋江", "吴用", "卢俊义"}

	for i := 0; i < len(heroes); i++ {
		fmt.Printf("i=%v v=%v\n", i, heroes[i]) //i=0 v=宋江
	}
}
```

2）方式2：for-range结构遍历

```go
package main

import (
	"fmt"
)

func main() {
	//for-range遍历数组
	heroes := [...]string{"宋江", "吴用", "卢俊义"}

	for i, v := range heroes {//index和value的名称不是固定的。可以自己改变
		fmt.Printf("i=%v v=%v\n", i, v) //i=0 v=宋江
		fmt.Printf("heroes[%d]=%v\n", i, heroes[i])  //heroes[0]=宋江
	}

	for _, v := range heroes { 
		fmt.Printf("元素的值=%v\n", v) //元素的值=宋江
	}
}
```

### 7.5 数组使用注意事项
1 ) 数组是多个相同类型数据的组合，一个数组一旦声明/定义了，其长度是固定的，不能动态变化。否则报越界

2 ) 数组中的元素可以是任何数据类型，包括值类型和引用类型，但是不能混用。

3 ) 数组创建后，如果没有赋值，有默认值(零值)

- 数值类型数组：默认值为 0
- 字符串数组： 默认值为 “”
- bool数组： 默认值为 false

5 ) 使用数组的步骤:

- 1.声明数组并开辟空间 
- 2.给数组各个元素赋值(默认零值) 
- 3.使用数组

6 ) Go的数组属值类型，在默认情况下是值传递，因此会进行值拷贝。数组间不会相互影响

7 ) 如想在其它函数中，去修改原来的数组，可以使用引用传递(指针方式)

```go
package main
import (
	"fmt"
)

//函数
func test02(arr *[3]int) {
	fmt.Printf("arr指针的地址=%p", &arr)//arr指针的地址=0xc000006030
	(*arr)[0] = 88 //!!
} 


func main() {	
	arr := [3]int{11, 22, 33}
	fmt.Printf("arr 的地址=%p", &arr)//arr 的地址=0xc00000c150
	test02(&arr)
	fmt.Println("main arr=", arr)//arr= [88 22 33]
}	
```

8 ) 长度是数组类型的一部分，在传递函数参数时需要考虑数组的长度

```go
/题1
package main
import (
	"fmt"
)

//默认值拷贝
func modify(arr []int) {
	arr[0] = 100
    fmt.Println("modify的arr",arr)
} 

func main() {	
	var arr = [...]int{1,2,3}
	modify(arr)
}	
//编译错误，因为不能把[3]int 传递给[]int
```

```go
//题2
package main
import (
	"fmt"
)

//默认值拷贝
func modify(arr [4]int) {
	arr[0] = 100
    fmt.Println("modify的arr",arr)
} 

func main() {	
	var arr = [...]int{1,2,3}
	modify(arr)
}	
//编译错误，因为不能把[3]int 传递给[4]int
```

### 7.6 切片的定义
1 ) 切片的英文是slice

2 ) 切片是数组的一个引用，因此切片是**引用类型**，在进行传递时，遵守引用传递的机制。

3 ) 切片的**使用和数组类似**，遍历切片、访问切片的元素和求切片长度len(slice)都一样。

4 ) 切片的长度是可以变化的，因此切片是一个可以**动态变化数组**。

5 ) 切片定义的基本语法:

```go
var 切片名 []类型
//比如：vara[]int
```

```go
package main
import (
	"fmt"
)

func main() {
	//演示切片的基本使用
	var intArr [5]int = [...]int{1, 22, 33, 66, 99}
	//声明/定义一个切片
	//1. slice 就是切片名
	//2. intArr[1:3] 表示 slice 引用到intArr这个数组 
	//3. 引用intArr数组的起始下标为 1 , 最后的下标为3(但是不包含3)    
	slice := intArr[1:3] 
	fmt.Println("intArr=", intArr) //[1 22 33 66 99]
	fmt.Println("slice 的元素是 =", slice) //  22, 33
	fmt.Println("slice 的元素个数 =", len(slice)) // 2
	fmt.Println("slice 的容量 =", cap(slice)) //4 切片的容量是可以动态变化  
}
```



## 八、排序与查找



## 九、map

### 9.1 map概述
- map是key-value数据结构，又称为字段或者关联数组。类似其它编程语言的集合，在编程中是经常使用到

- 基本语法

> var map 变量名 map[keytype]valuetype

- golang中的map的 key 可以是很多种类型，比如 bool, 数字，string，指针，channel，还可以是只包含前面几个类型的接口，结构体， 数组。通常 key 为 int，string。**注意:**slice，map还有function不可以，因为这几个没法用 ==来判断

- valuetype的类型和key基本一样。通常为: 数字(整数，浮点数)，string，map，struct

### 9.2 map声明
map声明：

```go
var a map[string]string
var a map[string]int
var a map[int]string
var a map[string]map[string]string
```

**声明是不会分配内存的，初始化需要make ，分配内存后才能赋值和使用。**

```go
package main
import (
	"fmt"
)

func main() {
	//map的声明和注意事项 
	var a map[string]string
	//在使用map前，需要先make , make的作用就是给map分配数据空间
	a = make(map[string]string, 10)
	a["no1"] = "宋江" 
	a["no2"] = "吴用" 
	a["no1"] = "武松" 
	a["no3"] = "吴用" 
	fmt.Println(a)//map[no1:武松 no2:吴用 no3:吴用]
}
```

1 ) map在使用前一定要make

2 ) map的key是不能重复，如果重复了，则以最后这个key-value为准

3 ) map的value是可以相同的.

4 ) map的 key-value是无序

5 ) make内置函数数目

![image-20221229151531480](imag/image-20221229151531480.png)

## 9.3 map的使用

方式 1

```go
package main
import (
	"fmt"
)

func main() {
	//第一种使用方式
	var a map[string]string
	//在使用map前，需要先make , make的作用就是给map分配数据空间
	a = make(map[string]string, 10)
	a["no1"] = "宋江" //ok?
	a["no2"] = "吴用" //ok?
	a["no1"] = "武松" //ok?
	a["no3"] = "吴用" //ok?
	fmt.Println(a)

}
```

方式 2

```go
package main
import (
	"fmt"
)

func main() {
	//第二种方式
	cities := make(map[string]string)
	cities["no1"] = "北京"
	cities["no2"] = "天津"
	cities["no3"] = "上海"
	fmt.Println(cities)
}
```

方式 3

```go
package main
import (
	"fmt"
)

func main() {
	//第三种方式
	heroes := map[string]string{
		"hero1" : "宋江",
		"hero2" : "卢俊义",
		"hero3" : "吴用",
	}
	heroes["hero4"] = "林冲"
	fmt.Println("heroes=", heroes)
}
```

9.4 map操作

- map增改

  ```go
  map[“key”]=value//如果 key 还没有，就是增加，如果 key 存在就是修改。
  ```

- map删除：
  说明：delete(map，“key”) ，delete是一个内置函数，如果key存在，就删除该key-value,如果key不存在，不操作，但是也不会报错

![image-20221229152017254](imag/image-20221229152017254.png)



```go
package main
import (
	"fmt"
)

func main() {
	//第二种方式
	cities := make(map[string]string)
	cities["no1"] = "北京"
	cities["no2"] = "天津"
	cities["no3"] = "上海"
	fmt.Println(cities) // map[no1:北京 no2:天津 no3:上海]

	//删除
	delete(cities, "no1")
	fmt.Println(cities) // map[no2:天津 no3:上海]
	//当delete指定的key不存在时，删除不会操作，也不会报错
	delete(cities, "no4") 
	fmt.Println(cities) // map[no2:天津 no3:上海]
}	
```

如果我们要删除map的**所有key**,没有一个专门的方法一次删除，可以遍历一下key，逐个删除或者 **map=make(…)，make一个新的，让原来的成为垃圾，被gc回收**

```go
package main
import (
	"fmt"
)

func main() {
	//第二种方式
	cities := make(map[string]string)
	cities["no1"] = "北京"
	cities["no2"] = "天津"
	cities["no3"] = "上海"
	fmt.Println(cities)

	//如果希望一次性删除所有的key
	//1. 遍历所有的key,如何逐一删除 [遍历]
	//2. 直接make一个新的空间
	cities = make(map[string]string)
	fmt.Println(cities)
}

```

- map 查找

```go
package main
import (
	"fmt"
)

func main() {
	//第二种方式
	cities := make(map[string]string)
	cities["no1"] = "北京"
	cities["no2"] = "天津"
	cities["no3"] = "上海"
	fmt.Println(cities)

	//演示map的查找
	val, ok := cities["no2"]
	if ok {
		fmt.Printf("有no1 key 值为%v\n", val)//有no1 key 值为天津
	} else {
		fmt.Printf("没有no1 key\n")
	}
}
```

- map遍历

map的遍历使用 **for-range** 的结构遍历

map的长度：len()

```go
package main
import (
	"fmt"
)

func main() {
	//使用for-range遍历map
	//第二种方式
	cities := make(map[string]string)
	cities["no1"] = "北京"
	cities["no2"] = "天津"
	cities["no3"] = "上海"
	
	for k, v := range cities {
		fmt.Printf("k=%v v=%v\n", k, v)  //k=no1 v=北京
	}

	fmt.Println("cities 有", len(cities), " 对 key-value") //cities 有 3  对 key-value

	//使用for-range遍历一个结构比较复杂的map
	studentmap := make(map[string]map[string]string)
	
	studentmap["stu01"] =  make(map[string]string, 3)
	studentmap["stu01"]["name"] = "tom"
	studentmap["stu01"]["sex"] = "男"
	studentmap["stu01"]["address"] = "北京长安街~"

	studentmap["stu02"] =  make(map[string]string, 3) //这句话不能少!!
	studentmap["stu02"]["name"] = "mary"
	studentmap["stu02"]["sex"] = "女"
	studentmap["stu02"]["address"] = "上海黄浦江~"

    /*
    k1= stu01                         
         k2=name v2=tom           
         k2=sex v2=男             
         k2=address v2=北京长安街~

    */
	for k1, v1 := range studentmap {
		fmt.Println("k1=", k1)
		for k2, v2 := range v1 {
				fmt.Printf("\t k2=%v v2=%v\n", k2, v2)
		}
		fmt.Println()
	}
}
```



## 十、面向对象编程



## 十一、文件操作



## 十二、单元测试



## 十三、goroutine和channel



## 十四、反射



## 十五、TCP编程





## 参考

[](https://blog.csdn.net/zhaicheng55/article/details/127978156)
