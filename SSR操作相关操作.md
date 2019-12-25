> 查看ssr服务端密码：
>
> ```shell
> cat /etc/shadowsocks.json
> ```
>
> 修改ssr服务端的配置文件（密码、端口等）
>
> ```shell
> vi /etc/shadowsocks.json
> ```
>
> ![image-20191223174931449](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191223174931449.png)
>
> **`修改完一定要重启shadowsocks的服务`**
>
> ```shell
> service shadowsocks restart
> ```
>
> 顺便附上服务的集中操作方法：
>
> ```shell
> service shadowsocks start		//启动服务
> service shadowsocks stop		//停止服务
> service shadowsocks restart		//重启服务
> service shadowsocks status		//查看服务的状态
> ```
>
> 