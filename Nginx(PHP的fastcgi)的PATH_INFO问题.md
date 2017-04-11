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
* 在apache中，当不加配置的时候，对于PHP脚本，
AcceptPathInfo来默认接受，也就是说，
如果在服务器存在一个/laruence/index.php,
那么，对于如下请求：
/laruence/index.php/dumny
/laruence/dunmy
apache都接受，都会被认为是对index.php的访问
并会设置PATH_INFO为dumny
* nginx下不支持PATH_INFO，原因在于默认的配置
文件对PHP只是很基础的，对于默认设置来说访问上面的请求也会出现404，
简直是致命的。
```

## 解决方法
```txt
* 使用rewrite，但是缺点也很明显，需要把PATH_INFO转化为Query String
* 模拟PATH_INFO：
  1）在Nginx中，通过对文件名的扩展名匹配，来决定是否要交给php cgi服务器
  去解释，在nginx.conf中一般默认配置项：
  location ~.php$ {
    fastcgi_index index.php;
    fastcgi_pass  127.0.0.1:9000;
    include       fastcgi_params;
  }
  所以，对于类似/laruence/info.php/pathinfo这样的文件路径，
  Nginx是不会正确的交给php cgi服务器的，需要改写这段配置：
  location ~.php {
    fastcgi_index   index.php;
    fastcgi_pass    127.0.0.1:9000;
    include         fastcgi_params;
  }
  现在，脚本路径已经交由PHP自己处理了。
```

## 怎么增加PATH_INFO
```txt
* 打开PHP中cgi.fix_pathinfo配置项，打开这个配置项以后，
PHP会根据CGI规范来检查SCRIPT_FILENAME中那部分是访问脚本
和PATH_INFO（ini配置解释:http://cn.php.net/manual/en/ini.core.php），并根据SCRIPT_NAME来修改PATH_INFO
location ~.php {
  fastcgi_index   index.php
  fastcgi_pass    127.0.0.1:9000;
  include         fastcgi_params;
  fastcgi_param   PATH_INFO $fastcgi_script_name;
}
```
