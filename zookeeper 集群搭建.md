# 1.zookeeper 集群搭建

- 将zookeeper的tar包上传到linux 的soft下

![image-20191210113716829](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210113716829.png)

- 解压zookeeper-3.4.6.tar.gz到 /usr/local

![image-20191210113650177](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210113650177.png)

- 进入解压后的zookeeper目录

  ![image-20191210113901664](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210113901664.png)

- 创建data目录（在zookeeper目录下）

![image-20191210114013895](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210114013895.png)

- 在zookeeper目录下进入`conf目录`将`zoo_sample.cfg `文件改名为 `zoo.cfg`

  ![image-20191210114546372](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210114546372.png)

- 在/usr/lcoal/ 目录下建立文件夹 zookeeper-cluster

  ![image-20191210114656237](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210114656237.png)

- 将解压后的zookeeper复制到建立的zookeeper-cluster中并命名zookeeper-01 以此类推02 03

  ![image-20191210115208763](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210115208763.png)

- 配置每一个zookeeper的dataDir  在每个zookeeper中的zoo.cfg中 并修改端口 分别为2181 2182 2183

![image-20191210120355608](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210120355608.png)

- 用editPlus连接192.168.25.128 具体过程如下

  ![image-20191210120603843](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210120603843.png)

`打开之后`

![image-20191210120734128](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210120734128.png)

`按顺序填写完成之后`

![image-20191210120805118](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210120805118.png)

`点击Advanced Options`

![image-20191210120917318](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210120917318.png)

完成后点击ok 

![image-20191210121005377](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210121005377.png)

`确定就行了`

这样就可以在windows里面改linux的文件了

- 完成后配置集群

  1. 在每个zookeeper的data目录下创建一个myid文件 文件的内容分别是1 2 3 这个文件的目的就是记录每个服务器的id

     ![image-20191210122606394](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210122606394.png)

     `vi 命令` 表示`该文件存在就编辑 如果该文件不存在就创建并编辑`

  2. 在每个zookeeper的zoo.cfg配置客户端访问端口（clientPort）和集群服务器IP列表如下

     ```
     server.1=192.168.25.128:2881:3881
     server.2=192.168.25.128:2882:3882
     server.3=192.168.25.128:2883:3883
     ```

     ```
     解释：server.服务器ID=服务器IP地址：服务器之间通信端口：服务器之间投票选举端口
     ```

`注意这里的端口与前面的2181 2182 2183 端口无关！！！`

- 启动集群实际

  进入每个集群实例的bin目录下启动：

  ![image-20191210123101434](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210123101434.png)



# 2.solrCloud 搭建

1. 搭建的要求

   ![image-20191210142652659](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210142652659.png)

   zookeeper作为句群的管理工具

   1. 集群管理：容错、负载均衡。
   2. 配置文件的集中管理
   3. 集群的入口

   需要实现 zookeeper 高可用，需要搭建zookeeper集群。建议是奇数节点。需要三个 zookeeper 服务

   器。

   搭建 `solr 集群需要 7 台服务器`（搭建伪分布式，建议虚拟机的内存 1G 以上）：

   `需要三个 zookeeper 节点`

   `需要四个 tomcat 节点`

