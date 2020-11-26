# GinWeb框架

<img align="right" width="159px" src="https://raw.githubusercontent.com/gin-gonic/logo/master/color.png">

[![Build Status](https://travis-ci.org/gin-gonic/gin.svg)](https://travis-ci.org/gin-gonic/gin)
[![codecov](https://codecov.io/gh/gin-gonic/gin/branch/master/graph/badge.svg)](https://codecov.io/gh/gin-gonic/gin)
[![Go Report Card](https://goreportcard.com/badge/github.com/gin-gonic/gin)](https://goreportcard.com/report/github.com/gin-gonic/gin)
[![GoDoc](https://pkg.go.dev/badge/github.com/gin-gonic/gin?status.svg)](https://pkg.go.dev/github.com/gin-gonic/gin?tab=doc)
[![Join the chat at https://gitter.im/gin-gonic/gin](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/gin-gonic/gin?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![Sourcegraph](https://sourcegraph.com/github.com/gin-gonic/gin/-/badge.svg)](https://sourcegraph.com/github.com/gin-gonic/gin?badge)
[![Open Source Helpers](https://www.codetriage.com/gin-gonic/gin/badges/users.svg)](https://www.codetriage.com/gin-gonic/gin)
[![Release](https://img.shields.io/github/release/gin-gonic/gin.svg?style=flat-square)](https://github.com/gin-gonic/gin/releases)
[![TODOs](https://badgen.net/https/api.tickgit.com/badgen/github.com/gin-gonic/gin)](https://www.tickgit.com/browse?repo=github.com/gin-gonic/gin)

## 简介

Gin是Golang写的Web框架, 功能类似另一个Go框架Martini[Martini](https://github.com/go-martini/martini)(暂停维护), Gin内部使用定制版本的[httprouter](https://github.com/julienschmidt/httprouter)(一款轻量级高性能HTTP请求路由器,或叫多路复用器), 速度是Martini的40倍, Gin拥有强大的性能,高效率,以及可扩展性, 所以赶快用起来吧!



## 云原生

更多云原生相关技术干货, 欢迎大家关注我的微信公众号:**云原生云**

![云原生云二维码](img/云原生云二维码大.gif)

## 内容

- [GinWeb框架](#GinWeb框架)
  - [内容](#内容)
  - [安装](#installation)
  - [快速开始](#quick-start)
  - [基准测试](#基准测试)
  - [Gin v1稳定版](#Gin v1稳定版)
  - [使用jsoniter编译](#使用jsoniter编译)
  - [API 示例](#API 示例)
    - [使用GET, POST, PUT, PATCH, DELETE, OPTIONS](#使用GET, POST, PUT, PATCH, DELETE, OPTIONS)
    - [获取请求中的路径参数](#获取请求中的路径参数)
    - [获取查询字符串参数](#获取查询字符串参数)
    - [获取Multipart/Urlencoded类型表单](#获取Multipart/Urlencoded类型表单)
    - [另一个示例: 查询参数 + Post表单](#另一个示例: 查询参数 + Post表单)
    - [以Map映射作为查询字符串或Post表单参数](#以Map映射作为查询字符串或Post表单参数)
    - [上传文件](#上传文件)
      - [单个文件](#单个文件)
      - [多个文件](#多个文件)
    - [路由分组](#路由分组)
    - [Gin引擎初始化(不带中间件或使用日志和异常恢复中间件)](#Gin引擎初始化(不带中间件或使用日志和异常恢复中间件))
    - [使用中间件](#使用中间件)
    - [自定义程序崩溃后的处理方式(邮件/微信/短信等告警)](#自定义程序崩溃后的处理方式(邮件/微信/短信等告警))
    - [怎样记录日志到文件](#怎样记录日志到文件)
    - [自定义日志格式](#自定义日志格式)
    - [控制日志输出颜色](#控制日志输出颜色)
    - [模型绑定和验证](#模型绑定和验证)
    - [自定义验证器](#自定义验证器)
    - [只绑定查询字符串](#只绑定查询字符串)
    - [绑定查询字符串或Post表单数据](#绑定查询字符串或Post表单数据)
    - [绑定URI](#绑定URI)
    - [绑定请求头](#绑定请求头)
    - [绑定HTML复选框](#绑定HTML复选框)
    - [绑定Multipart/Urlencoded类型的表单](#绑定Multipart/Urlencoded类型的表单)
    - [XML, JSON, YAML and ProtoBuf rendering](#xml-json-yaml-and-protobuf-rendering)
      - [SecureJSON](#securejson)
      - [JSONP](#jsonp)
      - [AsciiJSON](#asciijson)
      - [PureJSON](#purejson)
    - [Serving static files](#serving-static-files)
    - [Serving data from file](#serving-data-from-file)
    - [Serving data from reader](#serving-data-from-reader)
    - [HTML rendering](#html-rendering)
      - [Custom Template renderer](#custom-template-renderer)
      - [Custom Delimiters](#custom-delimiters)
      - [Custom Template Funcs](#custom-template-funcs)
    - [Multitemplate](#multitemplate)
    - [Redirects](#redirects)
    - [Custom Middleware](#custom-middleware)
    - [Using BasicAuth() middleware](#using-basicauth-middleware)
    - [Goroutines inside a middleware](#goroutines-inside-a-middleware)
    - [Custom HTTP configuration](#custom-http-configuration)
    - [Support Let's Encrypt](#support-lets-encrypt)
    - [Run multiple service using Gin](#run-multiple-service-using-gin)
    - [Graceful shutdown or restart](#graceful-shutdown-or-restart)
      - [Third-party packages](#third-party-packages)
      - [Manually](#manually)
    - [Build a single binary with templates](#build-a-single-binary-with-templates)
    - [Bind form-data request with custom struct](#bind-form-data-request-with-custom-struct)
    - [Try to bind body into different structs](#try-to-bind-body-into-different-structs)
    - [http2 server push](#http2-server-push)
    - [Define format for the log of routes](#define-format-for-the-log-of-routes)
    - [Set and get a cookie](#set-and-get-a-cookie)
  - [Testing](#testing)
  - [Users](#users)

## 安装

为了安装Gin包, 你需要先安装Go, 并且设置Go工作空间.

1. 首先参考[Go官方文档](https://golang.org/)安装Go(版本要求:**Go1.12**及以上), 然后执行以下命令安装Gin.

```sh
$ go get -u github.com/gin-gonic/gin
```

2. 导入gin包:

```go
import "github.com/gin-gonic/gin"
```

3. (可选)导入net/http包, 如果你要使用其中的常量,比如http.StatusOK,则需要导入

```go
import "net/http"
```

## 快速开始

```sh
编写main.go,写入以下代码并执行go run main.go, 访问http://localhost:8080/ping, 就可以得到响应消息{"message": "pong"}
```

```go
package main
​
import "github.com/gin-gonic/gin"
​
func main() {
  r := gin.Default()  //创建默认Gin引擎Engine,内部默认开启了日志和异常恢复中间件
  r.GET("/ping", func(c *gin.Context) {
    c.JSON(200, gin.H{
      "message": "pong",
    })
  })
  r.Run() //默认在localhost:8080监听
}
```

## 基准测试

Gin 使用定制版本的[HttpRouter](https://github.com/julienschmidt/httprouter)

[查看所有基准测试](/BENCHMARKS.md)

| Benchmark name                 |       (1) |             (2) |          (3) |             (4) |
| ------------------------------ | ---------:| ---------------:| ------------:| ---------------:|
| BenchmarkGin_GithubAll         | **43550** | **27364 ns/op** |   **0 B/op** | **0 allocs/op** |
| BenchmarkAce_GithubAll         |     40543 |     29670 ns/op |       0 B/op |     0 allocs/op |
| BenchmarkAero_GithubAll        |     57632 |     20648 ns/op |       0 B/op |     0 allocs/op |
| BenchmarkBear_GithubAll        |      9234 |    216179 ns/op |   86448 B/op |   943 allocs/op |
| BenchmarkBeego_GithubAll       |      7407 |    243496 ns/op |   71456 B/op |   609 allocs/op |
| BenchmarkBone_GithubAll        |       420 |   2922835 ns/op |  720160 B/op |  8620 allocs/op |
| BenchmarkChi_GithubAll         |      7620 |    238331 ns/op |   87696 B/op |   609 allocs/op |
| BenchmarkDenco_GithubAll       |     18355 |     64494 ns/op |   20224 B/op |   167 allocs/op |
| BenchmarkEcho_GithubAll        |     31251 |     38479 ns/op |       0 B/op |     0 allocs/op |
| BenchmarkGocraftWeb_GithubAll  |      4117 |    300062 ns/op |  131656 B/op |  1686 allocs/op |
| BenchmarkGoji_GithubAll        |      3274 |    416158 ns/op |   56112 B/op |   334 allocs/op |
| BenchmarkGojiv2_GithubAll      |      1402 |    870518 ns/op |  352720 B/op |  4321 allocs/op |
| BenchmarkGoJsonRest_GithubAll  |      2976 |    401507 ns/op |  134371 B/op |  2737 allocs/op |
| BenchmarkGoRestful_GithubAll   |       410 |   2913158 ns/op |  910144 B/op |  2938 allocs/op |
| BenchmarkGorillaMux_GithubAll  |       346 |   3384987 ns/op |  251650 B/op |  1994 allocs/op |
| BenchmarkGowwwRouter_GithubAll |     10000 |    143025 ns/op |   72144 B/op |   501 allocs/op |
| BenchmarkHttpRouter_GithubAll  |     55938 |     21360 ns/op |       0 B/op |     0 allocs/op |
| BenchmarkHttpTreeMux_GithubAll |     10000 |    153944 ns/op |   65856 B/op |   671 allocs/op |
| BenchmarkKocha_GithubAll       |     10000 |    106315 ns/op |   23304 B/op |   843 allocs/op |
| BenchmarkLARS_GithubAll        |     47779 |     25084 ns/op |       0 B/op |     0 allocs/op |
| BenchmarkMacaron_GithubAll     |      3266 |    371907 ns/op |  149409 B/op |  1624 allocs/op |
| BenchmarkMartini_GithubAll     |       331 |   3444706 ns/op |  226551 B/op |  2325 allocs/op |
| BenchmarkPat_GithubAll         |       273 |   4381818 ns/op | 1483152 B/op | 26963 allocs/op |
| BenchmarkPossum_GithubAll      |     10000 |    164367 ns/op |   84448 B/op |   609 allocs/op |
| BenchmarkR2router_GithubAll    |     10000 |    160220 ns/op |   77328 B/op |   979 allocs/op |
| BenchmarkRivet_GithubAll       |     14625 |     82453 ns/op |   16272 B/op |   167 allocs/op |
| BenchmarkTango_GithubAll       |      6255 |    279611 ns/op |   63826 B/op |  1618 allocs/op |
| BenchmarkTigerTonic_GithubAll  |      2008 |    687874 ns/op |  193856 B/op |  4474 allocs/op |
| BenchmarkTraffic_GithubAll     |       355 |   3478508 ns/op |  820744 B/op | 14114 allocs/op |
| BenchmarkVulcan_GithubAll      |      6885 |    193333 ns/op |   19894 B/op |   609 allocs/op |

- 测试结果说明:

  Benchmark name: 基准测试项

  第(1)列:在固定时间内完成的重复次数, 值越大性能好

  第(2)列:执行单次重复任务消耗的纳秒数, 单位ns/op, 值越低越好

  第(3)列:执行单次重复任务消耗的堆内存字节数, 单位B/op, 值越低越好

  第(4)列:每个重复任务平均分配内存的次数, 单位allocs/op, 值越低越好

## Gin v1稳定版

- [x] 零内存分配的路由器
- [x] 仍然是最快的http路由器和框架
- [x] 完整的单元测试
- [x] 严格测试
- [x] API版本冻结,新发布的版本对你原来的代码兼容

## 使用[jsoniter](https://github.com/json-iterator/go)编译

[jsoniter](https://github.com/json-iterator/go)是一个高性能可以替代Golang标准库encoding/json并且完全兼容的包, Gin默认使用`encoding/json`包,但是你可以使用以下tags修改为jsoniter重新编译源码

```sh
$ go build -tags=jsoniter .
```

## API 示例

你可以访问源码, 查看更多接口示例代码 [Gin示例仓库](https://github.com/gin-gonic/examples).

### 使用GET, POST, PUT, PATCH, DELETE, OPTIONS

```go
func main() {
	// Creates a gin router with default middleware:
	// logger and recovery (crash-free) middleware
	router := gin.Default()

	router.GET("/someGet", getting)
	router.POST("/somePost", posting)
	router.PUT("/somePut", putting)
	router.DELETE("/someDelete", deleting)
	router.PATCH("/somePatch", patching)
	router.HEAD("/someHead", head)
	router.OPTIONS("/someOptions", options)

	// By default it serves on :8080 unless a
	// PORT environment variable was defined.
	router.Run()
	// router.Run(":3000") for a hard coded port
}
```

### 获取请求中的路径参数

```go
func main() {
  router := gin.Default()
​
  // This handler will match /user/john but will not match /user/ or /user
  //以下路由只会匹配/user/用户名, 不会匹配/user/或者/user
  router.GET("/user/:name", func(c *gin.Context) {
    name := c.Param("name") //使用Param方法从路径中获取参数
    c.String(http.StatusOK, "Hello %s", name)
  })
​
  // However, this one will match /user/john/ and also /user/john/send
  // If no other routers match /user/john, it will redirect to /user/john/
  // 以下带冒号:和带星号*组成的路由可以匹配/user/用户名/或/user/用户名/动作,如果/user/用户名没有匹配到其他路由,它会自动重定向到/user/用户名/进行匹配
  router.GET("/user/:name/*action", func(c *gin.Context) {
    name := c.Param("name")
    action := c.Param("action")
    message := name + " is " + action
    c.String(http.StatusOK, message)
  })
​
  // For each matched request Context will hold the route definition
  // 请求上下文request Context会保存所有匹配上的路由定义到c.FullPath()方法
  router.POST("/user/:name/*action", func(c *gin.Context) {
    c.FullPath() == "/user/:name/*action" // true
  })
​
  router.Run(":8080")
}
```

### 获取查询字符串参数

```go
func main() {
  router := gin.Default()
​
  // Query string parameters are parsed using the existing underlying request object.
  // The request responds to a url matching:  /welcome?firstname=Jane&lastname=Doe
  // 发送测试请求:/welcome?firstname=Jane&lastname=Doe
  router.GET("/welcome", func(c *gin.Context) {
    firstname := c.DefaultQuery("firstname", "Guest") //如果没有获取到该键值,则使用第二个参数作为默认值
    lastname := c.Query("lastname") 
    //上一行的完整写法:c.Request.URL.Query().Get("lastname")
​
    c.String(http.StatusOK, "Hello %s %s", firstname, lastname)
  })
  router.Run(":8080")
}
```

### 获取Multipart/Urlencoded类型表单

```go
package main
​
import "github.com/gin-gonic/gin"
​
func main() {
  router := gin.Default()
​
  // 模拟提交表单:curl -XPOST http://localhost:8080/form_post -d "message=消息&nick=昵称"
  router.POST("/form_post", func(c *gin.Context) {
    message := c.PostForm("message")
    nick := c.DefaultPostForm("nick", "anonymous")
​
    c.JSON(200, gin.H{
      "status":  "posted",
      "message": message,
      "nick":    nick,
    })
  })
  router.Run(":8080")
}
//返回结果: {"message":"消息","nick":"昵称","status":"posted"}
```

### 另一个示例: 查询参数 + Post表单

```
POST /post?id=1234&page=1 HTTP/1.1
Content-Type: application/x-www-form-urlencoded

name=manu&message=this_is_great
```

```go
package main
​
import (
  "fmt"
  "github.com/gin-gonic/gin"
)
​
func main() {
  router := gin.Default()
​
  router.POST("/post", func(c *gin.Context) {
​
    id := c.Query("id")
    page := c.DefaultQuery("page", "0")
    name := c.PostForm("name")
    message := c.PostForm("message")
​
    fmt.Printf("id: %s; page: %s; name: %s; message: %s\n", id, page, name, message)
    c.JSON(200, gin.H{
      "id": id,
      "page": page,
      "name": name,
      "message": message,
    })
  })
  router.Run(":8080")
}
```

```
id: 1234; page: 1; name: manu; message: this_is_great
```

### 以Map映射作为查询字符串或Post表单参数

```
POST /post?ids[a]=1234&ids[b]=hello HTTP/1.1
Content-Type: application/x-www-form-urlencoded

names[first]=thinkerou&names[second]=tianou
```

```go
func main() {
  router := gin.Default()
​
  router.POST("/post", func(c *gin.Context) {
​
    ids := c.QueryMap("ids")  //获取查询参数中的Map
    names := c.PostFormMap("names")   //获取Post表单中的Map
​
    fmt.Printf("ids: %v; names: %v\n", ids, names)
  })
  router.Run(":8080")
}
```

```
模拟请求:
curl -XPOST http://localhost:8080/post?ids[a]=1234&ids[b]=hello -d "names[first]=thinkerou&names[second]=tianou"
打印结果:
ids: map[a:1234 b:hello]; names: map[first:thinkerou second:tianou]
```

### 上传文件

#### 单个文件

参考问题 [#774](https://github.com/gin-gonic/gin/issues/774),  [示例代码](https://github.com/gin-gonic/examples/tree/master/upload-file/single).

文件名`file.Filename` 中带路径是不可信赖的, 参考 [`Content-Disposition` on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Disposition#Directives) 和问题 [#1693](https://github.com/gin-gonic/gin/issues/1693)

> 文件名必须是安全可信赖的, 需要去掉路径信息,保留文件名即可

```go
package main
​
import (
  "fmt"
  "github.com/gin-gonic/gin"
  "log"
  "net/http"
  "os"
)
​
func main() {
  router := gin.Default()
  // Set a lower memory limit for multipart forms (default is 32 MiB)
  // 设置请求表单最大内存限制,默认是30MB
​
  //内部调用http请求的ParseMultipartForm方法,该方法要求传入一个字节数, 要取MultipartForm字段的数据，先使用ParseMultipartForm()方法解析Form，解析时会读取所有数据，但需要指定保存在内存中的最大字节数，剩余的字节数会保存在临时磁盘文件中
  maxMultipartMemory := int64(8 << 20)
  log.Printf("解析文件到内存的最大字节:%d", maxMultipartMemory)
  router.MaxMultipartMemory = maxMultipartMemory  // 8 MiB
  router.POST("/upload", func(c *gin.Context) {
    // single file
    file, _ := c.FormFile("file")  //FormFile从表单中返回第一个匹配到的文件对象(结构)
    log.Printf("获取到的文件名:%s", file.Filename)  //文件名必须是安全可信耐的,需要去掉路径信息,保留文件名即可
​
    // Upload the file to specific dst.
    currentPath, _ := os.Getwd()  //获取当前文件路径
    dst := currentPath + "/" + file.Filename
    log.Printf("保存文件绝对路径:%s", dst)
    c.SaveUploadedFile(file, dst)
​
    c.String(http.StatusOK, fmt.Sprintf("'%s' uploaded!", file.Filename))
  })
  router.Run(":8080")
}
​
//模拟单文件上传:
//curl -X POST http://localhost:8080/upload  -H "Content-Type: multipart/form-data" -F "file=@文件名"
```

#### 多个文件

 [完整示例代码](https://github.com/gin-gonic/examples/tree/master/upload-file/multiple).

```go
package main
​
import (
  "fmt"
  "github.com/gin-gonic/gin"
  "log"
  "net/http"
  "os"
)
​
func main() {
  router := gin.Default()
  // Set a lower memory limit for multipart forms (default is 32 MiB)
  // 设置请求表单最大内存限制,默认是30MB
  //内部调用http请求的ParseMultipartForm方法,该方法要求传入一个字节数, 要取MultipartForm字段的数据，先使用ParseMultipartForm()方法解析Form，解析时会读取所有数据，但需要指定保存在内存中的最大字节数，剩余的字节数会保存在临时磁盘文件中
  maxMultipartMemory := int64(8 << 20)
  log.Printf("解析文件到内存的最大字节:%d", maxMultipartMemory)
  router.MaxMultipartMemory = maxMultipartMemory  // 8 MiB
  router.POST("/upload", func(c *gin.Context) {
    // Upload the file to specific dst.
    currentPath, _ := os.Getwd()  //获取当前文件路径
    // Multipart form
    form, _ := c.MultipartForm() //多文件表单
    files := form.File["upload[]"] //通过前端提供的键名获取文件数组
    for _, file := range files {
      dst := currentPath + "/" + file.Filename
      log.Printf("保存文件绝对路径:%s", dst)
      // Upload the file to specific dst.
      c.SaveUploadedFile(file, dst)
    }
    c.String(http.StatusOK, fmt.Sprintf("%d files uploaded!", len(files)))
  })
  router.Run(":8080")
}
​
//模拟多文件上传
//curl -X POST http://localhost:8080/upload -H "Content-Type: multipart/form-data" -F "upload[]=@文件1" -F "upload[]=@文件2"
```

### 路由分组

路由分组可用于新老接口兼容, 针对不同分组的路由使用不同的中间件处理逻辑等

```go
func main() {
  router := gin.Default()
  // Simple group: v1  路由分组1
  v1 := router.Group("/v1")
  {
    v1.POST("/login", loginEndpoint)
    v1.POST("/submit", submitEndpoint)
    v1.POST("/read", readEndpoint)
  }
  // Simple group: v2  路由分组2
  v2 := router.Group("/v2")
  {
    v2.POST("/login", loginEndpoint)
    v2.POST("/submit", submitEndpoint)
    v2.POST("/read", readEndpoint)
  }
  router.Run(":8080")
}
```

### Gin引擎初始化(不带中间件或使用日志和异常恢复中间件)

New()方法得到一个不使用任何中间件的Gin引擎Engine对象r

```go
r := gin.New()
```

默认方法Default()使用Logger(日志记录器)和Recovery(异常自恢复)中间件

```go
// Default With the Logger and Recovery middleware already attached
// 默认方法使用Logger(日志记录器)和Recovery(异常自恢复)中间件
r := gin.Default()
```


### 使用中间件
```go
func main() {
	// Creates a router without any middleware by default
	r := gin.New()

	// Global middleware
	// Logger middleware will write the logs to gin.DefaultWriter even if you set with GIN_MODE=release.
  // Logger日志中间件会将日志写到Gin默认写出器(标准输出),即使开启了release模式
	// By default gin.DefaultWriter = os.Stdout
	r.Use(gin.Logger())

	// Recovery middleware recovers from any panics and writes a 500 if there was one.
  // Recovery异常恢复中间件会在程序崩溃时恢复程序,返回状态码为500的错误
	r.Use(gin.Recovery())

	// Per route middleware, you can add as many as you desire.
  // 你可以针对每个路由添加需要的中间件
	r.GET("/benchmark", MyBenchLogger(), benchEndpoint)

	// Authorization group
	// authorized := r.Group("/", AuthRequired())
	// exactly the same as:
	authorized := r.Group("/")
	// per group middleware! in this case we use the custom created
	// AuthRequired() middleware just in the "authorized" group.
  // 也可以针对路由分组添加统一的中间件
	authorized.Use(AuthRequired())
	{
		authorized.POST("/login", loginEndpoint)
		authorized.POST("/submit", submitEndpoint)
		authorized.POST("/read", readEndpoint)

		// nested group
    // 嵌套路由组
		testing := authorized.Group("testing")
		testing.GET("/analytics", analyticsEndpoint)
	}

	// Listen and serve on 0.0.0.0:8080
	r.Run(":8080")
}
```

### 自定义程序崩溃后的处理方式(邮件/微信/短信等告警)
```go
package main
​
import (
  "fmt"
  "github.com/gin-gonic/gin"
  "log"
  "net/http"
)
​
func CustomRecovery() gin.HandlerFunc {
  return func(c *gin.Context) {
    defer func() {
      //if r := recover(); r != nil {
      //  log.Printf("崩溃信息:%s", r)
      //}
​
      if err, ok := recover().(string); ok {
        log.Printf("您可以在这里完成告警任务,邮件,微信等告警")
        c.String(http.StatusInternalServerError, fmt.Sprintf("error: %s", err))
      }
      c.AbortWithStatus(http.StatusInternalServerError)
    }()
    c.Next()
  }
}
​
func main() {
  // Creates a router without any middleware by default
  r := gin.New()
​
  // Global middleware
  // Logger middleware will write the logs to gin.DefaultWriter even if you set with GIN_MODE=release.
  // By default gin.DefaultWriter = os.Stdout
  r.Use(gin.Logger())
​
  // Recovery middleware recovers from any panics and writes a 500 if there was one.
  //r.Use(CustomRecovery())  //使用自定义中间件处理程序崩溃
​
  //使用匿名函数组成中间件,处理程序崩溃
  r.Use(func( c *gin.Context){
    defer func() {
      if err, ok := recover().(string); ok {
        log.Printf("您可以在这里完成告警任务,邮件,微信等告警")
        c.String(http.StatusInternalServerError, fmt.Sprintf("error: %s", err))
      }
      c.AbortWithStatus(http.StatusInternalServerError)
    }()
    c.Next()
  })
​
  r.GET("/panic", func(c *gin.Context) {
    // panic with a string -- the custom middleware could save this to a database or report it to the user
    panic("程序崩溃")
  })
​
  r.GET("/", func(c *gin.Context) {
    c.String(http.StatusOK, "ohai")
  })
​
  // Listen and serve on 0.0.0.0:8080
  r.Run(":8080")
}
//模拟程序崩溃: curl http://localhost:8080/panic
```

### 怎样记录日志到文件

利用io.MultiWriter多写出器可以实现日志记录到文件的同时也输出到控制台

```go
package main
​
import (
  "github.com/gin-gonic/gin"
  "io"
  "os"
)
​
func main() {
  // Disable Console Color, you don't need console color when writing the logs to file.
  // 禁用控制台日志颜色,日志写到文件的时候,不需要打开控制台日志颜色
  gin.DisableConsoleColor()
  // Logging to a file.  新建日志文件,得到文件结构,文件结构实现了写出器Writer接口
  f, _ := os.Create("gin.log")
  //io.MultiWriter(多写出器方法)创建一个写出器, 将传入的多个写出器追加为一个写出器数组, 得到的写出器实现了Writer接口, 它会将需要写出的数据写出到每个写出器, 就像Unix命令tee,会将数据写入文件的同时打印到标准输出
  //配置Gin默认日志写出器为得到的多写出器
  gin.DefaultWriter = io.MultiWriter(f)
  // Use the following code if you need to write the logs to file and console at the same time.
  // 使用下面的代码,将日志写入文件的同时,也输出到控制台
  // gin.DefaultWriter = io.MultiWriter(f, os.Stdout)
​
  router := gin.Default()
  router.GET("/ping", func(c *gin.Context) {
    c.String(200, "pong")
  })
​
  router.Run(":8080")
}
```

### 自定义日志格式
```go
package main
​
import (
  "fmt"
  "github.com/gin-gonic/gin"
  "time"
)
​
func main() {
  router := gin.New()
​
  // LoggerWithFormatter middleware will write the logs to gin.DefaultWriter
  // By default gin.DefaultWriter = os.Stdout
  // type LogFormatter func(params LogFormatterParams) string 这里的LogFormatterParams是一个格式化日志参数的结构体
  router.Use(gin.LoggerWithFormatter(func(param gin.LogFormatterParams) string {
    // your custom format
    // 127.0.0.1 - [Sun, 22 Nov 2020 17:09:53 CST] "GET /ping HTTP/1.1 200 56.113µs "curl/7.64.1" "
    return fmt.Sprintf("%s - [%s] \"%s %s %s %d %s \"%s\" %s\"\n",
      param.ClientIP,                       //请求客户端的IP地址
      param.TimeStamp.Format(time.RFC1123), //请求时间
      param.Method,                         //请求方法
      param.Path,                           //路由路径
      param.Request.Proto,                  //请求协议
      param.StatusCode,                     //http响应码
      param.Latency,                        //请求到响应的延时
      param.Request.UserAgent(),            //客户端代理程序
      param.ErrorMessage,                   //如果有错误,也打印错误信息
    )
  }))
  router.Use(gin.Recovery())
​
  router.GET("/ping", func(c *gin.Context) {
    c.String(200, "pong")
  })
​
  router.Run(":8080")
}
//模拟请求测试: curl http://localhost:8080/ping
```

**参考输出**

```
::1 - [Fri, 07 Dec 2018 17:04:38 JST] "GET /ping HTTP/1.1 200 122.767µs "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.80 Safari/537.36" "
```

### 控制日志输出颜色 

默认情况, 日志输出到控制台的颜色取决于使用的虚拟终端TTY的颜色方案.

禁用日志颜色: 

```go
func main() {
    // Disable log's color
    gin.DisableConsoleColor()
    
    // Creates a gin router with default middleware:
    // logger and recovery (crash-free) middleware
    router := gin.Default()
    
    router.GET("/ping", func(c *gin.Context) {
        c.String(200, "pong")
    })
    
    router.Run(":8080")
}
```

打开日志颜色:

```go
func main() {
    // Force log's color
    gin.ForceConsoleColor()
    
    // Creates a gin router with default middleware:
    // logger and recovery (crash-free) middleware
    router := gin.Default()
    
    router.GET("/ping", func(c *gin.Context) {
        c.String(200, "pong")
    })
    
    router.Run(":8080")
}
//模拟请求测试: curl http://localhost:8080/ping
```

### 模型绑定和验证

使用模型绑定来绑定请求体到一个Go类型上. 目前支持JSON,XML,YAML以及标准表单(如foo=bar&boo=baz)的绑定.

Gin使用[**go-playground/validator/v10**](https://github.com/go-playground/validator)包来验证请求, 关于tags在验证中使用详见[Tags](https://godoc.org/github.com/go-playground/validator#hdr-Baked_In_Validators_and_Tags)

注意:绑定前请确认结构体中需要绑定的字段标签与绑定类型一致,比如绑定JSON,设置标签:` json:"fieldname"`

Gin提供两种方式(类型)来完成绑定:

- **方式一** - Must bind
  - **方法** - `Bind`, `BindJSON`, `BindXML`, `BindQuery`, `BindYAML`, `BindHeader`
  - **特点** - 这些方法底层使用`MustBindWith`方法. 如果出现绑定错误, 请求将以状态码400返回失败信息:`c.AbortWithError(400, err).SetType(ErrorTypeBind)`, 响应中设置Content-Type头为text/plain; charset=utf-8.如果手动设置响应码,会警告响应头已经设置,比如提示: `[GIN-debug] [WARNING] Headers were already written. Wanted to override status code 400 with 422`, 如果想要更好的控制这些行为,建议使用下面对应的ShoudBind方法.
- **方式二** - Should bind
  - **方法** - `ShouldBind`, `ShouldBindJSON`, `ShouldBindXML`, `ShouldBindQuery`, `ShouldBindYAML`, `ShouldBindHeader`
  - **特点** - 这些方法底层使用`ShouldBindWith`. 如果出现绑定错误, 会返回错误, 开发者可以控制和恰当的处理这些错误.

当使用绑定方法时, Gin尝试根据类型头`Content-Type header`自动推断要使用的绑定器. 如果你已经确认需要绑定的类型,可以直接使用底层的`MustBindWith`或`ShouldBindWith`方法.

你也可以针对特殊的字段指定required标签值, 如果某个字段指定了:`binding:"required"`标签, 但是在绑定时该字段为空会返回错误.

如以下代码绑定JSON:

```go
package main
​
import (
  "github.com/gin-gonic/gin"
  "net/http"
)
​
// Binding from JSON
type Login struct {
  User string `form:"user" json:"user" xml:"user"  binding:"required"` //分别定义form,json,xml,binding等标签
  //Password string `form:"password" json:"password" xml:"password" binding:"required"`
  Password string `form:"password" json:"password" xml:"password" binding:"-"`
}
​
func main() {
  router := gin.Default()
​
  // Example for binding JSON ({"user": "manu", "password": "123"})
  router.POST("/loginJSON", func(c *gin.Context) {
    var json Login
    if err := c.ShouldBindJSON(&json); err != nil {
      c.JSON(http.StatusBadRequest, gin.H{"error": err.Error()})
      return
    }
​
    if json.User != "manu" || json.Password != "123" {
      c.JSON(http.StatusUnauthorized, gin.H{"status": "unauthorized"})
      return
    }
​
    c.JSON(http.StatusOK, gin.H{"status": "you are logged in"})
  })
​
  // Example for binding XML (
  //  <?xml version="1.0" encoding="UTF-8"?>
  //  <root>
  //    <user>user</user>
  //    <password>123</password>
  //  </root>)
  router.POST("/loginXML", func(c *gin.Context) {
    var xml Login
    if err := c.ShouldBindXML(&xml); err != nil {
      c.JSON(http.StatusBadRequest, gin.H{"error": err.Error()})
      return
    }
​
    if xml.User != "manu" || xml.Password != "123" {
      c.JSON(http.StatusUnauthorized, gin.H{"status": "unauthorized"})
      return
    }
​
    c.JSON(http.StatusOK, gin.H{"status": "you are logged in"})
  })
​
  // Example for binding a HTML form (user=manu&password=123)
  router.POST("/loginForm", func(c *gin.Context) {
    var form Login
    // This will infer what binder to use depending on the content-type header.
    if err := c.ShouldBind(&form); err != nil {
      c.JSON(http.StatusBadRequest, gin.H{"error": err.Error()})
      return
    }
​
    if form.User != "manu" || form.Password != "123" {
      c.JSON(http.StatusUnauthorized, gin.H{"status": "unauthorized"})
      return
    }
​
    c.JSON(http.StatusOK, gin.H{"status": "you are logged in"})
  })
​
  // Listen and serve on 0.0.0.0:8080
  router.Run(":8080")
}
​
//模拟请求: curl -v -X POST http://localhost:8080/loginJSON -H 'content-type: application/json' -d '{ "user": "manu", "password": "123" }'
```

**请求示例**

```shell
$ curl -v -X POST \
  http://localhost:8080/loginJSON \
  -H 'content-type: application/json' \
  -d '{ "user": "manu" }'
> POST /loginJSON HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.51.0
> Accept: */*
> content-type: application/json
> Content-Length: 18
>
* upload completely sent off: 18 out of 18 bytes
< HTTP/1.1 400 Bad Request
< Content-Type: application/json; charset=utf-8
< Date: Fri, 04 Aug 2017 03:51:31 GMT
< Content-Length: 100
<
{"error":"Key: 'Login.Password' Error:Field validation for 'Password' failed on the 'required' tag"}
```

**跳过验证**

跳过验证: 与`binding:"required"`标签对应的是`binding:"-"`, 表示该字段不做绑定, 所以绑定时该字段为空不会报错.



### 自定义验证器

你也可以自己注册一个自定义验证器,  [示例代码](https://github.com/gin-gonic/examples/tree/master/custom-validation/server.go).

```go
package main
​
import (
  "net/http"
  "time"
​
  "github.com/gin-gonic/gin"
  "github.com/gin-gonic/gin/binding"
  "github.com/go-playground/validator/v10"
)
​
// Booking contains binded and validated data.
// Booking结构中定义了包含绑定器和日期验证器标签
type Booking struct {
  CheckIn  time.Time `form:"check_in" binding:"required,bookabledate" time_format:"2006-01-02"`  //登记时间
  CheckOut time.Time `form:"check_out" binding:"required,gtfield=CheckIn" time_format:"2006-01-02"`  //gtfield=CheckIn表示结账时间必须大于登记时间
}
​
// 定义日期验证器
var bookableDate validator.Func = func(fl validator.FieldLevel) bool {
  date, ok := fl.Field().Interface().(time.Time)  //利用反射获取到字段值 -> 转为接口 -> 类型断言(时间类型)
  if ok {
    today := time.Now()
    if today.After(date) {  //如果当前时间在checkIn字段时间之后,返回false,即登记时间不能早于当前的时间
      return false
    }
  }
  return true
}
​
func main() {
  route := gin.Default()
  //对binding.Validator.Engine()接口进行类型断言,断言类型为Validate结构,如果断言成功,就将自定义的验证器注册到Gin内部
  if v, ok := binding.Validator.Engine().(*validator.Validate); ok {
    // - if the key already exists, the previous validation function will be replaced. 该注册方法会将已经存在的验证器替换
    // - this method is not thread-safe it is intended that these all be registered prior to any validation
    // 注册方法不是线程安全的, 在验证开始前,需要保证所有的验证器都注册成功
    v.RegisterValidation("bookabledate", bookableDate)
  }
​
  route.GET("/bookable", getBookable)
  route.Run(":8085")
}
​
func getBookable(c *gin.Context) {
  var b Booking
  if err := c.ShouldBindWith(&b, binding.Query); err == nil {
    c.JSON(http.StatusOK, gin.H{"message": "Booking dates are valid!"})
  } else {
    c.JSON(http.StatusBadRequest, gin.H{"error": err.Error()})
  }
}
​
//模拟请求:
// 登记时间和结账时间符合条件
//$ curl "localhost:8085/bookable?check_in=2030-04-16&check_out=2030-04-17"
//{"message":"Booking dates are valid!"}
//
// 登记时间在结账时间之后, 不满足gtfield校验规则
//$ curl "localhost:8085/bookable?check_in=2030-03-10&check_out=2030-03-09"
//{"error":"Key: 'Booking.CheckOut' Error:Field validation for 'CheckOut' failed on the 'gtfield' tag"}
//
// 登记时间在当前时间之前,不满足自定义的验证器
//$ curl "localhost:8085/bookable?check_in=2000-03-09&check_out=2000-03-10"
//{"error":"Key: 'Booking.CheckIn' Error:Field validation for 'CheckIn' failed on the 'bookabledate' tag"}%
```

```console
$ curl "localhost:8085/bookable?check_in=2030-04-16&check_out=2030-04-17"
{"message":"Booking dates are valid!"}

$ curl "localhost:8085/bookable?check_in=2030-03-10&check_out=2030-03-09"
{"error":"Key: 'Booking.CheckOut' Error:Field validation for 'CheckOut' failed on the 'gtfield' tag"}

$ curl "localhost:8085/bookable?check_in=2000-03-09&check_out=2000-03-10"
{"error":"Key: 'Booking.CheckIn' Error:Field validation for 'CheckIn' failed on the 'bookabledate' tag"}%    
```

另外[结构体级别的验证](https://github.com/go-playground/validator/releases/tag/v8.7)采用如下的方式注册, v.RegisterStructValidation(UserStructLevelValidation, User{}),  请参考[结构体级别验证示例](https://github.com/gin-gonic/examples/tree/master/struct-lvl-validations)



### 只绑定查询字符串

使用`SholdBindQuery`方法只绑定查询参数, 而不会绑定post的数据. 请参[详情](https://github.com/gin-gonic/gin/issues/742#issuecomment-315953017).

```go
package main
​
import (
  "log"
​
  "github.com/gin-gonic/gin"
)
​
type Person struct {
  Name    string `form:"name"`
  Address string `form:"address"`
}
​
func main() {
  route := gin.Default()
  route.Any("/testing", startPage)
  route.Run(":8085")
}
​
func startPage(c *gin.Context) {
  var person Person
  // ShouldBindQuery is a shortcut for c.ShouldBindWith(obj, binding.Query)
  // ShouldBindQuery是c.ShouldBindWith(obj, binding.Query)方法的一个快捷绑定方法, 该方法只绑定请求字符串query string,而忽略Post提交的表单数据
  if c.ShouldBindQuery(&person) == nil {
    log.Println("====== Only Bind By Query String ======")
    log.Println(person.Name)
    log.Println(person.Address)
  }
  c.String(200, "Success")
}
//only bind query 模拟查询字符串请求
//curl -X GET "localhost:8085/testing?name=eason&address=xyz"
​
//only bind query string, ignore form data 模拟查询字符串请求和Post表单,这里的表单会被忽略
//curl -X POST "localhost:8085/testing?name=eason&address=xyz" --data 'name=ignore&address=ignore' -H "Content-Type:application/x-www-form-urlencoded
```

### 绑定查询字符串或Post表单数据

 [详情请参考](https://github.com/gin-gonic/gin/issues/742#issuecomment-264681292).

```go
package main
​
import (
  "log"
  "time"
​
  "github.com/gin-gonic/gin"
)
​
type Person struct {
  Name       string    `form:"name"`
  Address    string    `form:"address"`
  Birthday   time.Time `form:"birthday" time_format:"2006-01-02" time_utc:"1"`
  CreateTime time.Time `form:"createTime" time_format:"unixNano"`
  UnixTime   time.Time `form:"unixTime" time_format:"unix"`
}
​
func main() {
  route := gin.Default()
  //route.GET("/testing", startPage)           //使用GET
  route.POST("/testing", startPage)  //使用POST
  route.Run(":8085")
}
​
func startPage(c *gin.Context) {
  var person Person
  // If `GET`, only `Form` binding engine (`query`) used.  如果路由是GET方法,则只使用查询字符串引擎绑定
  // If `POST`, first checks the `content-type` for `JSON` or `XML`, then uses `Form` (`form-data`).
  // See more at https://github.com/gin-gonic/gin/blob/master/binding/binding.go#L48
  //如果是POST方式, ShouldBind方法检查请求类型头Content-Type来自动选择绑定引擎,比如Json/XML
  if c.ShouldBind(&person) == nil {
    log.Println(person.Name)
    log.Println(person.Address)
    log.Println(person.Birthday)
    log.Println(person.CreateTime)
    log.Println(person.UnixTime)
  }
​
  //if c.BindJSON(&person) == nil {
  //  log.Println("====== Bind By JSON ======")
  //  log.Println(person.Name)
  //  log.Println(person.Address)
  //}
​
  c.String(200, "Success")
}
//模拟查询字符串参数请求:
//curl -X GET "localhost:8085/testing?name=appleboy&address=xyz&birthday=1992-03-15&createTime=1562400033000000123&unixTime=1562400033"
//模拟Post Json请求
//curl -X POST localhost:8085/testing --data '{"name":"JJ", "address":"xyz"}' -H "Content-Type:application/json"
```

Test it with:
```sh
$ curl -X GET "localhost:8085/testing?name=appleboy&address=xyz&birthday=1992-03-15&createTime=1562400033000000123&unixTime=1562400033"
```

### 绑定URI

将结构体中标签指定的字段与URI中对应的字段进行绑定, 请参考[详情](https://github.com/gin-gonic/gin/issues/846).

```go
package main
​
import "github.com/gin-gonic/gin"
​
type Person struct {
  ID string `uri:"id" binding:"required,uuid"`  //指定URI标签
  Name string `uri:"name" binding:"required"`
}
​
func main() {
  route := gin.Default()
  //下面的URI中的name和id与Person结构中的标签分别对应
  route.GET("/:name/:id", func(c *gin.Context) {
    var person Person
    if err := c.ShouldBindUri(&person); err != nil {
      c.JSON(400, gin.H{"msg": err})
      return
    }
    c.JSON(200, gin.H{"name": person.Name, "uuid": person.ID})
  })
  route.Run(":8088")
}
//模拟请求
//curl -v localhost:8088/thinkerou/987fbc97-4bed-5078-9f07-9141ba07c9f3
//curl -v localhost:8088/thinkerou/not-uuid
```

模拟请求测试:
```sh
$ curl -v localhost:8088/thinkerou/987fbc97-4bed-5078-9f07-9141ba07c9f3
$ curl -v localhost:8088/thinkerou/not-uuid
```

### 绑定请求头

```go
package main
​
import (
  "fmt"
  "github.com/gin-gonic/gin"
)
​
type testHeader struct {
  Rate   int    `header:"Rate"`   //结构中添加header标签
  Domain string `header:"Domain"`
}
​
func main() {
  r := gin.Default()
  r.GET("/", func(c *gin.Context) {
​    h := testHeader{}
​
    //ShouldBindHeader是c.ShouldBindWith(obj, binding.Header)的快捷方法
    if err := c.ShouldBindHeader(&h); err != nil {
      c.JSON(200, err)
    }
​
    fmt.Printf("%#v\n", h)
    c.JSON(200, gin.H{"Rate": h.Rate, "Domain": h.Domain})
  })
​
  r.Run()
}
​
//模拟请求
// curl -H "rate:300" -H "domain:music" http://localhost:8080/
// 参考输出:
// {"Domain":"music","Rate":300}
```

### 绑定HTML复选框

请参考[详情](https://github.com/gin-gonic/gin/issues/129#issuecomment-124260092), 将html与main.go放到一个目录,执行go run main.go运行后, 访问http://localhost:8080,勾选复选框,然后提交测试

main.go

```go
package main
​
import (
  "github.com/gin-gonic/gin"
)
​
type myForm struct {
  Colors []string `form:"colors[]"` //标签中的colors[]数组切片与html文件中的name="colors[]"对应
}
​
func main() {
  r := gin.Default()
​
  //LoadHTMLGlob采用通配符模式匹配HTML文件,并将内容进行渲染,提供给前端访问
  r.LoadHTMLGlob("*.html")
​  r.GET("/", indexHandler)
  r.POST("/", formHandler)
​
  r.Run(":8080")
}
​
func indexHandler(c *gin.Context) {
  c.HTML(200, "form.html", nil)
}
​
func formHandler(c *gin.Context) {
  var fakeForm myForm
  c.Bind(&fakeForm) //Bind方法根据请求头类型Content-Type, 自动选择合适的绑定引擎,如Json/XML
  c.JSON(200, gin.H{"color": fakeForm.Colors})
}
​
//将html与main.go放到一个目录,执行go run main.go运行后, 访问http://localhost:8080,勾选复选框,然后提交测试
```

form.html

```html
<form action="/" method="POST">
    <p>Check some colors</p>
    <label for="red">Red</label>
    <input type="checkbox" name="colors[]" value="red" id="red">
    <label for="green">Green</label>
    <input type="checkbox" name="colors[]" value="green" id="green">
    <label for="blue">Blue</label>
    <input type="checkbox" name="colors[]" value="blue" id="blue">
    <input type="submit">
</form>
```

结果:

```
{"color":["red","green","blue"]}
```

### 绑定Multipart/Urlencoded类型的表单

使用`ShouldBind`方法结合结构体标签, 以及mime/multipart包完成多部分类型表单数据`multipart/form-data`或URL编码类型表单`application/x-www-form-urlencoded`数据进行绑定:

```go
package main
​
import (
  "github.com/gin-gonic/gin"
  "mime/multipart"
  "net/http"
)
​
type ProfileForm struct {
  Name   string                `form:"name" binding:"required"`
  Avatar *multipart.FileHeader `form:"avatar" binding:"required"`
​
  // or for multiple files
  // Avatars []*multipart.FileHeader `form:"avatar" binding:"required"`
}
​
func main() {
  router := gin.Default()
  router.POST("/profile", func(c *gin.Context) {
    // you can bind multipart form with explicit binding declaration:  可以使用显示申明的方式,即用ShouldBindWith(&from, binding.Form)方法来绑定多部分类型表单multipart form
    // c.ShouldBindWith(&form, binding.Form)
    // or you can simply use autobinding with ShouldBind method:
    var form ProfileForm
    // in this case proper binding will be automatically selected
    // 这里使用ShouldBind方法自动选择绑定器进行绑定
    if err := c.ShouldBind(&form); err != nil {
      c.String(http.StatusBadRequest, "bad request")
      return
    }
    //保存上传的表单文件到指定的目标文件
    err := c.SaveUploadedFile(form.Avatar, form.Avatar.Filename)
    if err != nil {
      c.String(http.StatusInternalServerError, "unknown error")
      return
    }
    // db.Save(&form)
    c.String(http.StatusOK, "ok")
  })
  router.Run(":8080")
}
//模拟测试:
//curl -X POST -v --form name=user --form "avatar=@./avatar.png" http://localhost:8080/profile
```

模拟测试:
```sh
$ curl -X POST -v --form name=user --form "avatar=@./avatar.png" http://localhost:8080/profile
```

### XML, JSON, YAML and ProtoBuf rendering

```go
func main() {
	r := gin.Default()

	// gin.H is a shortcut for map[string]interface{}
	r.GET("/someJSON", func(c *gin.Context) {
		c.JSON(http.StatusOK, gin.H{"message": "hey", "status": http.StatusOK})
	})

	r.GET("/moreJSON", func(c *gin.Context) {
		// You also can use a struct
		var msg struct {
			Name    string `json:"user"`
			Message string
			Number  int
		}
		msg.Name = "Lena"
		msg.Message = "hey"
		msg.Number = 123
		// Note that msg.Name becomes "user" in the JSON
		// Will output  :   {"user": "Lena", "Message": "hey", "Number": 123}
		c.JSON(http.StatusOK, msg)
	})

	r.GET("/someXML", func(c *gin.Context) {
		c.XML(http.StatusOK, gin.H{"message": "hey", "status": http.StatusOK})
	})

	r.GET("/someYAML", func(c *gin.Context) {
		c.YAML(http.StatusOK, gin.H{"message": "hey", "status": http.StatusOK})
	})

	r.GET("/someProtoBuf", func(c *gin.Context) {
		reps := []int64{int64(1), int64(2)}
		label := "test"
		// The specific definition of protobuf is written in the testdata/protoexample file.
		data := &protoexample.Test{
			Label: &label,
			Reps:  reps,
		}
		// Note that data becomes binary data in the response
		// Will output protoexample.Test protobuf serialized data
		c.ProtoBuf(http.StatusOK, data)
	})

	// Listen and serve on 0.0.0.0:8080
	r.Run(":8080")
}
```

#### SecureJSON

Using SecureJSON to prevent json hijacking. Default prepends `"while(1),"` to response body if the given struct is array values.

```go
func main() {
	r := gin.Default()

	// You can also use your own secure json prefix
	// r.SecureJsonPrefix(")]}',\n")

	r.GET("/someJSON", func(c *gin.Context) {
		names := []string{"lena", "austin", "foo"}

		// Will output  :   while(1);["lena","austin","foo"]
		c.SecureJSON(http.StatusOK, names)
	})

	// Listen and serve on 0.0.0.0:8080
	r.Run(":8080")
}
```
#### JSONP

Using JSONP to request data from a server  in a different domain. Add callback to response body if the query parameter callback exists.

```go
func main() {
	r := gin.Default()

	r.GET("/JSONP", func(c *gin.Context) {
		data := gin.H{
			"foo": "bar",
		}
		
		//callback is x
		// Will output  :   x({\"foo\":\"bar\"})
		c.JSONP(http.StatusOK, data)
	})

	// Listen and serve on 0.0.0.0:8080
	r.Run(":8080")

        // client
        // curl http://127.0.0.1:8080/JSONP?callback=x
}
```

#### AsciiJSON

Using AsciiJSON to Generates ASCII-only JSON with escaped non-ASCII characters.

```go
func main() {
	r := gin.Default()

	r.GET("/someJSON", func(c *gin.Context) {
		data := gin.H{
			"lang": "GO语言",
			"tag":  "<br>",
		}

		// will output : {"lang":"GO\u8bed\u8a00","tag":"\u003cbr\u003e"}
		c.AsciiJSON(http.StatusOK, data)
	})

	// Listen and serve on 0.0.0.0:8080
	r.Run(":8080")
}
```

#### PureJSON

Normally, JSON replaces special HTML characters with their unicode entities, e.g. `<` becomes  `\u003c`. If you want to encode such characters literally, you can use PureJSON instead.
This feature is unavailable in Go 1.6 and lower.

```go
func main() {
	r := gin.Default()
	
	// Serves unicode entities
	r.GET("/json", func(c *gin.Context) {
		c.JSON(200, gin.H{
			"html": "<b>Hello, world!</b>",
		})
	})
	
	// Serves literal characters
	r.GET("/purejson", func(c *gin.Context) {
		c.PureJSON(200, gin.H{
			"html": "<b>Hello, world!</b>",
		})
	})
	
	// listen and serve on 0.0.0.0:8080
	r.Run(":8080")
}
```

### Serving static files

```go
func main() {
	router := gin.Default()
	router.Static("/assets", "./assets")
	router.StaticFS("/more_static", http.Dir("my_file_system"))
	router.StaticFile("/favicon.ico", "./resources/favicon.ico")

	// Listen and serve on 0.0.0.0:8080
	router.Run(":8080")
}
```

### Serving data from file

```go
func main() {
	router := gin.Default()

	router.GET("/local/file", func(c *gin.Context) {
		c.File("local/file.go")
	})

	var fs http.FileSystem = // ...
	router.GET("/fs/file", func(c *gin.Context) {
		c.FileFromFS("fs/file.go", fs)
	})
}

```

### Serving data from reader

```go
func main() {
	router := gin.Default()
	router.GET("/someDataFromReader", func(c *gin.Context) {
		response, err := http.Get("https://raw.githubusercontent.com/gin-gonic/logo/master/color.png")
		if err != nil || response.StatusCode != http.StatusOK {
			c.Status(http.StatusServiceUnavailable)
			return
		}

		reader := response.Body
 		defer reader.Close()
		contentLength := response.ContentLength
		contentType := response.Header.Get("Content-Type")

		extraHeaders := map[string]string{
			"Content-Disposition": `attachment; filename="gopher.png"`,
		}

		c.DataFromReader(http.StatusOK, contentLength, contentType, reader, extraHeaders)
	})
	router.Run(":8080")
}
```

### HTML rendering

Using LoadHTMLGlob() or LoadHTMLFiles()

```go
func main() {
	router := gin.Default()
	router.LoadHTMLGlob("templates/*")
	//router.LoadHTMLFiles("templates/template1.html", "templates/template2.html")
	router.GET("/index", func(c *gin.Context) {
		c.HTML(http.StatusOK, "index.tmpl", gin.H{
			"title": "Main website",
		})
	})
	router.Run(":8080")
}
```

templates/index.tmpl

```html
<html>
	<h1>
		{{ .title }}
	</h1>
</html>
```

Using templates with same name in different directories

```go
func main() {
	router := gin.Default()
	router.LoadHTMLGlob("templates/**/*")
	router.GET("/posts/index", func(c *gin.Context) {
		c.HTML(http.StatusOK, "posts/index.tmpl", gin.H{
			"title": "Posts",
		})
	})
	router.GET("/users/index", func(c *gin.Context) {
		c.HTML(http.StatusOK, "users/index.tmpl", gin.H{
			"title": "Users",
		})
	})
	router.Run(":8080")
}
```

templates/posts/index.tmpl

```html
{{ define "posts/index.tmpl" }}
<html><h1>
	{{ .title }}
</h1>
<p>Using posts/index.tmpl</p>
</html>
{{ end }}
```

templates/users/index.tmpl

```html
{{ define "users/index.tmpl" }}
<html><h1>
	{{ .title }}
</h1>
<p>Using users/index.tmpl</p>
</html>
{{ end }}
```

#### Custom Template renderer

You can also use your own html template render

```go
import "html/template"

func main() {
	router := gin.Default()
	html := template.Must(template.ParseFiles("file1", "file2"))
	router.SetHTMLTemplate(html)
	router.Run(":8080")
}
```

#### Custom Delimiters

You may use custom delims

```go
	r := gin.Default()
	r.Delims("{[{", "}]}")
	r.LoadHTMLGlob("/path/to/templates")
```

#### Custom Template Funcs

See the detail [example code](https://github.com/gin-gonic/examples/tree/master/template).

main.go

```go
import (
    "fmt"
    "html/template"
    "net/http"
    "time"

    "github.com/gin-gonic/gin"
)

func formatAsDate(t time.Time) string {
    year, month, day := t.Date()
    return fmt.Sprintf("%d%02d/%02d", year, month, day)
}

func main() {
    router := gin.Default()
    router.Delims("{[{", "}]}")
    router.SetFuncMap(template.FuncMap{
        "formatAsDate": formatAsDate,
    })
    router.LoadHTMLFiles("./testdata/template/raw.tmpl")

    router.GET("/raw", func(c *gin.Context) {
        c.HTML(http.StatusOK, "raw.tmpl", gin.H{
            "now": time.Date(2017, 07, 01, 0, 0, 0, 0, time.UTC),
        })
    })

    router.Run(":8080")
}

```

raw.tmpl

```html
Date: {[{.now | formatAsDate}]}
```

Result:
```
Date: 2017/07/01
```

### Multitemplate

Gin allow by default use only one html.Template. Check [a multitemplate render](https://github.com/gin-contrib/multitemplate) for using features like go 1.6 `block template`.

### Redirects

Issuing a HTTP redirect is easy. Both internal and external locations are supported.

```go
r.GET("/test", func(c *gin.Context) {
	c.Redirect(http.StatusMovedPermanently, "http://www.google.com/")
})
```

Issuing a HTTP redirect from POST. Refer to issue: [#444](https://github.com/gin-gonic/gin/issues/444)
```go
r.POST("/test", func(c *gin.Context) {
	c.Redirect(http.StatusFound, "/foo")
})
```

Issuing a Router redirect, use `HandleContext` like below.

``` go
r.GET("/test", func(c *gin.Context) {
    c.Request.URL.Path = "/test2"
    r.HandleContext(c)
})
r.GET("/test2", func(c *gin.Context) {
    c.JSON(200, gin.H{"hello": "world"})
})
```


### Custom Middleware

```go
func Logger() gin.HandlerFunc {
	return func(c *gin.Context) {
		t := time.Now()

		// Set example variable
		c.Set("example", "12345")

		// before request

		c.Next()

		// after request
		latency := time.Since(t)
		log.Print(latency)

		// access the status we are sending
		status := c.Writer.Status()
		log.Println(status)
	}
}

func main() {
	r := gin.New()
	r.Use(Logger())

	r.GET("/test", func(c *gin.Context) {
		example := c.MustGet("example").(string)

		// it would print: "12345"
		log.Println(example)
	})

	// Listen and serve on 0.0.0.0:8080
	r.Run(":8080")
}
```

### Using BasicAuth() middleware

```go
// simulate some private data
var secrets = gin.H{
	"foo":    gin.H{"email": "foo@bar.com", "phone": "123433"},
	"austin": gin.H{"email": "austin@example.com", "phone": "666"},
	"lena":   gin.H{"email": "lena@guapa.com", "phone": "523443"},
}

func main() {
	r := gin.Default()

	// Group using gin.BasicAuth() middleware
	// gin.Accounts is a shortcut for map[string]string
	authorized := r.Group("/admin", gin.BasicAuth(gin.Accounts{
		"foo":    "bar",
		"austin": "1234",
		"lena":   "hello2",
		"manu":   "4321",
	}))

	// /admin/secrets endpoint
	// hit "localhost:8080/admin/secrets
	authorized.GET("/secrets", func(c *gin.Context) {
		// get user, it was set by the BasicAuth middleware
		user := c.MustGet(gin.AuthUserKey).(string)
		if secret, ok := secrets[user]; ok {
			c.JSON(http.StatusOK, gin.H{"user": user, "secret": secret})
		} else {
			c.JSON(http.StatusOK, gin.H{"user": user, "secret": "NO SECRET :("})
		}
	})

	// Listen and serve on 0.0.0.0:8080
	r.Run(":8080")
}
```

### Goroutines inside a middleware

When starting new Goroutines inside a middleware or handler, you **SHOULD NOT** use the original context inside it, you have to use a read-only copy.

```go
func main() {
	r := gin.Default()

	r.GET("/long_async", func(c *gin.Context) {
		// create copy to be used inside the goroutine
		cCp := c.Copy()
		go func() {
			// simulate a long task with time.Sleep(). 5 seconds
			time.Sleep(5 * time.Second)

			// note that you are using the copied context "cCp", IMPORTANT
			log.Println("Done! in path " + cCp.Request.URL.Path)
		}()
	})

	r.GET("/long_sync", func(c *gin.Context) {
		// simulate a long task with time.Sleep(). 5 seconds
		time.Sleep(5 * time.Second)

		// since we are NOT using a goroutine, we do not have to copy the context
		log.Println("Done! in path " + c.Request.URL.Path)
	})

	// Listen and serve on 0.0.0.0:8080
	r.Run(":8080")
}
```

### Custom HTTP configuration

Use `http.ListenAndServe()` directly, like this:

```go
func main() {
	router := gin.Default()
	http.ListenAndServe(":8080", router)
}
```
or

```go
func main() {
	router := gin.Default()

	s := &http.Server{
		Addr:           ":8080",
		Handler:        router,
		ReadTimeout:    10 * time.Second,
		WriteTimeout:   10 * time.Second,
		MaxHeaderBytes: 1 << 20,
	}
	s.ListenAndServe()
}
```

### Support Let's Encrypt

example for 1-line LetsEncrypt HTTPS servers.

```go
package main

import (
	"log"

	"github.com/gin-gonic/autotls"
	"github.com/gin-gonic/gin"
)

func main() {
	r := gin.Default()

	// Ping handler
	r.GET("/ping", func(c *gin.Context) {
		c.String(200, "pong")
	})

	log.Fatal(autotls.Run(r, "example1.com", "example2.com"))
}
```

example for custom autocert manager.

```go
package main

import (
	"log"

	"github.com/gin-gonic/autotls"
	"github.com/gin-gonic/gin"
	"golang.org/x/crypto/acme/autocert"
)

func main() {
	r := gin.Default()

	// Ping handler
	r.GET("/ping", func(c *gin.Context) {
		c.String(200, "pong")
	})

	m := autocert.Manager{
		Prompt:     autocert.AcceptTOS,
		HostPolicy: autocert.HostWhitelist("example1.com", "example2.com"),
		Cache:      autocert.DirCache("/var/www/.cache"),
	}

	log.Fatal(autotls.RunWithManager(r, &m))
}
```

### Run multiple service using Gin

See the [question](https://github.com/gin-gonic/gin/issues/346) and try the following example:

```go
package main

import (
	"log"
	"net/http"
	"time"

	"github.com/gin-gonic/gin"
	"golang.org/x/sync/errgroup"
)

var (
	g errgroup.Group
)

func router01() http.Handler {
	e := gin.New()
	e.Use(gin.Recovery())
	e.GET("/", func(c *gin.Context) {
		c.JSON(
			http.StatusOK,
			gin.H{
				"code":  http.StatusOK,
				"error": "Welcome server 01",
			},
		)
	})

	return e
}

func router02() http.Handler {
	e := gin.New()
	e.Use(gin.Recovery())
	e.GET("/", func(c *gin.Context) {
		c.JSON(
			http.StatusOK,
			gin.H{
				"code":  http.StatusOK,
				"error": "Welcome server 02",
			},
		)
	})

	return e
}

func main() {
	server01 := &http.Server{
		Addr:         ":8080",
		Handler:      router01(),
		ReadTimeout:  5 * time.Second,
		WriteTimeout: 10 * time.Second,
	}

	server02 := &http.Server{
		Addr:         ":8081",
		Handler:      router02(),
		ReadTimeout:  5 * time.Second,
		WriteTimeout: 10 * time.Second,
	}

	g.Go(func() error {
		err := server01.ListenAndServe()
		if err != nil && err != http.ErrServerClosed {
			log.Fatal(err)
		}
		return err
	})

	g.Go(func() error {
		err := server02.ListenAndServe()
		if err != nil && err != http.ErrServerClosed {
			log.Fatal(err)
		}
		return err
	})

	if err := g.Wait(); err != nil {
		log.Fatal(err)
	}
}
```

### Graceful shutdown or restart

There are a few approaches you can use to perform a graceful shutdown or restart. You can make use of third-party packages specifically built for that, or you can manually do the same with the functions and methods from the built-in packages.

#### Third-party packages

We can use [fvbock/endless](https://github.com/fvbock/endless) to replace the default `ListenAndServe`. Refer to issue [#296](https://github.com/gin-gonic/gin/issues/296) for more details.

```go
router := gin.Default()
router.GET("/", handler)
// [...]
endless.ListenAndServe(":4242", router)
```

Alternatives:

* [manners](https://github.com/braintree/manners): A polite Go HTTP server that shuts down gracefully.
* [graceful](https://github.com/tylerb/graceful): Graceful is a Go package enabling graceful shutdown of an http.Handler server.
* [grace](https://github.com/facebookgo/grace): Graceful restart & zero downtime deploy for Go servers.

#### Manually

In case you are using Go 1.8 or a later version, you may not need to use those libraries. Consider using `http.Server`'s built-in [Shutdown()](https://golang.org/pkg/net/http/#Server.Shutdown) method for graceful shutdowns. The example below describes its usage, and we've got more examples using gin [here](https://github.com/gin-gonic/examples/tree/master/graceful-shutdown).

```go
// +build go1.8

package main

import (
	"context"
	"log"
	"net/http"
	"os"
	"os/signal"
	"syscall"
	"time"

	"github.com/gin-gonic/gin"
)

func main() {
	router := gin.Default()
	router.GET("/", func(c *gin.Context) {
		time.Sleep(5 * time.Second)
		c.String(http.StatusOK, "Welcome Gin Server")
	})

	srv := &http.Server{
		Addr:    ":8080",
		Handler: router,
	}

	// Initializing the server in a goroutine so that
	// it won't block the graceful shutdown handling below
	go func() {
		if err := srv.ListenAndServe(); err != nil && err != http.ErrServerClosed {
			log.Fatalf("listen: %s\n", err)
		}
	}()

	// Wait for interrupt signal to gracefully shutdown the server with
	// a timeout of 5 seconds.
	quit := make(chan os.Signal)
	// kill (no param) default send syscall.SIGTERM
	// kill -2 is syscall.SIGINT
	// kill -9 is syscall.SIGKILL but can't be catch, so don't need add it
	signal.Notify(quit, syscall.SIGINT, syscall.SIGTERM)
	<-quit
	log.Println("Shutting down server...")

	// The context is used to inform the server it has 5 seconds to finish
	// the request it is currently handling
	ctx, cancel := context.WithTimeout(context.Background(), 5*time.Second)
	defer cancel()
	if err := srv.Shutdown(ctx); err != nil {
		log.Fatal("Server forced to shutdown:", err)
	}
	
	log.Println("Server exiting")
}
```

### Build a single binary with templates

You can build a server into a single binary containing templates by using [go-assets][].

[go-assets]: https://github.com/jessevdk/go-assets

```go
func main() {
	r := gin.New()

	t, err := loadTemplate()
	if err != nil {
		panic(err)
	}
	r.SetHTMLTemplate(t)

	r.GET("/", func(c *gin.Context) {
		c.HTML(http.StatusOK, "/html/index.tmpl",nil)
	})
	r.Run(":8080")
}

// loadTemplate loads templates embedded by go-assets-builder
func loadTemplate() (*template.Template, error) {
	t := template.New("")
	for name, file := range Assets.Files {
		defer file.Close()
		if file.IsDir() || !strings.HasSuffix(name, ".tmpl") {
			continue
		}
		h, err := ioutil.ReadAll(file)
		if err != nil {
			return nil, err
		}
		t, err = t.New(name).Parse(string(h))
		if err != nil {
			return nil, err
		}
	}
	return t, nil
}
```

See a complete example in the `https://github.com/gin-gonic/examples/tree/master/assets-in-binary` directory.

### Bind form-data request with custom struct

The follow example using custom struct:

```go
type StructA struct {
    FieldA string `form:"field_a"`
}

type StructB struct {
    NestedStruct StructA
    FieldB string `form:"field_b"`
}

type StructC struct {
    NestedStructPointer *StructA
    FieldC string `form:"field_c"`
}

type StructD struct {
    NestedAnonyStruct struct {
        FieldX string `form:"field_x"`
    }
    FieldD string `form:"field_d"`
}

func GetDataB(c *gin.Context) {
    var b StructB
    c.Bind(&b)
    c.JSON(200, gin.H{
        "a": b.NestedStruct,
        "b": b.FieldB,
    })
}

func GetDataC(c *gin.Context) {
    var b StructC
    c.Bind(&b)
    c.JSON(200, gin.H{
        "a": b.NestedStructPointer,
        "c": b.FieldC,
    })
}

func GetDataD(c *gin.Context) {
    var b StructD
    c.Bind(&b)
    c.JSON(200, gin.H{
        "x": b.NestedAnonyStruct,
        "d": b.FieldD,
    })
}

func main() {
    r := gin.Default()
    r.GET("/getb", GetDataB)
    r.GET("/getc", GetDataC)
    r.GET("/getd", GetDataD)

    r.Run()
}
```

Using the command `curl` command result:

```
$ curl "http://localhost:8080/getb?field_a=hello&field_b=world"
{"a":{"FieldA":"hello"},"b":"world"}
$ curl "http://localhost:8080/getc?field_a=hello&field_c=world"
{"a":{"FieldA":"hello"},"c":"world"}
$ curl "http://localhost:8080/getd?field_x=hello&field_d=world"
{"d":"world","x":{"FieldX":"hello"}}
```

### Try to bind body into different structs

The normal methods for binding request body consumes `c.Request.Body` and they
cannot be called multiple times.

```go
type formA struct {
  Foo string `json:"foo" xml:"foo" binding:"required"`
}

type formB struct {
  Bar string `json:"bar" xml:"bar" binding:"required"`
}

func SomeHandler(c *gin.Context) {
  objA := formA{}
  objB := formB{}
  // This c.ShouldBind consumes c.Request.Body and it cannot be reused.
  if errA := c.ShouldBind(&objA); errA == nil {
    c.String(http.StatusOK, `the body should be formA`)
  // Always an error is occurred by this because c.Request.Body is EOF now.
  } else if errB := c.ShouldBind(&objB); errB == nil {
    c.String(http.StatusOK, `the body should be formB`)
  } else {
    ...
  }
}
```

For this, you can use `c.ShouldBindBodyWith`.

```go
func SomeHandler(c *gin.Context) {
  objA := formA{}
  objB := formB{}
  // This reads c.Request.Body and stores the result into the context.
  if errA := c.ShouldBindBodyWith(&objA, binding.JSON); errA == nil {
    c.String(http.StatusOK, `the body should be formA`)
  // At this time, it reuses body stored in the context.
  } else if errB := c.ShouldBindBodyWith(&objB, binding.JSON); errB == nil {
    c.String(http.StatusOK, `the body should be formB JSON`)
  // And it can accepts other formats
  } else if errB2 := c.ShouldBindBodyWith(&objB, binding.XML); errB2 == nil {
    c.String(http.StatusOK, `the body should be formB XML`)
  } else {
    ...
  }
}
```

* `c.ShouldBindBodyWith` stores body into the context before binding. This has
a slight impact to performance, so you should not use this method if you are
enough to call binding at once.
* This feature is only needed for some formats -- `JSON`, `XML`, `MsgPack`,
`ProtoBuf`. For other formats, `Query`, `Form`, `FormPost`, `FormMultipart`,
can be called by `c.ShouldBind()` multiple times without any damage to
performance (See [#1341](https://github.com/gin-gonic/gin/pull/1341)).

### http2 server push

http.Pusher is supported only **go1.8+**. See the [golang blog](https://blog.golang.org/h2push) for detail information.

```go
package main

import (
	"html/template"
	"log"

	"github.com/gin-gonic/gin"
)

var html = template.Must(template.New("https").Parse(`
<html>
<head>
  <title>Https Test</title>
  <script src="/assets/app.js"></script>
</head>
<body>
  <h1 style="color:red;">Welcome, Ginner!</h1>
</body>
</html>
`))

func main() {
	r := gin.Default()
	r.Static("/assets", "./assets")
	r.SetHTMLTemplate(html)

	r.GET("/", func(c *gin.Context) {
		if pusher := c.Writer.Pusher(); pusher != nil {
			// use pusher.Push() to do server push
			if err := pusher.Push("/assets/app.js", nil); err != nil {
				log.Printf("Failed to push: %v", err)
			}
		}
		c.HTML(200, "https", gin.H{
			"status": "success",
		})
	})

	// Listen and Server in https://127.0.0.1:8080
	r.RunTLS(":8080", "./testdata/server.pem", "./testdata/server.key")
}
```

### Define format for the log of routes

The default log of routes is:
```
[GIN-debug] POST   /foo                      --> main.main.func1 (3 handlers)
[GIN-debug] GET    /bar                      --> main.main.func2 (3 handlers)
[GIN-debug] GET    /status                   --> main.main.func3 (3 handlers)
```

If you want to log this information in given format (e.g. JSON, key values or something else), then you can define this format with `gin.DebugPrintRouteFunc`.
In the example below, we log all routes with standard log package but you can use another log tools that suits of your needs.
```go
import (
	"log"
	"net/http"

	"github.com/gin-gonic/gin"
)

func main() {
	r := gin.Default()
	gin.DebugPrintRouteFunc = func(httpMethod, absolutePath, handlerName string, nuHandlers int) {
		log.Printf("endpoint %v %v %v %v\n", httpMethod, absolutePath, handlerName, nuHandlers)
	}

	r.POST("/foo", func(c *gin.Context) {
		c.JSON(http.StatusOK, "foo")
	})

	r.GET("/bar", func(c *gin.Context) {
		c.JSON(http.StatusOK, "bar")
	})

	r.GET("/status", func(c *gin.Context) {
		c.JSON(http.StatusOK, "ok")
	})

	// Listen and Server in http://0.0.0.0:8080
	r.Run()
}
```

### Set and get a cookie

```go
import (
    "fmt"

    "github.com/gin-gonic/gin"
)

func main() {

    router := gin.Default()

    router.GET("/cookie", func(c *gin.Context) {

        cookie, err := c.Cookie("gin_cookie")

        if err != nil {
            cookie = "NotSet"
            c.SetCookie("gin_cookie", "test", 3600, "/", "localhost", false, true)
        }

        fmt.Printf("Cookie value: %s \n", cookie)
    })

    router.Run()
}
```


## Testing

The `net/http/httptest` package is preferable way for HTTP testing.

```go
package main

func setupRouter() *gin.Engine {
	r := gin.Default()
	r.GET("/ping", func(c *gin.Context) {
		c.String(200, "pong")
	})
	return r
}

func main() {
	r := setupRouter()
	r.Run(":8080")
}
```

Test for code example above:

```go
package main

import (
	"net/http"
	"net/http/httptest"
	"testing"

	"github.com/stretchr/testify/assert"
)

func TestPingRoute(t *testing.T) {
	router := setupRouter()

	w := httptest.NewRecorder()
	req, _ := http.NewRequest("GET", "/ping", nil)
	router.ServeHTTP(w, req)

	assert.Equal(t, 200, w.Code)
	assert.Equal(t, "pong", w.Body.String())
}
```

## Users

Awesome project lists using [Gin](https://github.com/gin-gonic/gin) web framework.

* [gorush](https://github.com/appleboy/gorush): A push notification server written in Go.
* [fnproject](https://github.com/fnproject/fn): The container native, cloud agnostic serverless platform.
* [photoprism](https://github.com/photoprism/photoprism): Personal photo management powered by Go and Google TensorFlow.
* [krakend](https://github.com/devopsfaith/krakend): Ultra performant API Gateway with middlewares.
* [picfit](https://github.com/thoas/picfit): An image resizing server written in Go.
* [brigade](https://github.com/brigadecore/brigade): Event-based Scripting for Kubernetes.
* [dkron](https://github.com/distribworks/dkron): Distributed, fault tolerant job scheduling system.

