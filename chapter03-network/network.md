###Socket
- func Dial(net, addr string) (Conn,error)  


###HTTP
- http.Get/Post/Head/Do  
- http.Client  
	三个公开数据成员可定制：  
	Transport RoundTripper  
	CheckRedirect func(req *Request,via []*Request) error  
	Jar CookieJar  
- http.ListenAndServe(addr string,handler Handler) error  
	handler默认注入http.DefaultServeMux  
	更多控制可以自定义 `s := http.Server; s.ListenAndServe()`  
- (https) http.ListenAndServeTLS(addr string,certFile string,keyFile string, handler Handler)  


###RPC
- RPC server register method定义：
	`func (t *T) MethodName(argType T1, replyType *T2) error  
- 服务器端 `rpc.ServeConn`  
- 客户端  
	`rpc.Dial() or rpc.DialHttp()`  
	`rpc.Call()同步 or rpc.Go()异步`  
- 序列化编码解码默认为gob，可实现ClientCodec和ServerCodecs进行自定义  



###JSON编码转化
* 布尔值转化为JSON后还是布尔类型。  
* 浮点数和整型会被转化为JSON里边的常规数字。  
* 字符串将以UTF-8编码转化输出为Unicode字符集的字符串，特殊字符比如<将会被转义为\u003c。  
* 数组和切片会转化为JSON里边的数组，但[]byte类型的值将会被转化为Base64 编码后的字符串，slice类型的零值会被转化为 null。  
* 结构体会转化为JSON对象，并且只有结构体里边以大写字母开头的可被导出的字段才会被转化输出，而这些可导出的字段会作为JSON对象的字符串索引。  
* 转化一个map类型的数据结构时，该数据的类型必须是  map[string]T（T可以是encoding/json 包支持的任意数据类型）。  


###JSON解码转换
* JSON中的布尔值将会转换为Go中的bool类型；  
* 数值会被转换为Go中的float64类型；  
* 字符串转换后还是string类型；  
* JSON数组会转换为[]interface{}类型；  
* JSON对象会转换为map[string]interface{}类型；  
* null值会转换为nil。  


###JSON的流式读写
- 提供Decoder和Encoder两个类型  
	`func NewDecoder(r io.Reader) *Decoder`  
	`func NewEncoder(w io.Writer) *Encoder`  

```
package main 
import( 
	"encoding/json" 
	"log" 
	"os" 
)

func main() { 
	dec := json.NewDecoder(os.Stdin) 
	enc := json.NewEncoder(os.Stdout) 
	for{ 
 		var v map[string] interface{} 
 		if err := dec.Decode(&v); err != nil{ 
			log.Println(err) 
			return
		} 
 		fork := range v { 
			if k != "Title" { 
				v[k] = nil, false
			}	 
		} 
 		if err := enc.Encode(&v); err != nil{ 
			log.Println(err) 
		} 
	} 
}
```

###网站开发
