> ​       Weblogic是一个更企业级的application server，从它是一个需要付费的软件就可知，而且它是Oracle旗下的一款产品。由于它的付费性，所以中小企业应该很少会选择它作为application server，更多可能选择的是免费开源的产品，比如Apache Tomcat。
>
> 


```
official docs：
https://docs.oracle.com/middleware/12211/wls/INTRO/intro.htm#INTRO123
```



### 域(Domains)

* 概念

```
     域是一个逻辑概念，它和一组Oracle Weblogic Server资源相关。域中包括了两种角色，一种是Administration Server(控制中心，配置和管理域中的资源)，一种是Managed Server，放置Web applications, EJBs, Web services, 和其它资源的地方。实际生产环境一般会让Administration Server 只充当管理员的角色，而不会将应用部署到上面，除非是开发环境，为了节省会让其既充当管理员和被管理员角色。
```
* 域和WLS的关系
```
一个Weblogic Server可以包含多个域在里面，一个域也可以包含多个Weblogic Server，具体可以看官方文档的哪张图，画得太好了。
https://docs.oracle.com/middleware/12211/wls/INTRO/domains.htm#INTRO176
```

* 域的划分原则

```
1.逻辑区分。比如根据系统的职责来划分域，将购物车系统和后台计算系统划分为两个域。
2.物理位置。处于不同物理位置的机房的WLS划分为不同的域来管理。
3.数量大小。
```

* 域的组成

```
官方那张图太好了。
https://docs.oracle.com/middleware/12211/wls/INTRO/domains.htm#INTRO178
```

```
一个域可以包括一个Administration Server，stand-alone Managed Servers，a cluster of Managed Servers。在一个域中，有且只有一个Administration Server(域中必须要有一个)，多个单独的Managed Servers(没有集群的)，和多个集群（加入集群的Managed Servers）。

加入集群和没加入集群的Managed Servers的关键区别是对failure 和load balancing的支持。

```

* Administration Server

```
充当着整个域中配置文件的控制中心，维护着域中的配置文件并且当配置文件有变化时，要将这些变化同步给Managed Servers。

可以通过administration tools（listed in "Summary of System Administration Tools and APIs）
和Administration Server交互(通信)。
```

* Managed Servers and Managed Server Clusters

```
   Managed Servers 存放(host)业务应用程序，应用组件，web服务以及相关的资源。基于优化性能的目的，Managed Servers持有一份所在域的配置文件的副本(这样子不用每次都去访问Administration Server所在的机器，较少网络io)，当Managed Servers启动的时候，它会去连接Administration Server并将其维护的配置文件同步过来。
  生产环境中，为了日益增长的性能，吞吐量，高可用，可以配置多台Managed Servers形成一个集群。处于集群中的 Managed Servers和非集群的Managed Servers的关键区别在于对failure和load balancing的支持(这是集群才有的功能)。
```

