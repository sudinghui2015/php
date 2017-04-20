## 下载Redis

[http://download.redis.io/releases/](redis官方下载)

## 安装&配置

```txt
~Downloads sudinghui$ cd redis-3.2.8
~make
~make test
~sudo make install
```

## 启动redis
```txt
cd 到redis解压目录下，执行src/redis-server
```

## 测试连通
```txt
~ cd /usr/local/bin
~ ./redis-cli
127.0.0.1:6379> set jackiehff hi
OK
127.0.0.1:6379> get jackiehff
"hi"
```
