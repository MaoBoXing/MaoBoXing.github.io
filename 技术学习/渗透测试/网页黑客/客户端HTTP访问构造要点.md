## GET

客户端从http://cookies.thm请求网页

```http
GET / HTTP/1.1
Host: cookies.thm
User-Agent:xxx
```

客户端发送携带COOKIE的请求

```http
GET / HTTP/1.1
Host: cookies.thm
User-Agent:xxx
Cookie:name=adam
```



## POST

客户端发送名称设置为adam的**表单**

```http
POST / HTTP/1.1	
Host: cookies.thm
User-Agent: xxx
Content-type:application/x-www-form-urlencoded
content-Length:9

name=adam
```

