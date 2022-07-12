---
title: "Docker环境下 MySQL快速配置"
date: 2021-12-19
tags: [Docker, 配置]
---
1.拉取Mysql镜像
```bash
docker pull mysql
```
2.启动并创建带超管用户的Mysql容器
```
docker run -itd --name 容器名 -p 主机端口:3306 -e MYSQL_ROOT_PASSWORD=密码 mysql
```
```
例子：
docker run -itd --name mysql-test -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql
监听容器内部3306端口并映射到宿主机3306端口，超管密码为123456
容器名字为mysql-test
```
3.进入容器
```
#列出容器
docker container ls 
#选择进入Mysql容器
docker exec -it 容器名或者ID bash
```
4.创建普通用户并授权
```
CREATE USER 'username'@'%' IDENTIFIED BY 'password';
GRANT ALL ON *.* TO 'username'@'%';
FLUSH PRIVILEGES;
```
5.enjoy it!