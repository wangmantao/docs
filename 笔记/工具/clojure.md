# clojure 用法study 
[w3c](https://www.w3cschool.cn/clojure/)
[timer](https://bjeanes.com/2012/09/call-clojure-function-on-a-timer)

## 学习灵感 (完成后备份到分割线以下)
8. lein run 可以；uberjar 后却不能运行
	uberjar时的警告：
	arning: specified :main without including it in :aot.  
	Implicit AOT of :main will be removed in Leiningen 3.0.0.           
	If you only need AOT for your uberjar, consider adding :aot :all into your                                      
	:uberjar profile instead.   
	Compiling io.ryos.tars.mycmds  
	----> 用了:aot :all 后，找不到io/moo/tars/dsl.clj classpath

7. Daemon移植到其它电脑
	要重新从官网下载jre环境（rpm安装）
	不能找到daemon loader org/apache/commons/daemon/support/DaemonLoader
	--> 对策方法：
		run.sh (jsvc启动脚本)	
		1. 加上参数 -cwd /当前/工作/目录
		2. -cp commons.daemon.1.x.x.jar:./daemon_api.jar
6. 籽了把clj-serial 也做成公用库
	upLocalRepo.sh 
	.产生的JAR名字，有project.clj定义的(所以项目目录名和项目名并不一直)
5. lein-jarbin (为了daemon; 不进行了)
	lien插件，运行包含jar的二进制文件
	用作复杂系统的二进制或者守护程序，没有安装步骤．

4. 把clojure 做成守护进程
	<< Clojure 经典实例 >> 8.4  (P. 321)
	用到Apache Commons Deamon库
	1. 应用必须实现接口：Deamon (org.apache.commons.deamon.Deamon)
	2. 做一个系统应用(unix: jsvc / windows: procrun)

- project.clj 
	:aot :all ---> 什么意思	
	:dependencise [org.apache.commons/commons-deamon "1.0.9"]
	:main　空间.类 (没有引号，没有扩展名)
	
- ns申明时:
	1. :import
	2. :gen-class ->实现基于 :implements

- 定义变量时：
	1. state atom()类型 

- 定义函数时：
	1. init [args] / start [] / stop []
	2. deamon的实现
	   -init[this ^DeamonContext context] -> 应用初始化
	   -start[this] ->　开启新线程执行工作　-> jsvc接手．
	   -stop[this]  -> 要停上start 启动的线程
	   -destroy[this] -> 可以写一具空函数给jsvc看
	3. 命令行调用 -main [& args]  (做冒烟测试，接口不要动)

- 用jscv 执行
	java_home ..................................

3. 把jar制作成守护进程
	
2. 线程交互
	利用了watch功能．当引用类型变量（atom)值改为时，atom的监视函数会被调用．　参考：　add-watch

	
## 知识点滴 (倒序)
24. jsvc 调用class类库（aot所编译）,
	入口函数在-start上，内用future其它线程调用

23. java_home 问题
	which java -> /usr/bin/java -> /etc/alternatives/java ->  /usr/java/jre1.8.0_151/bin/java

22. jsvc / procrun  (java service / process run)
	JVM 与操作系统的中间层，Ｃ编写;创建一个后台执行java应用

21. :import java类的空间名 类１名　类２名　（import的格式）

20. 实例方法（参数是this)

19. 函数连接号"-main" 告诉clojure编辑器，它是一个JAVA函数

18. cron任务调用
	linux下的定时任务, 由crontab设定

17. filter
	(filter fn map)
	把map的每个元素逐个给fn进行处理辨别，如果为真这个元素被筛选出.
	例：　(filter #(= std_val %) map_array)

16. distinct
	意思：有区别的. 作用：在一组数中只筛选出有区别的数

15. (:key map)
	直接获得map对应key的val

14. clojure.java.shell/sh 
	调用命令行

13. add-watch 
	(add-watch reference key fn)
	fn 必须有四个参数(keyId ref oldVal newVal)

12. assoc 
	(assoc map key val)(assoc map key val & kvs)	
	往已经map中添加指定的:key val对;如果key已经存在，则更新val;
 	可以写多份:key val :key2 val :key3 val	

11. update-in 
	(update-in m ks f & args)
	详：(update-in map keys fun & args)
	keys是多元素的向量，所以写法是：［:key1]
	f处是函数　(str " somestr") -> 更新为: "原内容　somestr"
	更新嵌套map结构中指定key的内容，用函数改变旧指返回新值.

10. 用swap!改变atom值的方法
	（swap!
	(swap! atom f)(swap! atom f x)(swap! atom f x y)(swap! atom f x y & args)
	f: conj; inc; dec; update-in; identify; assoc	
	x: f的第一个参数　y: f的第二个参数

9. 加载依赖 jdbc
	project.clj :dependencies [[org.coljure/java.jdbc "0.6.1"]
				  [org.postgresql/postgresql "9.4.1211"]]
	类.clj :require [clojure.java.jdbc :as jdbc])

