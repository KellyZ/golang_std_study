###变量  
- 变量初始化  
	`var v1 int = 0  or  var v2 = 0`  
	`v3 := 10`
- 变量赋值(多重赋值--多重返回值) `i,j = j,i`  
- 枚举/常量关键字const，预定义常量 `true false iota`  

  
###类型
- 基础类型  
> 
	**布尔类型**：bool  
	**整型**：int8、byte、uint8、int16、uint16、int32、uint32、int64、uint64、int、uint、uintptr  
	**浮点型**(*IEEE 754标准)：float32、float64(注意没有double)  
	**复数类型**：complex64、complex128  
	**字符串**：string  
	**字符类型**：rune  
	**错误类型**：error  
- 复合类型  
> 
	**指针**：pointer  
	**数组**：array(值类型，在赋值和作为参数传递时都将产生一次复制动作)  
	**切片**：slice(引用类型)  
	**字典**：map  
	**通道**：chan  
	**结构体**：struct  
	**接口**：interface  
  
- 浮点数本身不精确，建议用以下方式比较：  
```
import "math"

func IsEqual(f1,f2,p float64) bool{
	return math.Fdim(f1,f2) < p
}
```

  
###运算符
和其他语言基本类似，没有特殊的  
（算术运算：+、-、*、/、%）  
（条件运算：>、<、==、>=、<=、!=）  
（位运算：<<、>>、^、&、|）  

  
###字符串  
- 字符串的编码转换是处理文本文档非常常见的需求，不过可惜的是Go语言仅支持UTF-8和Unicode编码。对于其他编码，Go语言标准库并没有内置的编码转换支持。开源项目可以支持https://github.com/xushiwei/go-iconv  
- 在Go语言中支持两个类型字符，一个是byte（实际是uint8的别名），代表UTF-8字符串的单个字节的值；另一个是rune，代表单个Unicode字符（关于rune相关的操作可查阅unicode和unicode/utf8包，unicode/utf8包提供了unicode和utf8之间的转换）;  
- 字符串遍历  
	`for i:=0;i<len(str);i++{ch := str[i] (此处获取的是每个字节)}`  
	`for i,ch := range str{ (此处的ch为rune) }`  
