# ElasticSearch总结文档

## 1.简介

### 1.1 什么是es

Elasticsearch是一个实时的分布式搜索和分析引擎。它可以帮助你用前所未有的速 度去处理大规模数据。

ElasticSearch是一个基于Lucene的搜索服务器。它提供了一个分 布式多用户能力的全文搜索引擎，基于

RESTful web接口。Elasticsearch是用Java开发的，并作为Apache许可条款下的开放源码发布，是当前流行的

企业级搜索引擎。设计用于云计算中，能够达到实时搜索，稳定、可靠、快速，安装使用方便。

### 1.2 es特点

（1） 可以作为一个大型分布式集群（数百台服务器）技术，处理PB级数据，服务大公司；也可以运行在单机上

（2） 将全文检索、数据分析以及分布式技术，合并在了一起，才形成了独一无二的ES； 

（3） 开箱即用的，部署简单

（4） 全文检索，同义词处理，相关度排名，复杂数据分析，海量数据的近实时处理

### 1.3 es体系结构

| ElasticSearch    | 关系型数据库MySQL   |
| ---------------- | ------------------- |
| 索引（index）    | 数据库（databases） |
| 类型（type）     | 表（table）         |
| 文档（document） | 行（row）           |

## 2.ElasticSearch的启动与部署

启动ES：

```shell
#在官方网站现在一个Realese版本
https://www.elastic.co/downloads/past-releases/elasticsearch-5-6-8
#解压安装
```

进入`bin` shift+鼠标右键 进入cmd

```
elasticsearch	    #完成启动
```



> 测试：在浏览器输入：localhost:9200  即可查看是否启动成功

成功界面：

![image-20191219115704324](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191219115704324.png)

### 2.1 postman调用restAPI操作es索引库

#### 2.1.1 新建索引库

psotman 以put方式

```sh
127.0.0.1：9200/articleindex
```

![image-20191219120115422](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191219120115422.png)

#### 2.1.2 新建文档

> postman以post方式：localhost:9200/articleindex/article2
>
> 请求体中加入文档内容：
>
> {
> 	"title":"123java is the best one123",
> 	"content":"123welcome to study elasticsearch123"
>
> }

![image-20191219120259399](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191219120259399.png)

#### 2.1.3 查询全部文档

> postman以get请求：localhost:9200/articleindex/article2/_search
>
> 上面表示索引为articleindex，类型为article2中的所有文档

![image-20191219120632013](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191219120632013.png)

#### 2.1.4 按照文档id查询

> postman以get请求：localhost:9200/articleindex/article2/文档id

#### 2.1.5 按照文档中的字段基本匹配查询

> postman以get请求：localhost:9200/articleindex/article2/_search?q=字段名:值

#### 2.1.6 按照文档中的字段模糊查询

> postman以get请求：localhost:9200/articleindex/article2/_search?q=字段名:*值\*

#### 2.1.7 删除文档

> postman以delete请求：localhost:9200/articleindex/article2/文档id

### 2.2 HEAD插件操作es索引库

#### 2.2.1安装HEAD插件：

> 1. 下载：https://github.com/mobz/elasticsearch-head 
>
> 2. 解压到任意目录但是要和es的目录区别开（因为解压后的名字一样）
>
> 3. `安装node.js`，然后安装cnpm*（Node.js可以去官网下载）
>
>    ```shell
>    npm install -g cnpm --registry=https://registry.npm.taobao.org
>    ```
>
> 4. 将grunt安装为全局命令。Grunt是基于Node.js的项目构建工具（与maven相似），他可以自动运行你所设定的项目
>
>    ```shell
>    npm install -g grunt-cli
>    ```
>
> 5. 安装依赖：（`一定要在HEAD目录下`）
>
>    ```shell
>    cnpm install
>    ```
>
> 6. 进入head目录启动head，在命令提示符下输入命令
>
>    ```shell
>    grunt server
>    ```
>
> 7. 测试：浏览器输入
>
>    ```
>    localhost:9100
>    ```
>
>    `F12发现有跨域访问权限不足错误`
>
>    No'Access-Control-Allow-Origin'header is present on the requested resource这个错误是由于elasticsearch默认不允许跨域调用，而elasticsearch-head是属于前端工 程，所以报错。我们这时需要修改elasticsearch的配置，让其允许跨域访问。
>
> 8. `修改elasticsearch配置文件`：elasticsearch.yml，增加以下两句命令：
>
>    ```sh
>    http.cors.enabled: true 
>    http.cors.allow-origin: "*"
>    ```
>
> 9. 进入第七步看到如下界面成功：
>
>    ![image-20191219143842837](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191219143842837.png)
>
>    
>
>    
>
>    ![](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191219143821238.png)

