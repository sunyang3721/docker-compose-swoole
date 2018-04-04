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
        server_name  somename  alias  another.alias;

        root   /usr/share/nginx/html;
        index  index.html index.htm;
        location / {
	        proxy_http_version 1.1;
	        proxy_set_header Connection "keep-alive";
	        proxy_set_header Host $http_host;
	        proxy_set_header X-Real-IP $remote_addr;
	        if (!-e $request_filename) {
	        	# 注意 由本机IP地址显示为主 
	             proxy_pass http://10.68.80.155:8084;
	        }
	    }
    }

    # HTTPS server
    #
    #server {
    #    listen       443 ssl http2;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}

```
### 配置文件之后 输入下面命令 热加载即可
```
// 如果没有报错 说明载入成功  就可以访问了
 docker exec -it tengine  nginx -s reload
```
# 更新历史
2018-04-04  升级至 alpine:3.7   tengine升级至最新为 tengine_2.2.2

# 443端口访问  强制跳转HTTPS访问  未完成待续......
```
//百度采用这种方式
<meta http-equiv="refresh" content="0;url=https://www.xxx.com/">
```

