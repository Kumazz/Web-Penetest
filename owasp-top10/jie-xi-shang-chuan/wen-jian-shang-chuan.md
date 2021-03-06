# 上传漏洞 -- [上传漏洞总结](https://www.andseclab.com/2018/12/01/%E4%B8%8A%E4%BC%A0%E6%BC%8F%E6%B4%9E%E6%94%BB%E5%87%BB%E6%80%BB%E7%BB%93/)、[上传漏洞技巧](https://www.cnblogs.com/jinqi520/p/9977256.html)
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
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**4.特殊字符截断( ::$DATA 仅限 windows，还有 .php.空格. 绕过)**
![](/assets/WX20190401-132803@2x.png)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**5. .htaccess绕过**
![](/assets/WX20190401-165011@2x.png)

```
    创建任意文件
    文件内容为: SetHandler application/x-httpd-php
    文件另存为 .htaccess 即可，再上传任意文件即可当成 php 执行
    有时候系统无法保存 .htaccess 文件，可以先保存 任意名.htaccess 上传后通过bp改为 .htaccess，然后再上传木马文件
    
    或者先预设一个将要上传的木马文件改写文件规则
    <FilesMatch "自定义名称.jpg">
        SetHandler application/x-httpd-php
    </FilesMatch>	
    然后再上传一个 自定义名称.jpg，这样这个文件被当做php执行
```
###0x04 补充不常见后缀(混合大小写)--黑白名单
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;PHP: .php2、php1、.phtml、.pht、.pHp、.pHp5、.pHtml
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JSP: .jspa、.jsw、.jsv、.jspf、.jtml、.jSp
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ASP/ASPX: .asax、.ascx、.asmx、.aSp、aSpx、cEr、sWf
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;双写绕过: pphphp
###0x05 %00截断绕过
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**1.1 %00截断 GET 绕过 ( CVE-2015-2348 )**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;影响版本：5.4.x<= 5.4.39, 5.5.x<= 5.5.23, 5.6.x <= 5.6.7

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;exp：move_uploaded_file($_FILES['name']['tmp_name'],"/file.php\x00.jpg");源码中move_uploaded_file中的save_path可控，因此00截断即可
![](/assets/1442660-20181118205809473-913200603.png)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**1.2 %00截断 POST 绕过 (version<5.3.4,magic_quotes_gpc需要为OFF状态)**
![](/assets/WX20190402-145640@2x.png)
![](/assets/WX20190401-132640@2x.png)

