2. 准备工作

   - 环境准备

     linux-cent-os

     linux-jdk.tar

     linux-Apache-tomcat-7.0.47.tar

     linux-zookeeper-3.4.6.tar

     linux-solr-4.10.3.tar

   - 步骤

     1. 搭建zookeeper集群（见上文）

     2. 将部署了solr 的tomcat上传到linux

     3. 在linux中创建文件夹 /usr/local/solr-cloud 创建4个tomcat实例

        ```
        [root@localhost ~]# mkdir /usr/local/solr-cloud 
        [root@localhost ~]# cp -r tomcat-solr /usr/local/solr-cloud/tomcat-1 
        [root@localhost ~]# cp -r tomcat-solr /usr/local/solr-cloud/tomcat-2 
        [root@localhost ~]# cp -r tomcat-solr /usr/local/solr-cloud/tomcat-3 
        [root@localhost ~]# cp -r tomcat-solr /usr/local/solr-cloud/tomcat-4
        ```

     4. 将本地的solrhome上传到linux

     5. 在linux中创建文件夹 /usr/local/solrhomes ,将solrhome复制4份 

        ```
        [root@localhost ~]# mkdir /usr/local/solrhomes 
        [root@localhost ~]# cp -r solrhome /usr/local/solrhomes/solrhome-1 
        [root@localhost ~]# cp -r solrhome /usr/local/solrhomes/solrhome-2 
        [root@localhost ~]# cp -r solrhome /usr/local/solrhomes/solrhome-3 
        [root@localhost ~]# cp -r solrhome /usr/local/solrhomes/solrhome-4
        ```

     6. 修改每个solr的 web.xml 文件, 关联solrhome(以第一个solr服务器的修改为例)

        ```xml
        <env-entry> 
        	<env-entry-name>solr/home</env-entry-name> 
        	<env-entry-value>/usr/local/solrhomes/solrhome-1</env-entry-value> 
        	<env-entry-type>java.lang.String</env-entry-type> 
        </env-entry>
        ```

     7. 修改每个tomcat的原运行端口8085 8080 8009 ，分别为

        ```
        8185 8180 8109
        8285 8280 8209
        8385 8380 8309
        8485 8480 8409
        ```

        举一个例子

        ![image-20191210145534565](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210145534565.png)

        ![image-20191210145554770](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210145554770.png)

        文件目录在

        ```
        /usr/local/solr-cloud/tomcat-01/conf/server.xml
        /usr/local/solr-cloud/tomcat-02/conf/server.xml
        /usr/local/solr-cloud/tomcat-03/conf/server.xml
        /usr/local/solr-cloud/tomcat-04/conf/server.xml
        ```

   - 配置集群

     1. 修改每个 tomcat实例 bin 目录下的 catalina.sh 文件，把此配置添加到catalina.sh中( 第237行 ) ： 

        ```properties
        JAVA_OPTS="-DzkHost=192.168.25.128:2181,192.168.25.128:2182,192.168.25.128:2183"
        ```

        JAVA_OPTS ,顾名思义,是用来设置JVM相关运行参数的变量.此配置用于在tomcat启动时找到

        zookeeper集群。

     2. 配置 solrCloud 相关的配置。每个 solrhome 下都有一个solr.xml，把其中的 ip 及端口号配置好（是对应的tomcat的IP和端口）。

        ```
        路径：solrhomes/solrhome-01/solr.xml
        其他类推。。。
        ```

        ```xml
        <solrcloud> 
            <str name="host">192.168.25.128</str> 
            <int name="hostPort">8180</int> 
            <str name="hostContext">${hostContext:solr}</str> 
            <int name="zkClientTimeout">${zkClientTimeout:30000}</int> 
            <bool name="genericCoreNodeNames">${genericCoreNodeNames:true}</bool> </solrcloud>
        ```

        ```
        路径：solrhomes/solrhome-02/solr.xml
        其他类推。。。
        ```

        ```xml
        <solrcloud> 
            <str name="host">192.168.25.140</str> 
            <int name="hostPort">8280</int> 
            <str name="hostContext">${hostContext:solr}</str> 
            <int name="zkClientTimeout">${zkClientTimeout:30000}</int> 
            <bool name="genericCoreNodeNames">${genericCoreNodeNames:true}</bool> </solrcloud>
        ```

        ```
        路径：solrhomes/solrhome-03/solr.xml
        其他类推。。。
        ```

        ```xml
        <solrcloud> 
            <str name="host">192.168.25.128</str> 
            <int name="hostPort">8380</int> 
            <str name="hostContext">${hostContext:solr}</str> 
            <int name="zkClientTimeout">${zkClientTimeout:30000}</int> 
            <bool name="genericCoreNodeNames">${genericCoreNodeNames:true}</bool> </solrcloud>
        ```

        ```
        路径：solrhomes/solrhome-04/solr.xml
        其他类推。。。
        ```

        ```xml
        <solrcloud> 
            <str name="host">192.168.25.128</str> 
            <int name="hostPort">8480</int> 
            <str name="hostContext">${hostContext:solr}</str> 
            <int name="zkClientTimeout">${zkClientTimeout:30000}</int> 
            <bool name="genericCoreNodeNames">${genericCoreNodeNames:true}</bool> </solrcloud>
        ```

     3. 让 zookeeper 统一管理配置文件。需要把 solrhome下collection1/conf 目录上传到zookeeper。上传任意 solrhome 中的配置文件即可。

        我们需要使用solr给我们提供的工具上传配置文件：

        `solr-4.10.3/example/scripts/cloud-scripts/zkcli.sh`

        将solr-4.10.3压缩包上传到linux，解压，然后进入solr-4.10.3/example/scripts/cloud-scripts目录，执行下列命令

        ```java
        //中间可能存在权限问题,给对应的文件权限就行了:
        
        chmod -R 777 文件名
        ```

        

        ```
        ./zkcli.sh -zkhost 192.168.25.128:2181,192.168.25.128:2182,192.168.25.128:2183 -cmd upconfig -confdir /usr/local/solrhomes/solrhome-01/collection1/conf -confname myconf
        ```

        `参数解释`

        -zkhost ：指定zookeeper地址列表

        -cmd ：指定命令。upconfifig 为上传配置的命令

        -confdir : 配置文件所在目录

        -confname : 配置名称

   - 启动集群

     1. 启动每个tomcat实例。`要保证 zookeeper 集群是启动状态`

        ```
        回到根目录：
        cd /
        
        然后执行命令启动tomcat：
        ./usr/local/solr-cloud/tomcat-01/bin/startup.sh
        ./usr/local/solr-cloud/tomcat-02/bin/startup.sh
        ./usr/local/solr-cloud/tomcat-03/bin/startup.sh
        ./usr/local/solr-cloud/tomcat-04/bin/startup.sh
        ```

