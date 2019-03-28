# 解析上传

### 0x01 解析

####             查看服务器类别:  F12审查元素-Network-Headers-Response Headers-Server

### 0x02 上传

####             1.文件上传流程

![](/assets/1.png)

####             2.文件上传漏洞

![](/assets/10657CE2A431C6874A8C243786ACDDDA.png)

####             3.文件检测流程

![](/assets/5CF6B9DB4278738F18B4E81FA6088146.png)  
               **PS:**1.存在上传点  
                     2.可以上传动态文件  
                     3.上传目录具有执行权限，并且上传的文件可执行  
                     4.可访问到上传的动态文件

