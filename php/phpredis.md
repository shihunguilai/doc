# redis-server
## 1. 源码安装redis
- 下载地址：[http://redis.io/download](http://redis.io/download)下载最新版

```shell
1. wget http://124.202.164.12/files/1224000008C76212/download.redis.io/releases/redis-3.2.3.tar.gz
2. tar zxvf redis-3.2.3.tar.gz
3. cd redis-3.2.3/
4. make
5. make test
```

- 启动redis-server
```shell
cd src
./redis-server  //默认配置启动
./reids-server redis.conf //redis.conf是一个默认的配置文件。我们可以根据需要使用自己的配置文件。
```

- 用客户端和redis服务交互
```shell
cd src
./redis-cli
redis> set foo bar
OK
redis> get foo
"bar"
```


## 2. apt-get 安装
- 安装
```shell
sudo apt-get update
sudo apt-get install redis-server
```

- 启动redis服务器
```shell
redis-server
```
- reids 客户端连接
```shell
redis-cli
```


---

# phpredis 扩展
- 安装
```
wget https://codeload.github.com/phpredis/phpredis/zip/php7
unzip php7
cd mulu
./configure
sudo make && sudo make install && sudo make test
```
