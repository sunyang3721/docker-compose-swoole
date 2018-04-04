# docker-compose-swoole
利用docker快速搭建高性能web服务器


创建 docker-compose.yml 文件
```
version: '3.4'
services:
  swoole:
    image: "549658/docker-compose-swoole:swoole"
    ports:
      - "9501:9501"
    volumes:
      - ./app/www:/var/www/html:rw
    restart: always
    depends_on:
      - mysql
      - redis
    command: php -v

  mysql:
    image: "549658/docker-compose-swoole:mysql_latest"
    ports:
      - "3306:3306"
    volumes:
      - ./data/mysql/data:/var/lib/mysql:rw
      - ./data/mysql/sock:/var/run/mysqld:rw # remove when windows.
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: 549658
      MYSQL_DATABASE: swoft
      MYSQL_USER: swoft
      MYSQL_PASSWORD: 123456

  redis:
    image: "549658/docker-compose-swoole:redis_latest"
    ports:
      - "6379:6379"
    volumes:
      - ./data/redis/data:/var/lib/redis:rw
    sysctls:
        net.core.somaxconn: 65535
    restart: always
```

#docker 使用方法
```
docker-compose up -d
```

# swoft框架 快速搭建
先git clone 再修改docker-compose.yml
```
version: '2'
services:
  swoole:
    container_name: swoft
    image: "549658/swoft:latest"
    ports:
      - "80:80"
    volumes:
      - ./:/var/www/swoft:rw
    stdin_open: true
    tty: true
    restart: always
    depends_on:
      - mysql
      - redis
    command: php /var/www/swoft/bin/swoft start

  mysql:
    container_name: mysql
    image: mysql:latest
    ports:
      - "3306:3306"
    volumes:
      - ./data/mysql/data:/var/lib/mysql:rw
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: 123456

  redis:
    container_name: redis
    image: redis:latest
    ports:
      - "6379:6379"
    volumes:
      - ./data/redis/data:/var/lib/redis:rw
    restart: always

  phpmyadmin:
    container_name: phpmyadmin
    image: phpmyadmin/phpmyadmin:latest
    ports:
        - "8080:80"
    environment:
        - PMA_ARBITRARY=1
    depends_on:
        - mysql
    volumes:
        - ./data/phpmyadmin:/sessions

```

# 最后 composer update
```
docker run --rm --interactive --tty \
    --volume ./swoft:/app \
    composer update
```