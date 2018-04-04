# swoole 介绍
是一个高性能的异步并发 TCP、UDP、Unix Socket、HTTP，WebSocket 服务。Swoole 可以广泛应用于互联网、移动通信、企业软件、云计算、网络游戏、物联网（IOT）、车联网、智能家居等领域。
官网 https://www.swoole.com/

# 安装版本
- php和swoole都是最新稳定版本
- 使用swoole2.x最新版本构建，协程功能上线
- 已安装 ["GD", "iconv", "pdo_mysql", "dom", "xml", "curl", "swoole"]等PHP扩展
- 已开启["coroutine", "openssl", "http2", "async-redis", "mysqlnd","opcache"]扩展
- 清理安装包以及临时文件，节省空间
- 干净环境，无其他多余的安装
- 全部设置为默认为中国上海时区

# docker 使用方法
```
 docker run -it  --name swoole  -p 9501:9501  -v $pwd:/var/www/html:rw  -d  549658/docker-compose-swoole:swoole_latest
```

### 本人测试方法如下
```
docker run -it --name swoole -p 9501:9501 -v /docker-www/swoole:/var/www/html:rw -d 549658/docker-compose-swoole:php_swoole
```
