###函数
- 定义 

```
func Add(args ...int) (ret int ,err error){
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
- 值语义和引用语义  
	数组是很纯粹的值类型  
	引用语义类型：切片、map、channel、接口  
- 匿名组合  
- 接口赋值  

```
Go语言可以根据下面的函数：
func (a Integer) Less(b Integer) bool
自动生成一个新的Less()方法:
func (a *Integer) Less(b Integer) bool{
	return (*a).Less(b)
}
不能反向生成，因为值类型对外部实际要操作的对象并无影响。
```
- 接口查询 `v,ok := a.(*File)`  
- 类型查询 `v := a.(type) 返回类型如int、string`  
- 任何对象实例都满足空接口interface{}  
- 类型别名 type Integer int 其实类似 type name struct  


###并发
- 并发模型：多进程、多线程、基于回调的非阻塞IO(Node.js)、协程(轻量级线程，语言层面支持)  
- 并发通信：共享数据和消息  
- 缓冲channel,单向channel, select  
- 并发通信超时  

```
timeout := make(chan bool,1)
go func(){
	time.Sleep(1e9)
	timeout <- true
}()

select {
	case <-ch:
		//deal with data read from ch
	case <-timeout:
		//timeout
}
```
