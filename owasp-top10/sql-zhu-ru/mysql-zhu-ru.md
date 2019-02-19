# MySQL注入
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x01 环境需求
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MySQL数据库(version>=5.04)
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x02 注入函数
![](/assets/49A439B31D3656FE1266C2809C616748.png)
![](/assets/E33220D060B048EAA19A59928F1FFA64.png)
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x03 样例代码
![](/assets/83A2168FAA2CDFB87AF8716FC9F92A3B.png)
###&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0x03 注入流程
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
                
```
####&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.注入点识别:





