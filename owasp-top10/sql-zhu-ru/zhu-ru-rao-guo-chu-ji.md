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
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;原理: %25=%
![](/assets/819D6BE3ABC9332640A198A04C59DBE3.png)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;方法:
![](/assets/F9F1EB8B18B34194EF8874D1070C3F1A.png)


