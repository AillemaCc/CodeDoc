# REDIS

## 认识redis

### 认识nosql

sql我们比较熟悉，它对应着关系型数据库。

那么nosql就是非关系型数据库了。也有人说是not only sql--不止数据库

数据库最后的目的肯定是数据的增删改查

### CRUD方面的差异

#### 结构化：

存入关系型数据库的数据，都是结构化的数据。也就是说这些数据都有格式上的要求，就像各个表的数据里面，有主键，有约束。数据本身也有数据类型，数据长度的要求。这些都是所谓的结构化。这些约束建立好之后，表的结构也随之确定。后续对数据操作，都要严格遵循这个表的结构

一般来说，表的结构在使用之前就要确定好，并且不能随便的修改。这导致了有时候，这种形式会变得比较死板

那么nosql呢？他们是非结构化的数据库

以redis为例，他就使用了一种key+value的方式。对于key的约束几乎就是没有，当然了，对value也是一样。

除此之外，还有document类型的nosql，可以说是把数据存储到文档当中。类似于json的形式。字段的约束非常松散。

还有图类型的数据库，存入数据库的每一个元素可以看成一个节点。这个东西做的很少

上面的就是常见的nosql数据库，对于数据结构没有严格的要求。也可以随意地修改表的内容

#### 关联性

sql型数据库经常能看到表之间的关联，那么nosql类型数据库，一般都是采用json类型来进行这种关联的维护--json文档嵌套

但是这样的数据存储，有一个缺点，就是大量的重复。表之间没有任何所谓的关联

#### 查询方式

sql类型的查询就不用多说了，使用sql语句就可以。格式语法都是固定的。只要是关系型数据库，都能够使用相同的语句进行查询。

相对应的，nosql库的查询没有固定的语法格式，并不统一。redis和mongodb的查询语法也不一样。

这种方式有什么优点呢--灵活熟悉

使用起来相对简单，但是使用不同的库，需要改为使用不同的语法

#### 事务

sql类型数据库，底层就实现了ACID的事务特性

nosql要么没有事务，要么就只能满足很少的ACID特性。BASE满足。

假如你对于数据的安全性要求较高，就应该选择sql类型数据库了

------

### 认识redis

remote dictionary server

远程词典服务器，是一个基于内存的key value nosql数据库



特征：

* key value型
* 单线程 每个命令具备原子性。但是redis6.0的多线程，是指对于网络请求处理部分的。单线程会有性能差的缺点吗？不会哦
* 低延迟是redis的特性之一，因为他基于内存存储，存在io多路复用的方式，大大提高了整个服务的吞吐能力。良好的编码情况也让他的延迟更低。
* 支持数据持久化 内存的查询效率确实很高，但是你断电，内存就没用了。所以redis定期会把基于内存的存储，存储到磁盘当中。
* 支持主从集群，分片集群
* 支持多编程语言

### 安装redis

不写了

## redis常见命令

### redis数据结构介绍

key一般是string类型，但是他的值的类型多种多样：
string hash list set sortedset geo bitmap hyperlog

这些当然也只是一部分

前五种可以称为基本类型

剩下的三种往往用到一些特殊的数据统计。但他们都是基于基本类型。称为特殊类型

------

#### 怎么用？

##### 通用命令，是对所有key都有用的

* KEYS:查看符合模板的所有key `KEYS *`查看所有的key 所谓的模版，就是关键词。这个查询是基于模糊查询来做的。当redis的数据量很大的时候，这个查询会非常之慢。所以不建议在生产环境当中使用。会阻塞所有的请求
* DEL：删除一个指定的key 返回值代表删除的数量
* EXISTS：判断一个key是否存在
* EXPIRE：给一个key设置有效期，有效期到期，key自动删除，单位是s
* TTL：查看一个key的剩余有效期

#### String类型

字符串类型是redis当中最简单的存储类型

value是祖父穿，不过根据字符串的格式不同，也可以分为三类：

* string 普通字符串
* int 整数类型 可以做自增 自减操作
* float 浮点类型 自增自检

不管是那种格式，底层都是字节数组形式存储。只不过是编码方式不同。字符串类型的最大空间不能超过512M

常见命令如下：

* SET:添加或者修改已经存在的一个键值对
* GET：根据key获取string类型的value
* MSET：批量添加多个string类型的键值对
* MGET：根据多个key获取多个string类型的value
* INCR：让一个整形的key自增1
* INCRBY：让一个整形的key自增并且指定步长
* SETNX：添加一个String类型的键值对，前提是这个key不存在，否则不执行
* SETEX：添加一个String类型的键值对，并且指定有效期

#### Key的层级格式：

redis当中没有table的概念，我们该如何区分不同类型的key呢？

