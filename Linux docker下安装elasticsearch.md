# Linux docker下安装elasticsearch

## 1.搜索可用镜像

```shell
docker search 镜像名称
```

## 2.拉取镜像

```shell
docker pull 镜像名称：版本号   
#或者
docker pull 镜像id
```

### 3.创建并后台运行容器

```
docker run -id --name=es -p 9200:9200 -p 9300:9300 镜像id
#或者
docker run -id --name=es -p 9200:9200 -p 9300:9300 镜像名:版本
```

> 参数解释：-i 表示创建  -d 表示守护线程（后台运行） -p表示指定宿主机映射到容器端口

## 4.`查看日志（很重要可以查看异常）`

```shell
docker logs -f 容器名称（或者id）      #可以查看日志一遍寻找容器跑不起来的原因
```

