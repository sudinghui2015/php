本文地址：http://www.laruence.com/2009/11/13/1138.html

## 概念
```txt
PATH_INFO是一个CGI1.1的标准，经常用来做为传参载体
```
## 作用
```txt
* 代替rewrite来实现伪静态页面
* 不少PHP框架也使用PATH_INFO来作为路由载体
```
## nginx与apache之间区别
```txt
* 在apache中，当不加配置的时候，对于PHP脚本，AcceptPathInfo来默认接受，也就是说，
如果在服务器存在一个/laruence/index.php,
那么，对于如下请求：
/laruence/index.php/dumny
/laruence/dunmy
apache都接受，都会被认为是对index.php的访问
并会设置PATH_INFO为dumny
* nginx下不支持PATH_INFO，原因在于默认的配置文件对PHP只是很基础的，对于默认设置来说访问上面的请求也会出现404，简直是致命的。
```

## 解决方法
```txt
* 使用rewrite，但是缺点也很明显，需要把PATH_INFO转化为Query String
* 模拟PATH_INFO：
  1）
```