比如说吧，需要存储用户，商品信息到redis，有一个用户id为1，有一个商品id恰好也是1。怎么区分这两个id1

在redis当中，key允许有多个单词形成层级结构，多个单词之间使用“：”分割开来。

比如：`fuck:user:1`  `shit:item:1`

如果value是一个java对象，例如一个user对象，就可以将对象序列化为json字符串后存储。

#### HASH类型：

散列 他的value是一个无序字典。类似于java当中的hashmap

上面的字符串结构是将对象序列化为json字符串之后，来进行存储。但是要需要修改对象某个字段时，很不方便。

hash结构可以将对象中的每个字段独立存储，可以针对单个字段做CRUD

 Redis中存储的都是键值对，这些键值对本身就是用哈希的方式来组织的。我们要讲解的哈希是指的键值对中的 value。也就是 key 所对应的 value 的类型是Hash。value的Hash类型可以看作是一个键值对的容器，其中的键又被称为field(用于区分 Redis 整体的键值对（key-value))，值被称为value。例如key = "key"，value={ {field1, value1 } ,..., {fieldN, valueN } }，


![](http://photos.swindle.icu/picture/typora%E5%9B%BE%E7%89%87%E5%AD%98%E5%82%A8/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-11-20%20195821.png)

#### LIST类型

 列表类型是用来存储多个有序的字符串，a、b、c、 d、e五个元素从左到右组成了一个有序的列表，列表中的每个字符串称为元素(element) ，一个列表最多可以存储2^32-1个元素。在Redis 中，可以对列表两端插入(push)和弹出 (pop)，还可以获取指定范围的元素列表、获取指定索引下标的元素等。列表是一种比较灵活的数据结构，它可以充当栈和队列的角色，在实际开发上有很多应用场景。
![](http://photos.swindle.icu/picture/typora%E5%9B%BE%E7%89%87%E5%AD%98%E5%82%A8/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-11-21%20103634.png)

Redis中的List还是有别于其他的链表的，其特点如下：

    列表中的元素是有序的，这意味着可以通过索引下标获取某个元素或者某个范围的元素列表，例如要获取上图的第5个元素，可以执行lindex user:1:messages 4或者倒数第1个元素，lindexuser:1:messages -1就可以得到元素e。
    区分获取和删除的区别，例如上图中的lrem 1 b是从列表中把从左数遇到的前1个b元素删除，这个操作会导致列表的长度从5变成4;但是执行lindex 4只会获取元素，但列表长度是不会变化的。
    列表中的元素是允许重复的，例如列表中包含了两个 a 元素。

  注意：上述提到列表是有序的，这里的有序并非只的是大小的有序，而是指的相对顺序是有序的，也就是相对顺序改变了，那么该列表就与原列表不同了！

  提到列表中的元素可以重复，那么我们就应该想到Hash是不允许有重复的 field 的，同时我们在设置String时，其对应的key也是不可以重复的。


总结一下特征：

* 有序
* 元素可以重复
* 插入和删除快
* 查询速度一般

![](http://photos.swindle.icu/picture/typora%E5%9B%BE%E7%89%87%E5%AD%98%E5%82%A8/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-11-21%20104046.png)

## redis的java客户端

最后我们实现业务，就是需要用编程语言来实现

我们这次使用jedis：简单实用，学习成本低。但是jedis实例是线程不安全的。多线程环境之下，需要基于连接池来使用。

剩下的经常使用的还有两种：lettuce是基于netty实现的，支持同步 异步 响应式编程方式，并且是线程安全的。支持redis的哨兵模式 集群模式和管道模式；另外一种是redission 是一个基于redis实现的分布式，可伸缩的java数据结构合集

### jedis快速入门

~~~~java
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import redis.clients.jedis.Jedis;

public class jedisTest {
    private Jedis jedis;

    @BeforeEach
    void setup(){
        jedis = new Jedis("localhost");
        jedis.select(8);
    }

    @Test
    void test(){
        String result = jedis.set("name", "fuck");
        String name = jedis.get("name");
        System.out.println(name);
    }

    @AfterEach
    void teardown(){
        if(jedis != null){
            jedis.close();
        }
    }
}

~~~~

引入依赖的部分不说了

jedis本身是线程不安全的，并且频繁地创建和销毁连接，会有性能损耗。因此最好使用jedis连接池替代jedis的直连方式。

~~~~java
package utils;

import redis.clients.jedis.Jedis;
import redis.clients.jedis.JedisPool;
import redis.clients.jedis.JedisPoolConfig;

public class JedisConnectionFactory {
    private static final JedisPool jedisPool;
    static {//连接池配置
        JedisPoolConfig config = new JedisPoolConfig();
        config.setMaxIdle(10);
        config.setMinIdle(0);
        config.setMaxTotal(10);
        config.setMaxWaitMillis(5000);
        config.setTestOnBorrow(true);
        config.setTestOnReturn(true);
        config.setTestWhileIdle(true);
        jedisPool = new JedisPool(config, "localhost", 6379);

    }

    public static Jedis getJedis() {//只需要调用这个工具类的getjedis方法，就能从线程池当中拿到jedis对象
        return jedisPool.getResource();
    }
}

~~~~

### SpringDataRedis

* SDR提供了对不同redis客户端的整合
* 提供了redistemplate统一api来操作redis
* 支持redis的发布订阅模型
* 支持redis哨兵和redis集群
* 支持基于lettuce的响应式编程
* 支持基于JDK JSON 字符串 SPRING对象的数据序列化以及反序列化 也就是把他们转化成字节

核心是redistemplate封装的api

![](http://photos.swindle.icu/picture/typora%E5%9B%BE%E7%89%87%E5%AD%98%E5%82%A8/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-11-23%20140639.png)

这些返回值 封装了对相应类型的操作。能够让类不那么臃肿

### SDR快速入门

~~~~xml
<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-redis</artifactId>
            <version>2.5.0</version>
        </dependency>
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-pool2</artifactId>
            <version>2.12.0</version>
        </dependency>
~~~~

引入上面的依赖

配置文件：

~~~~yml
spring:
  redis:
    host: localhost
    port: 6379
    lettuce:
      pool:
        max-active: 8
        max-idle: 8
        min-idle: 0
        max-wait: 100
~~~~

注入redistemplate

~~~~java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.stereotype.Component;

@Component
public class redistemplate {
    @Autowired
    private RedisTemplate redisTemplate;
}

~~~~

编写测试 正常随便写点

### RedisSerializer

主要用于在Java等编程语言中，将对象在存储到Redis之前进行序列化，以及在从Redis读取时进行[反序列化](https://so.csdn.net/so/search?q=反序列化&spm=1001.2101.3001.7020)。

RedisSerializer是Redis客户端库（如Jedis、Lettuce等）中用于序列化和反序列化Java对象到Redis字节数组的接口或组件。由于Redis是一个基于内存的键值存储系统，它只支持字符串（bytes）、列表（list）、集合（set）、有序集合（zset）等简单数据结构，而不支持直接存储Java对象。因此，当需要将Java对象存储到Redis时，必须先将对象序列化为字节数组；反之，从Redis读取对象时，也需要将字节数组反序列化为Java对象。

RedisSerializer提供了两个主要的方法：serialize和deserialize。

    serialize方法用于将Java对象转换为字节数组，以便存储到Redis中。
    deserialize方法用于将Redis中的字节数组转换回Java对象。

RedisSerializer有多种实现方式，包括但不限于以下几种：

    JdkSerializationRedisSerializer：使用Java的默认序列化机制（JDK序列化）进行序列化和反序列化。这种方式简单直接，但生成的字节数组较大，包含大量的类元数据信息，且反序列化性能较低。
    StringRedisSerializer：使用字符串进行序列化和反序列化。这种方式适用于存储和检索字符串类型的数据，但不适用于复杂的Java对象。
    Jackson2JsonRedisSerializer或GenericJackson2JsonRedisSerializer：基于Jackson库实现，将Java对象序列化为JSON格式的字符串，并存储到Redis中。这种方式在序列化和反序列化性能上通常优于JDK序列化，且生成的字节数组较小，但要求Java对象具有无参构造函数和getter/setter方法。
    FastJsonRedisSerializer：基于Fastjson库实现，与Jackson2JsonRedisSerializer类似，但使用的是Fastjson库进行JSON序列化和反序列化。
编写配置类来配置序列化器：

~~~~java
@Configuration
public class RedisConfig {

    @Bean
    public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory connectionFactory) {
        RedisTemplate<String, Object> template = new RedisTemplate<>();
        template.setConnectionFactory(connectionFactory);

        // 使用StringRedisSerializer来序列化和反序列化key
        template.setKeySerializer(new StringRedisSerializer());

        // 使用Jackson2JsonRedisSerializer来序列化和反序列化value
        Jackson2JsonRedisSerializer jackson2JsonRedisSerializer = new Jackson2JsonRedisSerializer(Object.class);
        ObjectMapper om = new ObjectMapper();
        om.setVisibility(PropertyAccessor.ALL, JsonAutoDetect.Visibility.ANY);
        om.enableDefaultTyping(ObjectMapper.DefaultTyping.NON_FINAL);
        jackson2JsonRedisSerializer.setObjectMapper(om);
        template.setValueSerializer(jackson2JsonRedisSerializer);

        // 类似地，可以设置hashKeySerializer和hashValueSerializer

        return template;
    }
}

~~~~

