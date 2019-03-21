# 其他注入法(下)
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x01 HTTP注入 [(详情)](https://www.cnblogs.com/softidea/p/5325079.html)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;原理: 利用HTTP协议头部未进行过滤检查进行注入
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;方法: XFF、UserAgent、[Cookie](https://www.jianshu.com/p/186ed9bf2951)(头文件)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1.X-Forwarded-For简称XFF头，它代表了客户端的真实IP，通过修改他的值就可以伪造客户端IP
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;利用burpsuite的抓包及Repeater模块进行测试攻击，或者抓包头部信息利用SQLMap进行检测攻击

```
    1.1 利用burpsuite+Repeater模块进行XFF检测攻击
        
        查库: X-Forwarded-for: 127.0.0.1' union select 1,2,database()#,常规查询手法
    1.2 利用burpsuite+sqlmap组合检测注入
        测试注入点，发现XFF返回IP，那么可能存在XFF注入，burp抓包，添加x-forwarded-for:*，将raw的信息存为txt文件
        利用burpsuite抓包出文件保存到 txt 文本中，再利用 SQLMap -r 文件 -D 等常规操作
      
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.User-agent记录软件程序的客户端信息的HTTP头字段，他可以用来统计目标和违规协议
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[报错注入法](https://www.jianshu.com/p/ee7f660295b1)、[延时注入法](https://www.freebuf.com/articles/web/105124.html)、SQLMap导入文件法
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x02 COOKIE注入(参数传递类型)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;原理:php中，使用超全局变 $_GET，$_POST来接受参数。 asp中，使用Request.QueryString (GET)或 Request.Form (POST)来接收页面提交的参数值，程序不是先取GET中的数据，没有再取POST中的数据，还会去取Cookies中的数据，一般写防护的会忽略cookie防御
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;方法: [cookie中转工具实战](https://blog.51cto.com/yttitan/1562382)、[cookie手注](https://www.cnblogs.com/sun-sunshine123/p/6861677.html)
```html
    javascript:alert（document.ｃookie ="id="+escape("1")); 回车弹出对话框内容为1
    刷新一下网页，如果正常显示，表示该页是用Request("ID")这样的格式收集数据，这种格式就可以试Cookies注入了
    
    SQLMap:  sqlmap.py -u "http://172.16.12.2/test.php" --cookie "id=1" --level 2  --level>2才会检查cookie
    
```
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x03 POST注入、搜索型注入
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[手工+SQLMap实战](https://www.jianshu.com/p/26b1576b37bb)、[Burpsuite+SQLMap实战](https://blog.csdn.net/u011781521/article/details/58594941)


```
    搜索型注入核心语法:a%’ and 1=1/2–，在搜索框内进行测试
    SQLMap则是先抓包成文件，利用 sqlmap -r 文件 -p

```
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x04 [编码参数(base64)](https://blog.csdn.net/qq_42357070/article/details/81512470)

```
    sqlmap -u "URL" --tamper base64encode --level=3 --current-db
    如果手工注入，配合小葵万能编码转换时，是要将整个参数和注入语句一起编码代入
```
















