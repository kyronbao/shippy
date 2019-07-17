Golang微服务教程
https://wuyin.io/2018/05/10/microservices-part-1-introduction-and-consignment-service/

实际项目中proto目录可以单独独立出来，然后service和cli来import

https://ewanvalentine.io/microservices-in-golang-part-2/  
## 分支v2  
  标签v2-1：使用go-micro替代rpc, 使用docker  
  
  修改记录  
    无法生成micro版的proto  
      解决：  
      修改Makefile文件：  
        修改protoc命令，参考https://github.com/micro/protoc-gen-micro  
        添加GOPROXY变量   
    sudo make build 生成文件后 sudo make run 报错  
      standard_init_linux.go:211: exec user process caused "no such file or directory"  
      参考：  
        https://my.oschina.net/zhizhisoft/blog/2966531  
      解决  
        参考CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main . 修改相关命令  
  测试运行方法：  
      在service目录：sudo make build && sudo make run  
      cli目录同理  
   
## 下一版本
  https://github.com/kyronbao/shippy-service-consignment
  https://github.com/kyronbao/shippy-cli-consignment
  



