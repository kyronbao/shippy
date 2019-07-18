Golang微服务教程
https://wuyin.io/2018/05/10/microservices-part-1-introduction-and-consignment-service/

实际项目中proto目录可以单独独立出来，然后service和cli来import

https://ewanvalentine.io/microservices-in-golang-part-2/  
## 分支v2  
### 标签v2-2: 使用go-micro替代rpc, 使用docker  
  
  和源教程对比的修改记录  
  
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

  在独立的容器部署可以参考  
    - https://github.com/kyronbao/shippy-service-consignment  
    - https://github.com/kyronbao/shippy-cli-consignment  
    
### 标签v2-3  :添加vessel服务
  判断vessel轮船是否有可用的，然后来发货  
    （测试：调整consignment.json的weight大于200000，可以发现无法发货） 
    
## 分支v3
  调试记录  
      stat ./vessel-service: no such file or directory    
  原因：  
    本地运行go build后生成的vessel-service文件无法运行，需要运行sudo make build (参考里面的命令)  
    当docker-compose up 后创建的container会缓存  
  解决：  
    删除vessel相关的imges  
      sudo docker rmi xxx  
    然后重新启动docker-compose up 
    
  测试
     sudo docker-compose up consignment-service
  报错
  
     consignment-service_1  | 2019/07/18 14:39:59 error parsing uri: scheme must be "mongodb" or "mongodb+srv"
     consignment-service_1  | panic: error parsing uri: scheme must be "mongodb" or "mongodb+srv"
     consignment-service_1  | 
     consignment-service_1  | goroutine 1 [running]:
     consignment-service_1  | log.Panic(0xc000195f78, 0x1, 0x1)
     consignment-service_1  |        /usr/local/go/src/log/log.go:333 +0xac
     consignment-service_1  | main.main()
     consignment-service_1  |        /home/kyron/demo/shippy/consignment-service/main.go:33 +0x15c
     shippy_consignment-service_1 exited with code 2

  暂停开发。。。（待续）  
  
  
  