3. srpingDataSolr连接SolrCloud

   在SolrJ中提供一个叫做CloudSolrServer的类，它是SolrServer的子类，用于连接solrCloud

   它的构造参数就是zookeeper的地址列表，另外它要求要指定defaultCollection属性（默认的

   collection名称）

   我们现在修改springDataSolrDemo工程的配置文件 ，把原来的solr-server注销，替换为

   CloudSolrServer指定构造参数为地址列表，设置默认 collection名称

   1. `修改pinyougou-search-service工程的solr配置文件`

      ```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <beans xmlns="http://www.springframework.org/schema/beans"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xmlns:solr="http://www.springframework.org/schema/data/solr"
             xsi:schemaLocation="http://www.springframework.org/schema/beans
             http://www.springframework.org/schema/beans/spring-beans.xsd
             http://www.springframework.org/schema/data/solr
             http://www.springframework.org/schema/data/solr/spring-solr.xsd">
          <!--&lt;!&ndash;单击版的solr&ndash;&gt;-->
          <!--<solr:solr-server id="solrServer" url="http://localhost:8080/solr/collection2"/>-->
      
          <!--集群版的solr-->
          <bean id="solrServer" class="org.apache.solr.client.solrj.impl.CloudSolrServer">
              <!--构造注入 solr集群的地址列表-->
              <constructor-arg value="192.168.25.128:2181,192.168.25.128:2182,192.168.25.128:2183"/>
              <!--默认的collection-->
              <property name="defaultCollection" value="collection1"/>
          </bean>
          <bean id="solrTemplate" class="org.springframework.data.solr.core.SolrTemplate">
              <constructor-arg name="solrServer" ref="solrServer"/>
          </bean>
      </beans>
      ```

4. 分片设置

   - 创建新的collection进行分片处理。

     在浏览器输入以下地址，可以按照我们的要求 创建新的Collection

     ```
     http://192.168.25.140:8180/solr/admin/collections?action=CREATE&name=collection2&numShards=2&replicationFactor=2
     ```

     **参数：**

     **name**:将被创建的集合的名字

     **numShard**s:集合创建时需要创建逻辑碎片的个数

     **replicationFactor**:分片的副本数。

     看到这个提示表示成功

     ![image-20191210165810223](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210165810223.png)

   - 删除不用的collection 

     ```
     http://192.168.25.140:8480/solr/admin/collections?action=DELETE&name=collection1
     ```

     ![image-20191210170111720](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210170111720.png)

# 3.Redis集群搭建

## 3.1 redis 集群简介

### 3.1.1 什么是redis集群

为何要搭建Redis集群。Redis是在内存中保存数据的，而我们的电脑一般内存都不大，这也就意味着Redis不适

合存储大数据，适合存储大数据的是Hadoop生态系统的Hbase或者是MogoDB。Redis更适合处理高并发，一台设

备的存储能力是很有限的，但是多台设备协同合作，就可以让内存增大很多倍这就需要用到集群。

Redis集群搭建的方式有多种，例如使用客户端分片、Twemproxy、Codis等，但从redis 3.0之后版本支持

redis-cluster集群，它是Redis官方提出的解决方案，Redis-Cluster采用无中心结构，每个节点保存数据和

整个集群状态,每个节点都和其他所有节点连接。其redis-cluster架构图如下：

![image-20191210170744301](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210170744301.png)

客户端与 redis 节点直连,不需要中间 proxy 层客户端不需要连接集群所有节点连接集群中任何一个可用节点

即可。

所有的 redis 节点彼此互联(PING-PONG 机制),内部使用二进制协议优化传输速度和带宽

### 3.1.2 分布式存储机制-槽

1. redis-cluster 把所有的物理节点映射到[0-16383]slot 上,cluster 负责维护node<->slot<->value

