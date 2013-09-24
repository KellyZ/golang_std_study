###类型映射
- 在跨语言交互中，比较复杂的问题有两个：类型映射以及跨越调用边界传递指针所带来的对象生命周期和内存管理的问题。  

> 
对于C语言的原生类型，Cgo都会将其映射为Go语言中的类型：C.char和C.schar（对应于C语言中的signed char）、C.uchar（对应于C语言中的unsigned char）、C.short和C.ushort（对应于unsigned short）、C.int和C.uint（对应于unsigned int）、C.long和C.ulong（对应于unsigned long）、C.longlong（对应于C语言中的long long）、C.ulonglong（对应于C语言中的unsigned long long类型）以及C.float和C.double。C语言中的void*指针类型在Go语言中则用特殊的unsafe.Pointer类型来对应。  
C语言中的struct、union和enum类型，对应到Go语言中都会变成带这样前缀的类型名称：struct_、union_和enum_。比如一个在C语言中叫做person的struct会被Cgo翻译为
C.struct_person。  
如果C语言中的类型名称或变量名称与Go语言的关键字相同，Cgo会自动给这些名字加上下划线前缀。  

- 字符串映射:C.CString、C.GoString和C.GoStringN  
	由于C.CString的内存管理方式与Go语言自身的内存管理方式不兼容，因此在使用完后必须显示释放调用C.CString所生成的内存块。  

```
var gostr string
cstr := C.CString(gostr)
defer C.free(unsafe.Pointer(cstr))
```

- #cgo指定第三方库和编译选项  

```
// #cgo CFLAGS: -DPNG_DEBUG=1
// #cgo linux CFLAGS: -DLINUX=1
// #cgo LDFLAGS: -lpng
// #include <png.h>
import "C"
```

- 函数调用:传递数组时需显示指定第一个元素的地址  
	`n,err := C.f(&array[0])`

