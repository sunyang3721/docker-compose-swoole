# Tengine 介绍
Tengine是由淘宝网发起的Web服务器项目。它在Nginx的基础上，针对大访问量网站的需求，添加了很多高级功能和特性。Tengine的性能和稳定性已经在大型的网站如淘宝网，天猫商城等得到了很好的检验。它的最终目标是打造一个高效、稳定、安全、易用的Web平台。
已在docker生成，系统为apline3.7.
# docker 使用方法
```
 docker run -it  --name tengine  -p 80:80  -p 443:443 -v $pwd:/usr/share/nginx/html:rw -v $pwd:/etc/nginx/conf.d:rw -v $pwd:/var/log/nginx:rw -d 549658/docker-compose-swoole:tengine.2.2.2
```

### 本人测试如下
```
docker run -it  --name tengine  -p 8085:80  -v ./tengine/html:/usr/share/nginx/html:rw -v ./tengine/conf:/etc/nginx/conf.d:rw -v ./tengine/log:/var/log/nginx:rw -d 549658/docker-compose-swoole:tengine.2.2.2
```
### 挂载目录介绍
```
./tengine/html  这是html根目录
./tengine/conf  这是conf配置文件
./tengine/log   这是日志
```
### 创建conf配置文件复制下面并保存,把test.conf 放入 ./tengine/conf 目录内
```
# load modules compiled as Dynamic Shared Object (DSO)

#dso {
#    load ngx_http_fastcgi_module.so;
#    load ngx_http_rewrite_module.so;
#}

server {
    listen       80;
   #listen       somename:80;
    server_name  somename  alias  another.alias;

    location / {
       root   /usr/share/nginx/html;
       index  index.html index.htm;
    }
}
```
### 配置文件之后 输入下面命令 热加载即可
```
// 如果没有报错 说明载入成功  就可以访问了
 docker exec -it tengine  nginx -s reload
```
# 443端口访问