2. Redis 集群中内置了 16384 个哈希槽，当需要在 Redis 集群中放置一个 key-value 时，redis 先对key 

   使用 crc16 算法算出一个结果，然后把结果对 16384 求余数，这样每个key 都会对应一个编号在 0-

   16383 之间的哈希槽，redis 会根据节点数量大致均等的将哈希槽映射到不同的节点。

   例如三个节点：槽分布的值如下：

   SERVER1: 0-5460

   SERVER2: 5461-10922

   SERVER3: 10923-16383

### 3.1.3 容错机制-投票

1. 选举过程是集群中所有master参与,如果半数以上master节点与故障节点通信超过(cluster-node-

   timeout),认为该节点故障，自动触发故障转移操作故障节点对应的从节点自动升级为主节点

2. 什么时候整个集群不可用(cluster_state:fail)?

   如果集群任意master挂掉,且当前master没有slave.集群进入fail状态,也可以理解成集群的slot映射

   [0-16383]不完成时进入fail状态

![image-20191210171310591](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210171310591.png)



## 3.2搭建redis集群

### 3.2.1 搭建要求

需要 6 台 redis 服务器。搭建伪集群。

需要 6 个 redis 实例。

需要运行在不同的端口 7001-7006

### 3.2.2 准备工作

1. 安装gcc（如果安装过了跳过此步）

   Redis 是 c 语言开发的。安装 redis 需要 c 语言的编译环境。如果有 gcc 需要在线安装。

   ```
   yum install gcc-c++
   ```

   

2. 使用yum命令安装ruby（我们需要ruby脚本来实现集群的搭建）

   ```
   yum install ruby 
   yum install rubygems
   ```

   `Ruby`

   一种简单快捷的面向对象（面向对象程序设计）脚本语言，在20世纪90年代由日本人松本行弘(Yukihiro 

   Matsumoto)开发，遵守GPL协议和Ruby License。它的灵感与特性来自于 Perl、Smalltalk、Eiffffel、

   Ada以及 Lisp 语言。由 Ruby 语言本身还发展出了JRuby（Java平台）、IronRuby（.NET平台）等其他平

   台的 Ruby 语言替代品。Ruby的作者于1993年2月24日开始编写Ruby，直至1995年12月才正式公开发布于

   fj（新闻组）。因为Perl发音与6月诞生石pearl（珍珠）相同，因此Ruby以7月诞生石ruby（红宝石）命名

   RubyGems简称gems，是一个用于对 Ruby组件进行打包的 Ruby 打包系统

3. 将redis源码包上传到 linux 系统 ，解压redis源码包

4. 编译redis源码 ，进入redis源码文件夹

   ```
   make
   ```

   看到以下输出结果表示编译成功

   ![image-20191210172238580](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210172238580.png)

5. 创建redis 集群的目录/usr/local/redis-cluster,安装6个redis实例：

   ```
   mkdir /usr/local/redis-cluster
   ```

   （在刚刚make的目录下创建到上面指定的目录中）以第一个实例为例安装实例：

   ```
   make install PREFIX=/usr/local/redis-cluster/redis-01
   ```

   ![image-20191210172651616](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210172651616.png)

   出现上面的提示表示安装实例成功！

   ```
   ！注意：这六个实例都是make install 得到的不是copy的！！！！
   ```

6. 复制配置文件 将redis-3.0.0/redis.conf 复制到每个实例的bin中

   ```
   [root@localhost redis-3.0.0]# cp -r redis.conf /usr/local/redis-cluster/redis-01/bin/
   [root@localhost redis-3.0.0]# cp -r redis.conf /usr/local/redis-cluster/redis-02/bin/
   [root@localhost redis-3.0.0]# cp -r redis.conf /usr/local/redis-cluster/redis-03/bin/
   [root@localhost redis-3.0.0]# cp -r redis.conf /usr/local/redis-cluster/redis-04/bin/
   [root@localhost redis-3.0.0]# cp -r redis.conf /usr/local/redis-cluster/redis-05/bin/
   [root@localhost redis-3.0.0]# cp -r redis.conf /usr/local/redis-cluster/redis-06/bin/
   ```

### 3.2.3 配置集群

1. 修改每个redis节点的配置文件redis.conf

   -`修改其中的端口从 7001 到 7006`

   ![image-20191210174705272](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210174705272.png)

   -`将cluster-enabled-yes 前的注释去掉`

