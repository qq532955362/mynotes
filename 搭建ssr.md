> 购买阿里云服务器 
>
> 1. www.aliyun.com  搜索轻量级应用服务器  购买香港的最便宜的那个
> 2. 购买完成设置预装额系统  centos7 
> 3. 然后开始搭建ssr

> 搭建ssr
>
> ```shell
> #第一条命令 下载ssr客户端
> wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
> 
> #第二条命令 给权限
> chmod +x shadowsocks-all.sh
> 
> #第三条命令 安装ssr server端
> ./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
> 
> ```
>
> 之后会让你填 端口 密码 加密方式等 
>
> ![image-20191220120326236](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191220120326236.png)
>
> `出现上面这个界面说明安装成功` `这里的注意截个图后面连接要用`

> 删除阿里云的ip屏蔽
>
> `方法一`：
>
> ```shell
> #卸载阿里云盾监控
> wget http://update.aegis.aliyun.com/download/uninstall.shsh uninstall.sh
> 
> wget http://update.aegis.aliyun.com/download/quartz_uninstall.shsh quartz_uninstall.sh
> 
> #删除残留
> pkill aliyun-service       //杀进程
> rm -fr /etc/init.d/agentwatch /usr/sbin/aliyun-service  //删除服务文件
> rm -rf /usr/local/aegis*			//删除文件
> ```
>
> `方法二`:
>
> ```shell
> #查看配置列表
> chkconfig --list
> ```
>
> ![image-20191220120834283](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191220120834283.png)
>
> ```sh
> #停止服务
> service aegis stop
> ```
>
> ![image-20191220120959717](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191220120959717.png)
>
> 

> 在windows中设置客户端：
>
> 解压：![image-20191220123155851](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191220123155851.png)
>
> 运行客户端：
>
> ![image-20191220123235139](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191220123235139.png)
>
> 配置好之后：![image-20191220143333417](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191220143333417.png)

