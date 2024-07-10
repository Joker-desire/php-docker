# php-docker

## 镜像

```bash
docker pull tning6666/php83-xdebug:latest

docker pull tning6666/php83-swoole51x-openssl:latest

docker pull tning6666/php83-swoole:latest

docker pull tning6666/php83-swoole-xdebug:latest

docker pull tning6666/php83-swoole51x-openssl-xdebug:latest
```

## 将进入docker容器转成快捷命令进入（Mac版）

### 查看当前docker容器

```bash
docker container ls -a
```

获取到`NAMES`值（NAMES值如果不手动改将不会变动，CONTAINER ID 如果删除容器，重新启动则会变更）

### 编写shell脚本

文件存放示例目录`/Users/xxx/php-docker/bin`

`docker-php` 为容器名，根据实际情况进行更改

```shell
#! /bin/bash
docker exec -it docker-php /bin/bash
```

### 给shell脚本添加权限

```bash
cd bin
sudo chmod 755 docker-php
```

### 将shell脚本添加到环境变量中

进入`~/.zshrc` 增加以下内容

```bash
export DOCKER_PHP="/Users/xxx/php-docker"
export PATH=$PATH:$DOCKER_PHP/bin
```

执行命令，使其生效

```bash
source ~/.zshrc
```

### 快捷命令启动容器

```bash
docker-php
```
