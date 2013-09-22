###函数
- 定义 

```
func Add(args ...int) (ret int ,err error){
	var ret int = 0
	for _,arg := range args {
		ret += arg
	}
	return ret,nil
}
```
- 匿名函数：没有函数名，可将函数赋值给变量  
- 闭包：可访问内部变量和同作用域的外部变量  


###错误处理
- error类型  
- defer  
- panic()和recover() (recover常和defer一起用)  


###类型
- 类型定义  
- 类型转换  
