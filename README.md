py-multiprogress-sqlite
===
  该项目已弃用,请参考[py-http-sqlite][0]以获得更优的解决方案  
  python下的多进程(分布式进程)同时读写sqlite的demo  
  
原理简介
----
  混合使用了Queue和Pipe的通讯方式来满足,client to server, server reply client的应用场景  
  1.client使用mp的BaseManager连接server的指定端口,获得请求队列  
  2.client使用uuid生成一个transaction_id,并向server请求一个pipe用于接收server的返回结果,server生成一个pipe并使用transaction_id将pipe缓存起来  
  3.client将需要执行的语句封装在task对象中并附带transaction_id,随后等待pipe返回执行结果  
  4.server不断的从任务队列中取出任务信息,执行sql,并使用transaction_id对应的pipe返回执行结果  
  5.client接收到结果后调用代理方法关闭pipe  
  
特点
---
  1.多进程访问sqlite  
  2.多个语句可以在一次事务中执行  
  
环境需求
---
  Python2.6+(Python3需要自行改造)  
  
如何运行
---
  1.下载项目源码  
  2.进入项目源码文件夹  
  3.执行 python sqlite_manager_server.py  
  3.执行 python client-demo.py  
  
License
---
  MIT license.

[0]: https://github.com/xm0625/py-http-sqlite
