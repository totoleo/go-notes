go 项目开发规范
1. 使用 go module 管理依赖；
2. 使用 CI/CD 进行打包、测试和部署；

项目结构
```
 -- biz  
  |-- user  
  | |- service.go  
  | |- api.go  
  | |- model.go  
  |  
  |-- middleware  
  | |- qps.go  
  | |- cors.go  
  | |- auth.go  
  |  
  |-- ...  
  |  
 -- config  
  |- app.go  
  |- ...  
 -- conf  
  |- app.yaml  
  |-   
 - routes.go  
 - server.go  
 - go.mod  
 - go.sum  
  ```
编码规范
1. 使用`驼峰式`命名
2. 局部变量，首字母小写
3. context 应该出现在函数的第一个参数位置
4. 如果需要返回错误，应该式函数的最后一个返回值
5. 避免在返回错误的同时，记录日志；相反，应该在错误中包含足够的上下文信息
6. 

容易出错的地方：
1. 避免引用循环变量，如 `for index,item := range slice ` 中的 index，和 item 的变量的内存会复用，直接引用他们的指针，会造成最后只获取到 slice 最后的值
2. defer 按值调用，也就是说类似 `defer time.Since(time.Now())`  的调用，获取的时间不是函数的进入和返回的差值，而是 defer 声明处的时间
3. json.Decoder 默认对长整型做浮点处理，需要使用 UseNumber 特别声明
4. goroutine 的函数，需要配合 defer 增加 recover，否则在函数内发生 panic 会造成程序异常退出。
  
