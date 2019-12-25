# Docker命令

## centOS7 操作docker

```sh
systemctl restart docker			//重启docker
systemctl start docker				//启动docker
systemctl stop docker 				//停用docker
systemctl enable docker 			//检查docker是否可用
```

## Docker镜像命令

```sh
docker images								//查看所有镜像
docker rmi 镜像名：版本号（或者镜像的id）			//删除指定的镜像
docker rmi `docker images -q`				  //删除所有的镜像
```

## Docker容器操作

```sh
docker run -it --name=容器名称  镜像id（或者 镜像名：版本号） /bin/bash 		//创建容器在后台运行 （exited状态）

docker run -id --name=容器名称  镜像id（或者 镜像名：版本号） /bin/bash		//创建容器在前台运行（开启状态）

docker start 容器id												//开启容器

docker stop  容器id												//停止容器

docker ps -a 													 //查看各种状态的容器

docker ps 														//只查看处于激活状态的容器

docker inspect 容器名称											//查看容器的ip地址

docker rm 容器id（或者容器的名称）									//删除指定容器

docker rm `docker pa -a`										//删除所有的容器
```

