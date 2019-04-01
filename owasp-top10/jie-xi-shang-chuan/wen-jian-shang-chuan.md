# 上传漏洞 -- [上传漏洞总结](https://www.andseclab.com/2018/12/01/%E4%B8%8A%E4%BC%A0%E6%BC%8F%E6%B4%9E%E6%94%BB%E5%87%BB%E6%80%BB%E7%BB%93/)、[上传漏洞技巧](https://blog.csdn.net/a15803617402/article/details/83003152)
###0x00 Burpsuite报文解释
![](/assets/165BC275DAF6A223E3B8A8BCAE7406E5.jpg)
###0x01 前端检测绕过
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;客户端检测绕过 -- 一般只检测文件扩展名
![](/assets/26CCFF8A03E5D2EDBECC3D73EEDC8E9E.png)
![](/assets/39B17F43ECC2EBBE50BE035F68CC111F.jpg)
![](/assets/EA98209121D004407CB454136B638AC8.png)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**也可以找到控制函数，将文件后缀添加上去进行绕过**
###0x02 服务端检测绕过
![](/assets/CFCAF2D29537149133FA48782BC548AB.png)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1.MIME类型检测绕过 -- 利用上传文件扩展名白名单，Content-Type修改
![](/assets/EECBADAFDDE510A581B45435073EF64F.png)
![](/assets/D0AFD54E7643628E868252C9AAA34BE0.png)
![](/assets/B99492B429E94D7ADA75FC00C460B902.png)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.文件内容检测绕过 -- 画板生成 1*1px 的图像
![](/assets/364D4AAB3C4557E8BE2152DE8A842832.png)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**也可以先上传一张正常图片，抓包后，在文件内容代码末尾添加一句话木马**
![](/assets/WX20190401-112025@2x.png)
![](/assets/B4369CB0B82E4DD61EBACD785FD59CBC.png)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3.文件参数检测绕过 -- 添加多个 filename 属性绕过扩展名拦截
![](/assets/E61BBEFA96F807CBC994888B2145F8B2.png)
###0x03 其他绕过技巧
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1.目录穿越绕过 -- 403、目录可控情况下，每一层目录测试
![](/assets/347A990B43ED15FA221D46C4CA549D92.png)
![](/assets/D0A43F246125AADC3154BC5A7858DD6C.jpg)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.扩展名检测类型可控 -- 黑白名单
![](/assets/WX20190401-133031@2x.png)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**1.利用 windows 不区分大小写特性，在上传时候将文件后缀名大小写或者大小写混合**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**2.不常见的后缀名**
![![](/assets/WX20190401-115559@2x.pn](/assets/WX20190401-115730@2x.png)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**3.截断漏洞**
![](/assets/WX20190401-132149@2x.png)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**4.%00截断**
![](/assets/WX20190401-132640@2x.png)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**5.特殊字符截断**
![](/assets/WX20190401-132803@2x.png)
###0x04 补充不常见后缀
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;PHP: .php2、php1、.phtml、.pht、.pHp、.pHp5、.pHtml
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JSP: .jspa、.jsw、.jsv、.jspf、.jtml、.jSp
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ASP/ASPX: .asax、.ascx、.asmx、.aSp、aSpx、cEr、sWf