#### 2.2.2测试HEAD的添加

> ![image-20191219144259343](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191219144259343.png)

#### 2.2.3测试HEAD修改



> `URL中 ip+端口+索引库名+类型名+文档id 请求体内 是要修改的内容`
>
> ![image-20191219144822575](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191219144822575.png)

#### 2.2.4测试HEAD的查询

> `URL中 ip+端口+索引库名+类型名+文档id`
>
> ![image-20191219145024650](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191219145024650.png)

#### 2.2.4测试HEAD删除

> `URL中是 ip+端口+索引库名+类型名+文档id 请求是delete请求`
>
> ![image-20191219145531801](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191219145531801.png)
>
> 

### 2.3 java微服务项目操作es

## 3.IK分词器

### 3.1 es自带普通分词器测试

> 浏览器地址输入：http://127.0.0.1:9200/_analyze?analyzer=chinese&pretty=true&text=我是程序员
>
> ![image-20191219151348503](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191219151348503.png)
>
> 可以看到es自带的分词器是对中文一个一个的分显然不符合中国人的分词

### 3.2 安装IK分词器

> 下载地址：https://github.com/medcl/elasticsearch-analysis-ik/releases 
>
> 安装步骤：
>
> （1） 先将其解压，将解压后的elasticsearch文件夹重命名文件夹为ik
>
> （2） 将ik文件夹拷贝到elasticsearch/plugins 目录下。
>
> （3） 重新启动，即可加载IK分词器

### 3.3 自定义词库

> 在插件ik中的配置文件中（`/plugins/ik/confifig/下添加my.dic文件`）
>
> ![image-20191219153154519](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191219153154519.png)

> `注意`：`分词器的.dic文件必须保存为 无bom的UTF-8编码文件`  保存后重启es 启动词库

> 地址栏输入：http://127.0.0.1:9200/_analyze?analyzer=ik_smart&pretty=true&text=王太平是世界上最帅的男人
>
> ![image-20191219152754016](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191219152754016.png)

## 4.在java微服务项目中使用es

### 4.1 创建项目添加依赖

![image-20191219185357171](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191219185357171.png)

spring date 与 es整合

```xml
 <dependency>
     <groupId>org.springframework.data</groupId>
     <artifactId>spring-data-elasticsearch</artifactId>
 </dependency>
```

### 4.2 控制器

```java
@RestController
@RequestMapping("article")
@CrossOrigin    //该注解一定要加上  允许跨域访问
public class ArticleController {
    @Autowired
    private ArticleService articleService;
    
    /**
     * 关键字查询带分页
     * @param keyword
     * @param page
     * @param size
     * @return
     */
    @GetMapping("search/{keyword}/{page}/{size}")
    public Result searchPage(@PathVariable String keyword,@PathVariable int page,@PathVariable int size){
        try {
            PageResult<Article> articlePageResult = articleService.searchPage(keyword,page,size);
            return new Result(true,StatusCode.OK,"searchPage OK",articlePageResult);
        } catch (Exception e) {
            e.printStackTrace();
            return new Result(false,StatusCode.ERROR,"searchPage NOT");
        }
    }
}

```

### 4.3 service服务

```java
@Service
public class ArticleService {
    @Autowired
    private ArticleDao articleDao;
    @Autowired
    private IdWorker idWorker;
    
    public PageResult<Article> searchPage(String keyword, int page, int size) {
        Page<Article> byContentOrTitleLike = articleDao.findByContentAndTitleLike(keyword, keyword, PageRequest.of(page-1, size));
        return new PageResult<>(byContentOrTitleLike.getTotalElements(),byContentOrTitleLike.getContent());
    }
}
```

### 4.4 dao数据访问层

```java
public interface ArticleDao extends ElasticsearchRepository<Article,String> {
    Page<Article> findByContentAndTitleLike(String title, String content, Pageable pageable);
}
```

### 4.5 postman测试

![image-20191219185726972](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191219185726972.png)

## 5.使用logstash完成mysql同步到es（增量）

### 5.1 what is logstash？

Logstash是一款轻量级的日志搜集处理框架，可以方便的把分散的、多样化的日志搜集 起来，并进行自定义的处理，然后传输到指定的位置，比如某个服务器或者文件。

### 5.2 logstash安装与测试

