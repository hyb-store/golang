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
	fmt.Println("res1=", res1)
}
```



## 八、排序和查找



## 九、map



## 十、面向对象编程



## 十一、文件操作

