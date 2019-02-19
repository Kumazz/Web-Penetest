# 写在最前
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x01 环境需求
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[SQLi在线靶场](https://sqli-labs.htctf.com/)、[SQLi Github](https://github.com/Audi-1/sqli-labs)、Docker(镜像)、SQL语言、Hackbar插件
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;docker run -dt --name sqli -p 80:80 --rm acgpiano/sqli-labs
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;run 运行 -dt 守护进程 --name 别名 --rm 停止运行删除进程
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x02 关于SQLi
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**原因:** 开发人员对从web表单、cookie、输入参数等收到的值传递给SQL查询之前进行过滤控制
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**原理:** SQL代码插入或添加到应用(用户)的输入参数中，并且参数在后台SQL服务器中解析和执行


