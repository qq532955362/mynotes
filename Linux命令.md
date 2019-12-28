# Linux命令

## 1.服务相关

### 1.1 查看所有服务

```shell
#第一种
service --status-all
#详细
service --status-all|more
#简略
service --status-all|less
```

> #第一种
>
> ![image-20191223190421436](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191223190421436.png)
>
> #详细
>
> ![image-20191223190548527](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191223190548527.png)
>
> #简略
>
> ![image-20191223190640003](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191223190640003.png)

### 1.2 查看某个服务的状态

```shell
service --status-all|grep MySQL
#运用管道命令 过滤 mysql   注意服务名一定要写对 **大小写要区分**
#也可以这样：
service 服务名 status
```

> ![image-20191223191503962](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191223191503962.png)

### 1.3 查看正在运行的服务

```shell
service --status-all|grep running
```

> ![image-20191223191617748](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191223191617748.png)

### 1.4 检查各种服务状态(系统启动时)

```shell
chkconfig --list
```

> ![image-20191223190800343](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191223190800343.png)

## 2.文件操作

### 2.1 创建文件

```shell
#创建文件a 后缀为txt 的文件
touch a.txt
```



### 2.2 浏览文件

```shell
#
cat /文件所在路径/文件名
#
```

### 2.3 编辑文件

```shell
#
vi /文件目录/文件名 
#按 i 进入编辑状态 按ESC进入查看状态
#在查看状态下（ESC）
:wq		#保存并退出 或者（SHIFT+Z+Z）
:q!		#不保存退出
yy		#复制光标所在的行
3yy		#复制光标以下三行（包括）
p		#粘贴复制内容
dd		#删除光标所在行
3dd		#删除光标以下三行（包括）
:w		#保存
:q		#退出
#在查看模式下  gg  定位到文件的第一行   G 定位到最后一行
```

### 2.4 查找文件

```shell
find 目录 -name '文件名.后缀'
#例如
find /usr/local -name 'a.txt'
#查找以txt结尾的文件
find /usr/local -name *.txt
```

### 2.5 复制文件

```shell
#将a.txt文件复制到 b.txt （也就是说将a复制一份 副本 命名为 b）
cp a.txt  b.txt 
#复制指定目录的文件到指定目录下(文件名不改动)
cp /usr/local/a.txt  /usr/soft/
#复制指定目录的文件到指定目录下(文件名改动)
cp /usr/local/a.txt  /usr/soft/b.txt 
#递归复制（连同文件所在的文件夹一起复制）
cp -r /usr/local/a.txt  /usr/soft/test	
```

### 2.6 文件的解压

```shell
#将制定压缩文件解压到制定目录
tar zxf 压缩文件 -C 目录
#例如

```



## 3.目录操作

### 3.1 创建目录

```shell
#创建一个目录 目录名为test
mkdir test
#创建多级目录 目录结构为test/a/b/c
mkdir -p test/a/b/c
```

### 3.2 目录的进入与退出

```shell
#进入某个目录
cd /usr/local
#上一级
cd ..
#进入根目录
cd /
#当前目录下
./
#列出当前目录下所有文件或文件夹的名字
ls
# 列出当前目录下所有文件或文件夹的名字及其详细信息
ll
#使用 ls -a可以查看当前目录下的所有文件及目录 （包含隐藏文件、目录）
ls -a
#使用 ls-l 可以查看当前目录下的文件及子目录的详细信息
ls -l
```

### 3.3 查看当前目录的完整路径

```shell
pwd
```



## 4.文件与目录的删除

```shell
rm -rf 文件名(或者压缩包名 目录名)		//
#参数解释
-f 不用提示 
-r 强制删除 不仅删除文件还删除目录也可以删除其他文件或压缩包,无论删除任何目录或文件，都直接使用 rm-rf 目录/文件/压缩包
```

