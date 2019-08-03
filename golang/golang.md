[GO代码规范](https://github.com/golang/go/wiki/CodeReviewComments)
[GO错误处理](https://blog.golang.org/error-handling-and-go)
[GO精选代码库](https://github.com/avelino/awesome-go)
关于大对象
在cpu内部，有二级缓存，会一次缓存很多数据，像[]user这样的数据类型，会被直接缓存在cpu二级缓存里


先对返回值进行赋值：MOVQ $0xc8, 0x30(SP)
执行 defer 语句: CALL runtime.deferreturn(SB)
执行RET指令(函数返回): RET
- - - - - 
先panic 再defer