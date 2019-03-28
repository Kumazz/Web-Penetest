# 文件上传
###0x00 Burpsuite报文解释
![](/assets/165BC275DAF6A223E3B8A8BCAE7406E5.jpg)
###0x01 前端检测绕过
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;客户端检测绕过 -- 一般只检测文件扩展名
![](/assets/26CCFF8A03E5D2EDBECC3D73EEDC8E9E.png)
![](/assets/39B17F43ECC2EBBE50BE035F68CC111F.jpg)
![](/assets/EA98209121D004407CB454136B638AC8.png)
###0x02 服务端检测绕过
![](/assets/CFCAF2D29537149133FA48782BC548AB.png)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1.MIME类型检测绕过 -- 利用上传文件扩展名白名单，Content-Type修改
![](/assets/EECBADAFDDE510A581B45435073EF64F.png)
![](/assets/D0AFD54E7643628E868252C9AAA34BE0.png)
![](/assets/B99492B429E94D7ADA75FC00C460B902.png)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.文件内容检测绕过 -- 画板生成 1*1px 的图像
![](/assets/364D4AAB3C4557E8BE2152DE8A842832.png)
![](/assets/3A17CFE96EE80FE9E8620C647FB512F9.png)
![](/assets/B4369CB0B82E4DD61EBACD785FD59CBC.png)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3.文件参数检测绕过 -- 添加多个 filename 属性绕过扩展名拦截










