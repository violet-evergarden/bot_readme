# 服务器 ubuntu 20+版本

# 这里介绍两种方法部署

## 1:本地部署 运行脚本:python3.10+

```commandline
pip install tronpy
```
```commandline
pip install pymysql
```
```commandline
pip install python-telegram-bot==20.0a4
```
```commandline
pip install APScheduler
```
```commandline
pip install APScheduler
```

### 数据库:mysql5.7+
### 详细配置bot_config.py 注释有


## 2:docker 部署 安装
### 以上dock儿命令请注意-v的路径对应自己项目的路径 
### jaxchen/bot:v2 已经打包好在dockerhub上
```commandline
sudo docker network create --subnet=172.20.0.0/16 --opt "com.docker.network.bridge.name"="docker1" mynetwork
```

```commandline

sudo docker run --name mysql8 \
--restart=always \
--network mynetwork \
--ip 172.20.0.2 \
-p 3306:3306 \
-e MYSQL_ROOT_PASSWORD=bot_2500_passwd \
-e MYSQL_ROOT_HOST='%' \
-e MYSQL_MAX_CONNECTIONS=1000 \
-e TZ=Asia/Shanghai \
-d mysql
```

```commandline

sudo docker run \
--name bot \
--restart=always \
--network mynetwork \
--ip 172.20.0.4 \
-v /www/wwwroot/xfn666bot.cc/bot:/app -w  /app \
-d jaxchen/bot:v2 python -u bot.py
```


```commandline

sudo docker run \
--name check \
--restart=always \
--network mynetwork \
--ip 172.20.0.3 \
-v /www/wwwroot/xfn666bot.cc/bot:/app -w  /app \
-d jaxchen/bot:v2 python -u check.py
```
