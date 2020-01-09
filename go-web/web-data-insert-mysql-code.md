```go
package main

import (
	"fmt"
	"log"
	"net/http"

	"database/sql"
	_ "github.com/go-sql-driver/mysql"
)

// 提交表单页面  点击提交 转到  /page 页面  执行 /page 对应的处理函数  getData
var indexHTML = `<html>
<head>
<meta http-equiv="Content-type" content="text/html; charset=utf-8">
<title>测试</title>
</head>
<body>


<form action="/page" method="post">
hostname：<br>
<input name="hostname" type="text"><br>
hostip：<br>
<textarea name="hostip"></textarea><br>
<input type="submit" value="提交">
</form>


</body>
</html>`

// 用于将页面重定向到主页
var redirectHTML = `<html>
<head>
<meta http-equiv="Content-type" content="text/html; charset=utf-8">
<meta http-equiv="Refresh" content="0; url={{.}}">
</head>
<body></body>
</html>`

// 访问 /       返回页面indexHTML 中的内容
func index(w http.ResponseWriter, r *http.Request) {
	// 向客户端写入我们准备好的页面
	fmt.Fprintf(w, indexHTML)
}

// 处理客户端提交的数据
func getData(w http.ResponseWriter, r *http.Request) {
	// 我们规定必须通过 POST 提交数据
	if r.Method == "POST" {
		// 解析客户端请求的信息
		if err := r.ParseForm(); err != nil {
			log.Println(err)
		}
		// 获取客户端输入的内容
		hostName := r.Form.Get("hostname")
		hostIp := r.Form.Get("hostip")

		db, _ := sql.Open("mysql", "webuser:123456@tcp(127.0.0.1:3306)/test?charset=utf8")

		stmt, _ := db.Prepare(`INSERT host (host,ip) values (?,?)`)
		_, _ = stmt.Exec(hostName, hostIp)
		defer db.Close()

	} else {
		// 如果不是通过 POST 提交的数据，则将页面重定向到主页
		fmt.Fprintf(w, redirectHTML)
	}
}

func main() {
	http.HandleFunc("/", index)            // 设置访问的路由
	http.HandleFunc("/page", getData)      // 设置访问的路由
	err := http.ListenAndServe(":80", nil) // 设置监听的端口
	if err != nil {
		log.Fatal("ListenAndServe: ", err)
	}
}
```
