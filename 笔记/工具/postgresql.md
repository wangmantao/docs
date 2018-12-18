# Postgresql 学习笔记

## 灵感


## 知识点点滴
8. max min的认识
  以前以为max/min只能用在number里
　其实可以用在其它类型列

7. partition 数据分组 
 function name over (partition by column)   这里的partition by 子句用于对行进行分组的。

6. 窗口函数语法
windFn() over() from 集合
求单值，却返回与集合一样多的rows
	
5. 窗口函数
“ The whole idea behind window functions is :
to allow you to process several values of the result set at a time:
(充许你处理返回集合中的值)
 you see through the window some peer rows and are able to compute a single output value from them, 
通过匹配的行，并且可以计算它们的单个值输出,
much like when using an aggregate function. ”
类似聚合（合计）函数．

4. jdbc 查询
	(jdbc/query 连接名 ["select查义字串"]) ;; 连接名是map变量
1. pgsql 连接远程服务器
　　psql -h IP地址 -p 端口  -U 
[pali dbName](~/bin/pali 快捷命令)

2. 查看数据库/改变目标数据库
	\l 查看有哪些数据库
	\d 查看有哪些表
	\d 表名　查看表结构(字段)
3. 建个视图/并查询它

## 灵感 (备份)
1. 全部终端操作，不和GUI 
	容易掉线，sali远程操作吧

