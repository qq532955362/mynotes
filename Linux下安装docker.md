

# docker 安装

> 1. Docker要求CentOS系统的内核版本高于 3.10 ，通过 **uname -r** 命令查看你当前的内核版本是否支持安账docker
>
>    ```shell
>    uname -r
>    ```
>
> 2. 更新yum包：sudo yum update
>
>    ```shell
>    sudo yum update
>    ```
>
> 3. 安装需要的软件包，yum-util 提供yum-config-manager功能，另外两个是devicemapper驱动依赖的
>
>    ```shell
>    sudo yum install -y yum-utils device-mapper-persistent-data lvm2
>    ```
>
> 4. 设置yum源
>
>    ```shell
>    sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
>    ```
>
> 5. 可以查看所有仓库中所有docker版本，并选择特定版本安装
>
>    ```shell
>    yum list docker-ce --showduplicates | sort -r
>    ```
>
>    ![image-20191225000938605](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191225000938605.png)
>
> 6. 安装docker  这里选择的是下面的版本
>
>    ```shell
>    sudo yum install docker-ce-17.12.0.ce
>    ```
>
> 7. 启动安装号的docker服务并设置开机启动
>
>    ```shell
>    #启动docker
>    sudo systemctl start docker
>    #设置开机启动
>    sudo systemctl enable docker
>    ```
>
> 8. 验证安装是否成功(`有client和service两部分表示docker安装启动都成功了`)
>
>    ![image-20191225001258144](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191225001258144.png)
>
> 9. 查看docker的启动状态，如果有下图则说明启动成功
>
>    ```shell
>    systemctl status docker
>    ```
>
>    ![image-20191225001425994](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191225001425994.png)

# docker卸载

> 1. 查询docker安装过的包：
>
>    ```shell
>    yum list installed |grep docker
>    ```
>
>    ![image-20191225001728941](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191225001728941.png)
>
> 2. 删除安装包
>
>    ```shell
>    yum remove docker-ce.x86_64 ddocker-ce-cli.x86_64 -y
>    ```
>
> 3. 删除docker管理过的容器、镜像等
>
>    ```shell
>    rm -rf /var/lib/docker
>    ```
>
>    all ok！