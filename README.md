# spring-native-demo
使用Spring-Native构建本地Docker镜像的一个示例



本机构建包构建Spring Boot本机应用程序的实用概述。

# 构建native原生应用程序
```
$ mvn spring-boot:build-image
```

> 在本机编译期间，您将看到很多警告：无法注册反射元数据消息。

这将创建一个Linux容器，以使用GraalVM本机映像编译器构建本机应用程序。默认情况下，容器映像安装在本地。

# 运行原生应用程序

要运行应用程序，您可以使用docker的常用方式：
```
$ docker run --rm -p 8080:8080 rest-service-complete:0.0.1-SNAPSHOT
```

如果你喜欢docker compose，你可以编写docker compose.yml位于项目的根目录下，包含以下内容：
```
version: '3.1'
services:
  rest-service:
    image: rest-service-complete:0.0.1-SNAPSHOT
    ports:
      - "8080:8080"
```
然后运行
```
$ docker-compose up
```

启动时间应该小于100ms，而在JVM上启动应用程序的时间大约为1500ms。
现在服务已经启动，请访问localhost:8080/greeting，您应该会看到
```
{"id":1,"content":"Hello, World!"}
```