![image-20191210174643451](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210174643451.png)

 2. `带配置`启动每个redis实例

    ```java
    //以第一个实例为例启动
    //先进到bin
    cd /usr/local/redis-cluster/redis-1/bin/
    //再带配置启动
    ./redis-server redis.conf
        	//完了之后复制会话进入下个窗口否则redis会退出（如果不想退出也可以后台redis）
    ```

    ![image-20191210175808086](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210175808086.png)

****

![image-20191210175919495](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210175919495.png)

3.上传redis-3.0.0.gem ,安装ruby用于搭建redis集群脚本

```
//在redis.3.0.0.gem 所在的目录下安装 ,先给与权限参照上面的权限授予
gem install redis-3.0.0.gem
```

![image-20191210180450199](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210180450199.png)

4.使用ruby脚本搭建集群

`进入redis源码目录中的src目录 执行命令`：

```
./redis-trib.rb create --replicas 1 192.168.25.128:7001 192.168.25.128:7002 192.168.25.128:7003 192.168.25.128:7004 192.168.25.128:7005 192.168.25.128:7006
```

![image-20191210185243793](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191210185243793.png)

成功则出现以上提示！

## 3.3 连接redis-cluster

### 3.3.1 windows客户端工具连接

redis-client连接集群：

```
redis-cli -h 主机ip -p 端口（集群中任意端口） -c
```

-c：代表连接的是 redis 集群

测试值的存取:

（1）从本地连接到集群redis 使用7001端口加-c 参数

（2）存入name值为abc ，系统提示此值被存入到了7002端口所在的redis （槽是xxxx） 

（3）提取name的值，可以提取

（4）退出（quit） 

（5）再次以7001端口进入 ，不带-c

（6）查询name值，无法获取，因为值在7002端口的redis上 

（7）我们以7002端口进入，获取name值发现是可以获取的,而以其它端口进入均不能获取

### 3.3.2 SpringDataRedis连接Redis集群

修改pinyougou-common工程 添加spring配置文件：

`applicationContext-redis-cluster.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
    <!--0.读取配置文件-->
    <context:property-placeholder ignore-unresolvable="true"
                                  location="classpath*:properties/*.properties"/>

    <!--配置redis的集群配置-->
    <bean id="redisClusterConfiguration" class="org.springframework.data.redis.connection.RedisClusterConfiguration">
        <property name="clusterNodes">
            <set>
                <bean class="org.springframework.data.redis.connection.RedisClusterNode">
                    <constructor-arg name="host" value="${redis.host1}"/>
                    <constructor-arg name="port" value="${redis.port1}"/>
                </bean>
                <bean class="org.springframework.data.redis.connection.RedisClusterNode">
                    <constructor-arg name="host" value="${redis.host2}"/>
                    <constructor-arg name="port" value="${redis.port2}"/>
                </bean>
                <bean class="org.springframework.data.redis.connection.RedisClusterNode">
                    <constructor-arg name="host" value="${redis.host3}"/>
                    <constructor-arg name="port" value="${redis.port3}"/>
                </bean>
                <bean class="org.springframework.data.redis.connection.RedisClusterNode">
                    <constructor-arg name="host" value="${redis.host4}"/>
                    <constructor-arg name="port" value="${redis.port4}"/>
                </bean>
                <bean class="org.springframework.data.redis.connection.RedisClusterNode">
                    <constructor-arg name="host" value="${redis.host5}"/>
                    <constructor-arg name="port" value="${redis.port5}"/>
                </bean>
                <bean class="org.springframework.data.redis.connection.RedisClusterNode">
                    <constructor-arg name="host" value="${redis.host6}"/>
                    <constructor-arg name="port" value="${redis.port6}"/>
                </bean>
            </set>
        </property>
    </bean>

    <!--配置redis的连接池-->
    <bean id="poolConfig" class="redis.clients.jedis.JedisPoolConfig">
        <property name="maxIdle" value="${redis.maxIdle}" />
        <property name="maxWaitMillis" value="${redis.maxWait}" />
        <property name="testOnBorrow" value="${redis.testOnBorrow}" />
    </bean>
    <!--2.配置connectionFactory工厂对象 -->
    <bean id="connectionFactory" class="org.springframework.data.redis.connection.jedis.JedisConnectionFactory">
        <!--2.1)引入集群的配置-->
        <constructor-arg name="clusterConfig" ref="redisClusterConfiguration"/>
        <!--引入连接池-->
        <constructor-arg ref="poolConfig"/>
    </bean>
    <!--配置redisTemplate对象 -->
    <bean id="redisTemplate" class="org.springframework.data.redis.core.RedisTemplate">
        <property name="connectionFactory" ref="connectionFactory"/>
    </bean>
</beans>
```



