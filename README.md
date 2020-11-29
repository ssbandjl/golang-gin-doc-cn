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

本文基于Golang Gin框架[官方文档](https://github.com/gin-gonic/gin)翻译, 验证了其中大部分示例代码, 便于Gin快速入门, 也欢迎大家提出意见, 一起交流学习.

本文地址: https://github.com/ssbandjl/golang-gin-doc-cn

Gin是Golang写的Web框架, 功能类似另一个Go框架[Martini](https://github.com/go-martini/martini)(暂停维护), Gin内部使用定制版本的[httprouter](https://github.com/julienschmidt/httprouter)(一款轻量级高性能HTTP请求路由器,或叫多路复用器), 速度是Martini的40倍, Gin拥有强大的性能,高效率,以及可扩展性, 所以赶快用起来吧!

## 云原生

更多云原生相关技术干货, 欢迎大家关注我的微信公众号:**云原生云**

![云原生云二维码](img/云原生云二维码大.gif)

## 内容

- [GinWeb框架](#GinWeb框架)
  - [内容](#内容)
  - [安装](#安装)
  - [快速开始](#快速开始)
  - [基准测试](#基准测试)
  - [GinV1稳定版](#GinV1稳定版)
  - [使用jsoniter编译](#使用jsoniter编译)
  - [API示例](#API示例)
    - [使用GET,POST,PUT,PATCH,DELETE,OPTIONS](#使用GET,POST,PUT,PATCH,DELETE,OPTIONS)
    - [获取请求中的路径参数](#获取请求中的路径参数)
    - [获取查询字符串参数](#获取查询字符串参数)
    - [获取Multipart/Urlencoded类型表单](#获取Multipart/Urlencoded类型表单)
    - [另一个示例,查询参数和Post表单](#另一个示例,查询参数和Post表单)
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
    - [XML,JSON,YAML,ProtoBuf等渲染](#XML,JSON,YAML,ProtoBuf等渲染)
      - [安全的JSON](#安全的JSON)
      - [JSONP](#jsonp)
      - [AsciiJSON](#asciijson)
      - [不带转义的原始JSON](#不带转义的原始JSON)
    - [静态文件服务](#静态文件服务)
    - [返回文件数据](#返回文件数据)
    - [用文件读出器提供文件数据服务](#用文件读出器提供文件数据服务)
    - [HTML渲染](#HTML渲染)
      - [自定义模板渲染器](#自定义模板渲染器)
      - [自定义分隔符](#自定义分隔符)
      - [自定义模板方法](#自定义模板方法)
    - [多个模板](#多个模板)
    - [重定向](#重定向)
    - [自定义中间件](#自定义中间件)
    - [使用基本认证BasicAuth()中间件](#使用基本认证BasicAuth()中间件)
    - [在中间件中使用协程Goroutines](#在中间件中使用协程Goroutines)
    - [自定义HTTP配置](#自定义HTTP配置)
    - [支持Let'sEncrypt证书加密处理HTTPS](#支持Let'sEncrypt证书加密处理HTTPS)
    - [使用Gin运行多个服务](#使用Gin运行多个服务)
    - [优雅的关闭和重启服务](#优雅的关闭和重启服务)
      - [使用第三方包](#使用第三方包)
      - [手动实现](#手动实现)
    - [将模板文件一起编译为一个二进制单文件](#将模板文件一起编译为一个二进制单文件)
    - [使用自定义的结构绑定请求表单](#使用自定义的结构绑定请求表单)
    - [尝试将请求体绑定到不同的结构](#尝试将请求体绑定到不同的结构)
    - [http2服务推送](#http2服务推送)
    - [定义路由日志格式](#定义路由日志格式)
    - [设置和读取Cookie](#设置和读取Cookie)
  - [测试](#测试)
  - [Gin框架用户](#Gin框架用户)

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

## GinV1稳定版

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

## API示例

你可以访问源码, 查看更多接口示例代码 [Gin示例仓库](https://github.com/gin-gonic/examples).

### 使用GET,POST,PUT,PATCH,DELETE,OPTIONS

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

### 另一个示例,查询参数和Post表单

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

### XML,JSON,YAML,ProtoBuf等渲染

```go
package main

import (
	"github.com/gin-gonic/gin"
	"github.com/gin-gonic/gin/testdata/protoexample"
	"net/http"
)

func main() {
	r := gin.Default()

	// gin.H is a shortcut for map[string]interface{}
	// gin.H对象是一个map映射,键名为字符串类型, 键值是接口,所以可以传递所有的类型
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

		//JSON serializes the given struct as JSON into the response body. It also sets the Content-Type as "application/json".
		//JSON方法将给定的结构序列化为JSON到响应体, 并设置内容类型Content-Type为:"application/json"
		c.JSON(http.StatusOK, msg)
	})

	r.GET("/someXML", func(c *gin.Context) {
		c.XML(http.StatusOK, gin.H{"message": "hey", "status": http.StatusOK})
	})

	r.GET("/someYAML", func(c *gin.Context) {
		c.YAML(http.StatusOK, gin.H{"message": "hey", "status": http.StatusOK})
	})

	//Protocol buffers are a language-neutral, platform-neutral extensible mechanism for serializing structured data.
	//Protocol buffers(简称ProtoBuf)是来自Google的一个跨语言,跨平台,用于将结构化数据序列化的可扩展机制,
	//详见:https://developers.google.com/protocol-buffers
	r.GET("/someProtoBuf", func(c *gin.Context) {
		reps := []int64{int64(1), int64(2)}
		label := "test"
		// The specific definition of protobuf is written in the testdata/protoexample file.
		// 使用protoexample.Test这个特别的protobuf结构来定义测试数据
		data := &protoexample.Test{
			Label: &label,
			Reps:  reps,
		}
		// Note that data becomes binary data in the response  //将data序列化为二进制的响应数据
		// Will output protoexample.Test protobuf serialized data
		// ProtoBuf serializes the given struct as ProtoBuf into the response body.
		// ProtoBuf方法将给定的结构序列化为ProtoBuf响应体
		c.ProtoBuf(http.StatusOK, data)
	})

	// Listen and serve on 0.0.0.0:8080
	r.Run(":8080")
}

/*
模拟测试
curl http://localhost:8080/someJSON
{"message":"hey","status":200}

curl http://localhost:8080/moreJSON
{"user":"Lena","Message":"hey","Number":123}

curl http://localhost:8080/someXML
<map><message>hey</message><status>200</status></map>

curl http://localhost:8080/someYAML
message: hey
status: 200

curl http://localhost:8080/someProtoBuf
test
*/
```

#### 安全的JSON

使用SecureJSON方法保护Json不被劫持, 如果响应体是一个数组, 该方法会默认添加`while(1)`前缀到响应头,  这样的死循环可以防止后面的代码被恶意执行, 也可以自定义安全JSON的前缀.

```go
package main

import (
	"github.com/gin-gonic/gin"
	"net/http"
)

func main() {
	r := gin.Default()

	// You can also use your own secure json prefix
	// 你也可以自定义安全Json的前缀
	r.SecureJsonPrefix(")]}',\n")

	//使用SecureJSON方法保护Json不被劫持, 如果响应体是一个数组, 该方法会默认添加`while(1)`前缀到响应头,  这样的死循环可以防止后面的代码被恶意执行, 也可以自定义安全JSON的前缀.
	r.GET("/someJSON", func(c *gin.Context) {
		names := []string{"lena", "austin", "foo"}

		//names := map[string]string{
		//	"hello": "world",
		//}

		// Will output  :   while(1);["lena","austin","foo"]
		c.SecureJSON(http.StatusOK, names)
	})

	// Listen and serve on 0.0.0.0:8080
	r.Run(":8080")
}

/*
模拟请求:curl http://localhost:8080/someJSON
)]}',
["lena","austin","foo"]%
*/
```
#### JSONP

使用JSONP可以实现跨域请求数据, 如果请求中有查询字符串参数callback, 则将返回数据作为参数传递给callback值(前端函数名),整体作为一个响应体,返回给前端.

JSONP是服务器与客户端跨源通信的常用方法. 最大特点就是简单适用, 老式浏览器全部支持, 服务器改造非常小, 它的基本思想是: 网页通过添加一个<script>元素, 向服务器请求JSON数据, 这种做法不受同源政策限制, 服务器收到请求后, 将数据放在一个指定名字的回调函数里传回来, 这样, 前端可以完成一次前端函数的调用, 而参数是后端返回的数据.

注意: 这种方式存在被劫持的风险

```go
package main

import (
	"github.com/gin-gonic/gin"
	"net/http"
)

func main() {
	r := gin.Default()

	r.GET("/JSONP", func(c *gin.Context) {
		data := gin.H{
			"foo": "bar",
		}

		//callback is x
		// Will output  :   x({\"foo\":\"bar\"})
		// 使用JSONP可以实现跨域请求数据, 如果请求中有查询字符串参数callback, 则将返回数据作为参数传递给callback值(前端函数名),整体作为一个响应体,返回给前端
		//JSONP是服务器与客户端跨源通信的常用方法。最大特点就是简单适用，老式浏览器全部支持，服务器改造非常小。
		//它的基本思想是，网页通过添加一个<script>元素，向服务器请求JSON数据，这种做法不受同源政策限制；服务器收到请求后，将数据放在一个指定名字的回调函数里传回来
		c.JSONP(http.StatusOK, data)
	})

	// Listen and serve on 0.0.0.0:8080
	r.Run(":8080")

	// 模拟客户端,请求参数中有callback参数,值为x(前端函数名),最后响应内容为x("foo":"bar")
	// curl http://127.0.0.1:8080/JSONP?callback=x
}
```

#### AsciiJSON

使用ASCII编码, 将非ASCII的字符进行转义和编码, 生成纯ASCII编码的JSON

```go
package main

import (
	"github.com/gin-gonic/gin"
	"net/http"
)

func main() {
	r := gin.Default()

	r.GET("/someJSON", func(c *gin.Context) {
		data := gin.H{
			"lang": "GO语言",
			"tag":  "<br>",
		}

		// 输出结果 : {"lang":"GO\u8bed\u8a00","tag":"\u003cbr\u003e"}
		// AsciiJSON方法返回带有Unicode编码和转义组成的纯ASCII字符串
		c.AsciiJSON(http.StatusOK, data)
	})

	// Listen and serve on 0.0.0.0:8080
	r.Run(":8080")
}

/*
模拟请求:curl http://localhost:8080/someJSON
 */
```

#### 不带转义的原始JSON

通常, JSON会将特殊的HTML字符转化为他们的unicode编码, 如标签`<`转为`\u003c` 使用PureJSON方法可以得到原始不做转义的字符串.

注意: 该方法至少需要Go版本1.6以上

```go
package main

import "github.com/gin-gonic/gin"

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
/*
模拟请求,得到将HTML标签转义后的JSON字符串
curl http://localhost:8080/json
{"html":"\u003cb\u003eHello, world!\u003c/b\u003e"}                                                                                                                                                                           
得到原始JSON字符串
curl http://localhost:8080/purejson
{"html":"<b>Hello, world!</b>"}
*/
```

### 静态文件服务

```go
package main

import (
	"github.com/gin-gonic/gin"
	"log"
	"net/http"
	"os"
)

func main() {
	router := gin.Default()
	cwd, _ := os.Getwd()  //获取当前文件目录
	log.Printf("当前项目路径:%s", cwd)
	router.Static("/static", cwd) //提供静态文件服务器, 第一个参数为相对路径,第二个参数为根路径, 这个路径一般放置css,js,fonts等静态文件,前端html中采用/static/js/xxx或/static/css/xxx等相对路径的方式引用
	router.StaticFS("/more_static", http.Dir("./")) //将本地文件树结构映射到前端, 通过浏览器可以访问本地文件系统, 模拟访问:http://localhost:8080/more_static
	router.StaticFile("/logo.png", "./resources/logo.png")  //StaticFile提供单静态单文件服务, 模拟访问:http://localhost:8080/log.png

	// Listen and serve on 0.0.0.0:8080
	router.Run(":8080")
}
```

### 返回文件数据

```go
package main

import (
	"github.com/gin-contrib/cors"
	"github.com/gin-gonic/gin"
	"net/http"
)

func main() {
	router := gin.Default()
	router.Use(cors.Default())

	router.GET("/local/file", func(c *gin.Context) {
		c.File("./main.go")
	})


	// A FileSystem implements access to a collection of named files.
	// The elements in a file path are separated by slash ('/', U+002F)
	// characters, regardless of host operating system convention.
	// FileSystem接口, 要求实现文件的访问的方法, 提供文件访问服务根路径的HTTP处理器
	var fs http.FileSystem = http.Dir("./")  //将本地目录作为文件服务根路径
	router.GET("/fs/file", func(c *gin.Context) {
		c.FileFromFS("main.go", fs)  //将文件服务系统下的文件数据返回
	})
	router.Run(":8080")
}
/*
模拟访问文件数据:
curl http://localhost:8080/local/file

模拟访问文件系统下的文件数据:
curl http://localhost:8080/fs/file
*/
```

### 用文件读出器提供文件数据服务

```go
package main

import (
	"github.com/gin-gonic/gin"
	"net/http"
)

func main() {
	router := gin.Default()
	router.GET("/someDataFromReader", func(c *gin.Context) {
		response, err := http.Get("https://raw.githubusercontent.com/gin-gonic/logo/master/color.png")
		if err != nil || response.StatusCode != http.StatusOK {  //请求链接中的文件出现错误时, 直接返回服务不可用
			c.Status(http.StatusServiceUnavailable)
			return
		}

		reader := response.Body  //用响应体内容构造一个文件读出器
		defer reader.Close()
		contentLength := response.ContentLength
		contentType := response.Header.Get("Content-Type")

		extraHeaders := map[string]string{
			"Content-Disposition": `attachment; filename="gopher.png"`,
		}
		// DataFromReader writes the specified reader into the body stream and updates the HTTP code.
		// func (c *Context) DataFromReader(code int, contentLength int64, contentType string, reader io.Reader, extraHeaders map[string]string) {}
		// DataFromReader方法将指定的读出器reader中的内容, 写入http响应体流中, 并更新响应码, 响应头信息等
		c.DataFromReader(http.StatusOK, contentLength, contentType, reader, extraHeaders)
	})
	router.Run(":8080")
}
/*
模拟访问:
curl http://localhost:8080/someDataFromReader
*/
```

### HTML渲染

使用LoadHTMLGlob()方法或LoadHTMLFiles()方法

```go
package main

import (
	"github.com/gin-gonic/gin"
	"net/http"
)

func main() {
	router := gin.Default()
	//LoadHTMLGlob方法以glob模式加载匹配的HTML文件, 并与HTML渲染器结合
	router.LoadHTMLGlob("templates/*")
	//router.LoadHTMLFiles("templates/template1.html", "templates/template2.html")
	router.GET("/index", func(c *gin.Context) {
		//HTML方法设置响应码, 模板文件名, 渲染替换模板中的值, 设置响应内容类型Content-Type "text/html"
		c.HTML(http.StatusOK, "index.tmpl", gin.H{
			"title": "Main website",
		})
	})
	router.Run(":8080")
}
/*
模拟测试:
curl http://localhost:8080/index
*/
```

增加模板文件, templates/index.tmpl

```html
<html>
	<h1>
		{{ .title }}
	</h1>
</html>
```

使用不同文件夹下的相同文件名的模板文件

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

posts目录下添加模板文件, templates/posts/index.tmpl

```html
{{ define "posts/index.tmpl" }}
<html><h1>
	{{ .title }}
</h1>
<p>Using posts/index.tmpl</p>
</html>
{{ end }}
```

users目录下添加模板文件, templates/users/index.tmpl

```html
{{ define "users/index.tmpl" }}
<html><h1>
	{{ .title }}
</h1>
<p>Using users/index.tmpl</p>
</html>
{{ end }}
```

#### 自定义模板渲染器

你也可以使用你自定义的HTML模板渲染器, 需要自定义模板文件file1, file2等

```go
package main

import (
	"github.com/gin-gonic/gin"
	"html/template"
	"net/http"
)

func main() {
	router := gin.Default()
	//template.ParseFiles(文件1,文件2...)创建一个模板对象, 然后解析一组模板，使用文件名作为模板的名字
	// Must方法将模板和错误进行包裹, 返回模板的内存地址 一般用于变量初始化,比如:var t = template.Must(template.New("name").Parse("html"))
	html := template.Must(template.ParseFiles("file1", "file2"))
	router.SetHTMLTemplate(html) //关联模板和HTML渲染器

	router.GET("/index", func(c *gin.Context) {
		//HTML方法设置响应码, 模板文件名, 渲染替换模板中的值, 设置响应内容类型Content-Type "text/html"
		c.HTML(http.StatusOK, "file1", gin.H{
			"title": "Main website",
		})
	})
	router.Run(":8080")
}
```

#### 自定义分隔符

你可以自定义分隔符, 模板中默认的分隔符是{{  }}, 我们也可以修改, 比如下面增加一对中括号

```go
	r := gin.Default()
	r.Delims("{[{", "}]}")
	r.LoadHTMLGlob("/path/to/templates")
```

#### 自定义模板方法

详见 [示例代码](https://github.com/gin-gonic/examples/tree/master/template).

模板中与后端都定义好模板方法, 模板渲染时执行该方法, 类似过滤器方法, 比如时间格式化操作

```go
package main

import (
	"fmt"
	"html/template"
	"net/http"
	"time"

	"github.com/gin-gonic/gin"
)

func formatAsDate(t time.Time) string {
	year, month, day := t.Date()  //Date方法返回年,月,日
	return fmt.Sprintf("%d%02d/%02d", year, month, day)  //格式化时间
}

func main() {
	router := gin.Default()
	router.Delims("{[{", "}]}") //自定义模板中的左右分隔符
	//SetFuncMap方法用给定的template.FuncMap设置到Gin引擎上, 后面模板渲染时会调用同名方法
	//FuncMap是一个map,键名关联方法名, 键值关联方法, 每个方法必须返回一个值, 或者返回两个值,其中第二个是error类型
	router.SetFuncMap(template.FuncMap{
		"formatAsDate": formatAsDate,
	})
	router.LoadHTMLFiles("./testdata/template/raw.tmpl") //加载单个模板文件并与HTML渲染器关联

	router.GET("/raw", func(c *gin.Context) {
		c.HTML(http.StatusOK, "raw.tmpl", gin.H{
			"now": time.Date(2017, 07, 01, 0, 0, 0, 0, time.UTC),
		})
	})

	router.Run(":8080")
}

/*
模拟测试:
curl http://localhost:8080/raw
*/
```

定义模板文件: raw.tmpl

```html
Date: {[{.now | formatAsDate}]}
```

时间格式化结果:
```
Date: 2017/07/01
```

### 多个模板

Gin默认只使用一个html.Template模板引擎, 也可以参考[多模板渲染器](https://github.com/gin-contrib/multitemplate)使用类似Go1.6的块级模板`block template`功能. 

模板相关详情请参考官方[template包](https://golang.org/pkg/text/template/)

### 重定向

Gin返回一个HTTP重定向非常简单, 使用Redirect方法即可. 内部和外部链接都支持.

```go
package main

import (
	"github.com/gin-gonic/gin"
	"net/http"
)

func main() {
	r := gin.Default()
	r.GET("/test", func(c *gin.Context) {
		c.Redirect(http.StatusMovedPermanently, "http://www.google.com/")  //重定向到外部链接
	})

	//重定向到内部链接
	r.GET("/internal", func(c *gin.Context) {
		c.Redirect(http.StatusMovedPermanently, "/home")
	})

	r.GET("/home", func(c *gin.Context) {
		c.JSON(200, gin.H{"msg": "这是首页"})
	})
	r.Run(":8080")
}

/*
重定向到外部链接,访问:http://localhost:8080/test
重定向到内部链接,访问:http://localhost:8080/internal
*/
```

从POST方法中完成HTTP重定向, 参考问题[#444](https://github.com/gin-gonic/gin/issues/444)

```go
r.POST("/test", func(c *gin.Context) {
	c.Redirect(http.StatusFound, "/foo")
})
```

如果要产生一个路由重定向, 类似上面的内部重定向, 则使用 `HandleContext`方法, 像下面这样使用:

``` go
r.GET("/test", func(c *gin.Context) {
    c.Request.URL.Path = "/test2"
    r.HandleContext(c)
})
r.GET("/test2", func(c *gin.Context) {
    c.JSON(200, gin.H{"hello": "world"})
})
```


### 自定义中间件

```go
package main

import (
	"github.com/gin-gonic/gin"
	"log"
	"time"
)

//自定义日志中间件
func Logger() gin.HandlerFunc {
	return func(c *gin.Context) {
		t := time.Now()

		// Set example variable 在gin上下文中设置键值对
		c.Set("example", "12345")

		// before request

		//Next方法只能用于中间件中,在当前中间件中, 从方法链执行挂起的处理器
		c.Next()

		// after request  打印中间件执行耗时
		latency := time.Since(t)
		log.Print(latency)

		// access the status we are sending  打印本中间件的状态码
		status := c.Writer.Status()
		log.Println(status)
	}
}

func main() {
	r := gin.New()
  //使用该自定义中间件
	r.Use(Logger())
	r.GET("/test", func(c *gin.Context) {
		example := c.MustGet("example").(string) //从上下文中获取键值对
		// it would print: "12345"
		log.Println(example)
	})

	// Listen and serve on 0.0.0.0:8080
	r.Run(":8080")
}
```

### 使用基本认证BasicAuth()中间件

```go
package main

import (
	"github.com/gin-gonic/gin"
	"net/http"
)

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
	// 路由组authorized使用基本认证中间件, 参数为gin.Accounts,是一个map,键名是用户名, 键值是密码, 该中间件会将认证信息保存到cookie中
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
		// 从cookie中获取用户认证信息, 键名为user
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
/*
测试访问:http://localhost:8080/admin/secrets
*/
```

### 在中间件中使用协程Goroutines

在中间件或者控制器中启动新协程时, 不能直接使用原来的Gin上下文, 必须使用一个只读的上下文副本

```go
package main

import (
	"github.com/gin-gonic/gin"
	"log"
	"time"
)

func main() {
	r := gin.Default()

	r.GET("/long_async", func(c *gin.Context) {
		// create copy to be used inside the goroutine
		// 创建一个Gin上下文的副本, 准备在协程Goroutine中使用
		cCp := c.Copy()
		go func() {
			// simulate a long task with time.Sleep(). 5 seconds
			// 模拟长时间任务,这里是5秒
			time.Sleep(5 * time.Second)

			// note that you are using the copied context "cCp", IMPORTANT
			// 在中间件或者控制器中启动协程时, 不能直接使用原来的上下文, 必须使用一个只读的上线文副本
			log.Println("Done! in path " + cCp.Request.URL.Path)
		}()
	})

	r.GET("/long_sync", func(c *gin.Context) {
		// simulate a long task with time.Sleep(). 5 seconds
		time.Sleep(5 * time.Second)

		// since we are NOT using a goroutine, we do not have to copy the context
		// 没有使用协程时, 可以直接使用Gin上下文
		log.Println("Done! in path " + c.Request.URL.Path)
	})

	// Listen and serve on 0.0.0.0:8080
	r.Run(":8080")
}
/*
模拟同步阻塞访问:http://localhost:8080/long_sync
模拟异步非阻塞访问:http://localhost:8080/long_async
*/
```

### 自定义HTTP配置

直接使用 `http.ListenAndServe()`方法:

```go
func main() {
	router := gin.Default()
	http.ListenAndServe(":8080", router)
}
```
或者自定义HTTP配置

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

### 支持Let'sEncrypt证书加密处理HTTPS

下面是一行式的LetsEncrypt HTTPS服务

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
	//一行式LetsEncrypt证书, 处理https
	log.Fatal(autotls.Run(r, "example1.com", "example2.com"))
}
```

自定义自动证书管理器autocert manager实例代码:

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
		Prompt:     autocert.AcceptTOS, //Prompt指定一个回调函数有条件的接受证书机构CA的TOS服务, 使用AcceptTOS总是接受服务条款
		HostPolicy: autocert.HostWhitelist("example1.com", "example2.com"),  //HostPolicy用于控制指定哪些域名, 管理器将检索新证书
		Cache:      autocert.DirCache("/var/www/.cache"),  //缓存证书和其他状态
	}

	log.Fatal(autotls.RunWithManager(r, &m))
}
```

详情参考[autotls包](https://github.com/gin-gonic/autotls)

### 使用Gin运行多个服务

可以在主函数中使用协程Goroutine运行多个服务, 每个服务端口不同, 路由分组也不同. 请参考这个[问题](https://github.com/gin-gonic/gin/issues/346),  尝试运行以下示例代码:

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

/*
模拟访问服务1:
curl http://localhost:8080/
{"code":200,"error":"Welcome server 01"}

模拟访问服务2:
curl http://localhost:8081/
{"code":200,"error":"Welcome server 02"}
*/
```

### 优雅的关闭和重启服务

有一些方法可以优雅的关闭或者重启服务, 比如不应该中断活动的连接, 需要优雅等待服务完成后才执行关闭或重启. 你可以使用第三方包来实现, 也可以使用内置的包自己实现优雅关闭或重启.

#### 使用第三方包

[fvbock/endless](https://github.com/fvbock/endless) 包, 可以实现Golang HTTP/HTTPS服务的零停机和优雅重启(Golang版本至少1.3以上)

我们可以使用[fvbock/endless](https://github.com/fvbock/endless) 替代默认的 `ListenAndServe`方法, 更多详情, 请参考问题[#296](https://github.com/gin-gonic/gin/issues/296).

```go
router := gin.Default()
router.GET("/", handler)
// [...]
endless.ListenAndServe(":4242", router)
```

其他替代包:

* [manners](https://github.com/braintree/manners): 一个优雅的Go HTTP服务, 可以优雅的关闭服务.
* [graceful](https://github.com/tylerb/graceful): 优雅的Go包, 能够优雅的关闭一个http.Handler服务
* [grace](https://github.com/facebookgo/grace): 该包为Go服务实现优雅重启, 零停机

#### 手动实现

如果你使用Go1.8或者更高的版本, 你可能不需要使用这些库. 可以考虑使用http.Server的内置方法[Shutdown()](https://golang.org/pkg/net/http/#Server.Shutdown)来优雅关闭服务. 下面的示例描述了基本用法, 更多示例请参考[这里](https://github.com/gin-gonic/examples/tree/master/graceful-shutdown)

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
	// 用协程初始化一个服务, 它不会阻塞下面的优雅逻辑处理
	go func() {
		if err := srv.ListenAndServe(); err != nil && err != http.ErrServerClosed {
			log.Fatalf("listen: %s\n", err)
		}
	}()

	// Wait for interrupt signal to gracefully shutdown the server with
	// a timeout of 5 seconds.
	//等待一个操作系统的中断信号, 来优雅的关闭服务
	quit := make(chan os.Signal)
	// kill (no param) default send syscall.SIGTERM  //kill会发送终止信号
	// kill -2 is syscall.SIGINT  //发送强制进程结束信号
	// kill -9 is syscall.SIGKILL but can't be catch, so don't need add it  //发送SIGKILL信号给进程
	signal.Notify(quit, syscall.SIGINT, syscall.SIGTERM)
	<-quit //阻塞在这里,直到获取到一个上面的信号
	log.Println("Shutting down server...")

	// The context is used to inform the server it has 5 seconds to finish
	// the request it is currently handling
	//这里使用context上下文包, 有5秒钟的处理超时时间
	ctx, cancel := context.WithTimeout(context.Background(), 5*time.Second)
	defer cancel()
	if err := srv.Shutdown(ctx); err != nil {  //利用内置Shutdown方法优雅关闭服务
		log.Fatal("Server forced to shutdown:", err)
	}

	log.Println("Server exiting")
}
```

### 将模板文件一起编译为一个二进制单文件

使用[go-assets][], 你可以将模板文件和服务一起编译为一个二进制的单文件, 可以方便快捷的部署该服务. 请参考go资产编译器[go-assets-builder](https://github.com/jessevdk/go-assets-builder)

使用方法:

```
1.下载依赖包
go get github.com/gin-gonic/gin
go get github.com/jessevdk/go-assets-builder

2.将html文件夹(包含html代码)生成为go资产文件assets.go
go-assets-builder html -o assets.go

3.编译构建,将服务打包为单二进制文件
go build -o assets-in-binary

4.运行服务
./assets-in-binary
```

go资产文件go-assets.go参考内容如下:

```go
package main

import (
	"time"

	"github.com/jessevdk/go-assets"
)

var _Assetsbfa8d115ce0617d89507412d5393a462f8e9b003 = "<!doctype html>\n<body>\n  <p>Can you see this? → {{.Bar}}</p>\n</body>\n"
var _Assets3737a75b5254ed1f6d588b40a3449721f9ea86c2 = "<!doctype html>\n<body>\n  <p>Hello, {{.Foo}}</p>\n</body>\n"

// Assets returns go-assets FileSystem
var Assets = assets.NewFileSystem(map[string][]string{"/": {"html"}, "/html": {"bar.tmpl", "index.tmpl"}}, map[string]*assets.File{
	"/": {
		Path:     "/",
		FileMode: 0x800001ed,
		Mtime:    time.Unix(1524365738, 1524365738517125470),
		Data:     nil,
	}, "/html": {
		Path:     "/html",
		FileMode: 0x800001ed,
		Mtime:    time.Unix(1524365491, 1524365491289799093),
		Data:     nil,
	}, "/html/bar.tmpl": {
		Path:     "/html/bar.tmpl",
		FileMode: 0x1a4,
		Mtime:    time.Unix(1524365491, 1524365491289611557),
		Data:     []byte(_Assetsbfa8d115ce0617d89507412d5393a462f8e9b003),
	}, "/html/index.tmpl": {
		Path:     "/html/index.tmpl",
		FileMode: 0x1a4,
		Mtime:    time.Unix(1524365491, 1524365491289995821),
		Data:     []byte(_Assets3737a75b5254ed1f6d588b40a3449721f9ea86c2),
	}}, "")
```

[go-assets]: https://github.com/jessevdk/go-assets

```go
package main

import (
	"github.com/gin-gonic/gin"
	"io/ioutil"
	"net/http"
	"strings"
	"html/template"

)

func main() {
	r := gin.New()

	t, err := loadTemplate() //加载go-assets-builder生成的模板
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
// 加载go-assets-builder生成的资产文件, 返回模板的地址
func loadTemplate() (*template.Template, error) {
	t := template.New("")
	for name, file := range Assets.Files {
		defer file.Close()
		if file.IsDir() || !strings.HasSuffix(name, ".tmpl") {  //跳过目录或没有.tmpl后缀的文件
			continue
		}
		h, err := ioutil.ReadAll(file)
		if err != nil {
			return nil, err
		}
		t, err = t.New(name).Parse(string(h))  //新建一个模板, 文件名做为模板名, 文件内容作为模板内容
		if err != nil {
			return nil, err
		}
	}
	return t, nil
}
```

完整示例请查看该[目录](https://github.com/gin-gonic/examples/tree/master/assets-in-binary)

### 使用自定义的结构绑定请求表单

参考实例代码:

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

使用命令 `curl` 模拟请求测试和结果如下:

```
$ curl "http://localhost:8080/getb?field_a=hello&field_b=world"
{"a":{"FieldA":"hello"},"b":"world"}
$ curl "http://localhost:8080/getc?field_a=hello&field_c=world"
{"a":{"FieldA":"hello"},"c":"world"}
$ curl "http://localhost:8080/getd?field_x=hello&field_d=world"
{"d":"world","x":{"FieldX":"hello"}}
```

### 尝试将请求体绑定到不同的结构

常规的方法绑定请求体是调用`c.Request.Body`, 但是它不能多次被调用

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
  // 使用c.ShoudBind消费c.Request.Body, 但是它只能调用一次
  if errA := c.ShouldBind(&objA); errA == nil {
    c.String(http.StatusOK, `the body should be formA`)
  // Always an error is occurred by this because c.Request.Body is EOF now.
  //这里会报错,因为c.Request.Body已经被消费, 会返回文件结束符EOF
  } else if errB := c.ShouldBind(&objB); errB == nil {
    c.String(http.StatusOK, `the body should be formB`)
  } else {
    ...
  }
}
```

为了解决这个问题, 可以使用`c.ShouldBindBodyWith`方法.

```go
func SomeHandler(c *gin.Context) {
  objA := formA{}
  objB := formB{}
  // This reads c.Request.Body and stores the result into the context.
  // c.ShouldBindBodyWith方法读取c.Request.Body,并且将结果存储到上下文
  if errA := c.ShouldBindBodyWith(&objA, binding.JSON); errA == nil {
    c.String(http.StatusOK, `the body should be formA`)
  // At this time, it reuses body stored in the context.
  //再次调用c.ShouldBindBodyWith时, 可以从上下文中复用请求体内容
  } else if errB := c.ShouldBindBodyWith(&objB, binding.JSON); errB == nil {
    c.String(http.StatusOK, `the body should be formB JSON`)
  // And it can accepts other formats 也可以接受其他类型的绑定,比如XML
  } else if errB2 := c.ShouldBindBodyWith(&objB, binding.XML); errB2 == nil {
    c.String(http.StatusOK, `the body should be formB XML`)
  } else {
    ...
  }
}
```

* `c.ShouldBindBodyWith` 该方法在绑定前, 将请求体存储到gin上下文中, 所以这会对性能有轻微的影响, 所以如果你只打算绑定一次的时候, 不应该使用该方法.
* 这种方式仅仅支持以下格式: `JSON`, `XML`, `MsgPack`,`ProtoBuf`. 对于其他格式, `Query`, `Form`, `FormPost`, `FormMultipart`, 可以重复使用`c.ShouldBind()`方法, 而不会带来类似的性能影响, 详见([#1341](https://github.com/gin-gonic/gin/pull/1341))

### http2服务推送

为了解决HTTP/1.X的网络资源利用率不够高, 延迟问题等, HTTP/2 引入了服务器推送机制来解决这些问题.

http.Pusher需要**go1.8+**版本支持. 详见[golang博客](https://blog.golang.org/h2push).

```go
package main

import (
	"html/template"
	"log"

	"github.com/gin-gonic/gin"
)

//定义html模板
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
		if pusher := c.Writer.Pusher(); pusher != nil { //获取推送器
			// use pusher.Push() to do server push
			// 使用pusher.Push()方法执行服务端推送动作, 尝试推送app.js文件
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

### 定义路由日志格式

默认路由日志如下:
```
[GIN-debug] POST   /foo                      --> main.main.func1 (3 handlers)
[GIN-debug] GET    /bar                      --> main.main.func2 (3 handlers)
[GIN-debug] GET    /status                   --> main.main.func3 (3 handlers)
```

如果你想用给定的格式(如:JSON,键值对等)记录路由日志, 你可以使用`gin.DebugPrintRouteFunc`方法自定义日志格式, 下面的示例, 我们用日志log标准库记录路由器日志, 当然你也可以使用其他适合业务的日志工具. 

```go
package main

import (
	"log"
	"net/http"

	"github.com/gin-gonic/gin"
)

func main() {
	r := gin.Default()
	//使用DebugPrintRouteFunc设置路由日志记录格式, 这里使用标准库log包记录请求方法/请求路径/控制器名/控制器链个数,
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

### 设置和读取Cookie

```go
import (
    "fmt"

    "github.com/gin-gonic/gin"
)

func main() {

    router := gin.Default()

    router.GET("/cookie", func(c *gin.Context) {
				//读取Cookie
        cookie, err := c.Cookie("gin_cookie")

        if err != nil {
            cookie = "NotSet"
          	//设置Cookie
            c.SetCookie("gin_cookie", "test", 3600, "/", "localhost", false, true)
        }

        fmt.Printf("Cookie value: %s \n", cookie)
    })

    router.Run()
}
```


## 测试

推荐使用`net/http/httptest` 包做HTTP测试.

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

测试代码示例:

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
  //断言
	assert.Equal(t, 200, w.Code)
	assert.Equal(t, "pong", w.Body.String())
}
```

## Gin框架用户

其他优质的项目也使用[Gin](https://github.com/gin-gonic/gin)Web框架.

* [gorush](https://github.com/appleboy/gorush): 一个用GO实现的推送通知系统
* [fnproject](https://github.com/fnproject/fn): 原生容器化, 无服务的跨云平台
* [photoprism](https://github.com/photoprism/photoprism): 使用Go和Google的TensorFlow框架支持的个人照片管理
* [krakend](https://github.com/devopsfaith/krakend): 带有中间件的极致高性能API网关
* [picfit](https://github.com/thoas/picfit): 使用Go实现的一款图片编辑服务器
* [brigade](https://github.com/brigadecore/brigade): 为Kubernetes服务的基于事件驱动的脚本
* [dkron](https://github.com/distribworks/dkron): 分布式, 可靠的任务调度系统



​                                                                                 😄都看到这里, 一定是真爱, 关注一个吧! 

![云原生云二维码](img/云原生云二维码大.gif)