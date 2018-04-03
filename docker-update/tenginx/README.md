# Tengine 介绍
Tengine是由淘宝网发起的Web服务器项目。它在Nginx的基础上，针对大访问量网站的需求，添加了很多高级功能和特性。Tengine的性能和稳定性已经在大型的网站如淘宝网，天猫商城等得到了很好的检验。它的最终目标是打造一个高效、稳定、安全、易用的Web平台。
已在docker生成，系统为apline3.7.
# docker 使用方法
```
 docker run -it  --name tengine  -p 80:80  -p 443:443 -v $pwd:/usr/share/nginx/html:rw -v $pwd:/etc/nginx/conf.d:rw -v $pwd:/var/log/nginx:rw -d 549658/docker-compose-swoole:tengine_2.2.2 
```

## 公告
Dockerfile_ubuntu-14.04、Dockerfile_2.1.0 这两个文件是旧版本 不再更新