8. java对像/实例的方法调用 (前面加点)
	(.getTime Date类) (.toString javaObject)

7. project.clj :main 的写法
	:main 含有main函数的空间名 (空间名无需引号)
	main函数的定义 (def -main [ & args ])

6. lein-localrepo 本地库用法 (opencv clojure 安装所讲)
[github](https://github.com/kumarshantanu/lein-localrepo)
(在profiles.clj中配置它为全局插件)
__localrepo用法:__
lein localrepo install [-r repo-path] [-p pom-file] <filename> <[groupId/]artifactId> <version>
例：__lein localrepo install__ foo-1.0.6.jar com.example/foo 1.0.6
lein localrepo list [-r repo-path] [-s | -f | -d]
lein localrepo remove <[groupId/]artifactId> [<version>]
例：__lein localrepo remove__ com.example/foo 

5. clojure 项目配置文件 ~/.lein/profiles.clj 

4. sting->number转换 (if number? (read-string "2"))
	read-string 属于 clojure.tools.reader <见github> 

1. *string <=> date*
　　（.parse <=> .format) 
例：
(.format
    (java.text.SimpleDateFormat. "dd.MM.yyyy") ;; 参数１，要字符串化的样子
    (.parse  (java.text.SimpleDateFormat. "ddMMyyyy") "08082013")) ;; 参数２，一个jave.util.Date 类型

(.parse 参数１待指定字符串的格式　参数２符合前面格式的字符串)

2. *getTime ---获得当前时间整形*
java语言 Date类的方法 
(.getTime (java.util.Date.))  ;;Date实例的成员函数，获得当前时间(类型java.lang.Long 整形)

3. *timer制作方法*
- (future  & body): body部分被另一个thread调用; 可以(def f (future ...)) @f--同步(阻塞式)取返回结果
- Thread/sleep int: 定时器延时必有项
- doseq [one somes]: 取序列的每个项并做处理
- repeatedly n fn:  结合一个可有副作用的函数(无参数)，该函数被重复(无限次或n次)调用，每次调用返回结果组成Lazy seq(懒惰序列)．
- apply fn args: 类似reduce + [1 2 3] 第个参数迭加运算；而它是把每个参数依次带到函数fn运行．

```
(defn tick
  "Call f with args every ms. First call will be after ms"
  "每x毫秒调用一次f函数（带参数），首次调用会有x毫秒的延迟"
  [ms f & args]

  (future  ;; 以下body新线程执行
    (doseq [f (repeatedly #(apply f args))]  ;每个seq子项依次执行，
      (Thread/sleep ms)
      (f))))
```
简单的做法：　loop f recur 缺点是无限循环；不可控；无参数

## java.text　空间(包)
[SimpleDateFormat类](https://docs.oracle.com/javase/7/docs/api/java/text/SimpleDateFormat.html) (java.text.SimpleDateFormat.)

## java.util　空间(包)

---------------------------------------------------------------------------------------------
## 学习灵感 (备份)

### 建自已的clojure库
1. coljure 怎么建自己的类库util.clj，每个项目可以自动被加载，类似本地的maven reps.
(当前就为了完成建一个库，内有根据人员调出ＩＤ号的函数, 并把API做的正规/文档化一点)

2.  建立一个项目(cljutil)，定义一个空间ns, 其内定义一个函数（分公用和私用）做一个最简demo
	ns: cljutil.core/foo
	lein uberjar  生产一个jar, 确定它的位置: targetSNAPSHOT-standalone.jar

3. 把jar它做成本地mvn repostory
	> lein localrepo install /home/wmt/temp/test/cljutil/target/cljutil-0.1.0-SNAPSHOT.jar cc.taily/cljutil 0.1.0
	> lein localrepo list -f |grep cljutil
	[cc.taily/cljutil "0.1.0"]     cljutil-0.1.0.jar                   7250 2018-11-13 23:24:20

4. 新建另一个项目utiltest，让它调用以上　jar 工作包 -> 查看调用运行结果
	(project.clj 中: 	:dependencies: [[其它][groupId/artifactId "version"]] (需求库)
	(在使用的源文件中：　	:require [cljutil.core] as xx)
	(cljutil库函数应用方法为：　（cljutil.core/foo "wmt")    )

5. 变更cljutil函数内容，再次lein uberjar, 再次MVN local reporstory
	(重复执行以下内容－－－将来可用脚本执行, 或lein uberjar 后就直接自动执行脚本)
	lein uberjar
	lein localrepo install /home/wmt/temp/test/cljutil/target/cljutil-0.1.0-SNAPSHOT.jar cc.taily/cljutil 0.1.0

6. 查看utiltest运行结果是否有变.
	(变更成功)

7. 确定cc.taily.util这个项目源码建在哪里，本地化的脚本写在哪里，怎么运行，有哪些功能函数．


