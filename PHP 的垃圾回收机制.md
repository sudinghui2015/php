## 文件来源：
http://blog.jobbole.com/110456/?utm_source=blog.jobbole.com&utm_medium=relatedPosts
## GC概念
```txt
PHP语言同其他语言一样，具有垃圾回收机制。那么今天我们要为大家讲解的内容就是
关于PHP垃圾回收机制的相关问题。希望对大家有所帮助。
PHP strtotime应用经验之谈PHP memory_get_usage()管理内存PHP unset全局
变量运用问题详解PHP unset()函数销毁变量教你快速实现PHP全站权限验证
    一、PHP 垃圾回收机制(Garbage Collector 简称GC) 
在PHP中，没有任何变量指向这个对象时，这个对象就成为垃圾。PHP会将其在内存中销毁；这是PHP的GC垃圾处理机制，防止内存溢出。
当一个PHP线程结束时，当前占用的所有内存空间都会被销毁，当前程序中所有对象同时被销毁。
GC进程一般都跟着每起一个SESSION而开始运行的.gc目的是为了在session文件过期以后自动销毁删除这些文件.
    二、__destruct /unset __destruct() 析构函数，是在垃圾对象被回收时执行。
unset 销毁的是指向对象的变量，而不是这个对象。
    三、 Session 与PHP垃圾回收机制由于PHP的工作机制，
它并没有一个daemon线程来定期的扫描Session信息并判断其是否失效，
当一个有效的请求发生时，PHP 会根据全局变量 session.gc_probability和session.gc_divisor的值，
来决定是否启用一个GC。 在默认情况下，session.gc_probability=1, session.gc_divisor =100也就是说有1%的可能性启动GC
(也就是说100个请求中只有一个gc会伴随100个中的某个请求而启动).
PHP垃圾回收机制的工作就是扫描所有的Session信息，用当前时间减去session最后修改的时间，
同session.gc_maxlifetime参数进行比较，如果生存时间超过gc_maxlifetime(默认24分钟),就将该session删除。
但是，如果你Web服务器有多个站点，多个站点时,GC处理session可能会出现意想不到的结果，原因就是：GC在工作时，并不会区分不同站点的session.
那么这个时候怎么解决呢？
修改session.save_path,或使用session_save_path()让每个站点的session保存到一个专用目录，
提供GC的启动率，自然，PHP垃圾回收机制的启动率提高，系统的性能也会相应减低，不推荐。
在代码中判断当前session的生存时间，利用session_destroy()删除。
```
