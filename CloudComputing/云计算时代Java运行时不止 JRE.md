# 云计算时代 Java 运行时不止 JRE

## 前言

Java 语言于 1995 年由 Sun 公司首次发布，次年发布了 Java 开发工具包也就是常说 Java Development Kit 简称 JDK1.0，截止到目前为止最新的版本为 JDK13.0。JRE（Java Running Environment）即 Java 运行环境，包括 JVM、核心类库、核心配置工具库等。

在云计算时代，部分开发者对 Java 运行环境的了解还局限在比较早期的基础设施角度，限制了很多架构设计，也造成了很多不必要研发投入。

本文尝试基于自己的见闻梳理一下，在当下的技术条件下，Java 的运行环境有哪些？以便于开发者可以选择一个相对更合理的基础设施上，开展研发工作。

## 1.0 单机时代

单机时代也是 Java 语言诞生的年度，标准的 JRE 是比较好的选择，有些开发者喜欢用 JDK 做运行环境，有其合理性。

在这个时代或者这种模式下，依然有很多选择，包括 JRE、JDK 的不同发行商的不同版本，主流的包括 Oracle、Sun 的版本，以及由  IBM、SAP、微软等发布基于OpenJDK的版本。整体基本兼容，但受一些商业版权、安全、发行商环境等原因，还是略有一些差别。另外，还有一支流是国产 CPU 厂商及操作系统厂商发布的 JDK。

Java 开发者都熟悉 JVM（Java Virtual Machine），但很多人不了解的是不同发行版中的 JVM 核心可能是不同的。有兴趣的同学可以阅读一下《深入理解Java虚拟机：JVM高级特性与最佳实践》。

在这里推荐大家试用下一下阿里发布的 OpenJDK : Alibaba Dragonwell（<https://www.aliyun.com/product/dragonwell>）。它是一款免费的, 生产就绪型Open JDK 发行版，提供长期支持，包括性能增强和安全修复。Alibaba Dragonwell作为Java应用的基石，支撑了阿里经济体内所有的Java业务，完全兼容 Java SE 标准，可以在任何常用操作系统（包括 Linux、Windows 和 macOS）上开发 Java 应用程序， 运行时生产环境选择Alibaba Dragonwell。（GitHub:<https://github.com/alibaba/dragonwell8>）

## 2.0 Web 时代

Web 时代最知名就是那只叫 Tomcat 的猫，属于 Apache 基金会的项目。Tomcat 服务器是一个免费的开放源代码的Web 应用服务器，属于轻量级应用服务器。虽然它具有处理HTML页面的功能，但大家更多是将其作为Servlet和JSP容器。（<http://tomcat.apache.org/index.html>）

这一次进步的意义在于：开发者可以专注于应用逻辑开发，而不用关心网络通讯以及如何让应用作为一个服务来运行，相关职责转交给了 Tomcat。

对等的应用服务器还有WebLogic、JBoss 等等。

## 3.0 大数据时代

大数据时代最知名的系统当推 Hadoop。其核心是借鉴Google的那篇MapReduce论文里所说的思想：Our abstraction is inspired by the map and reduce primitives present in Lisp and many other functional languages。

Hadoop 框架是由 Java 开发的，虽然 MapReduce 应用程序不一定用 Java 开发，但血溶于水的 Java 是比较好的选择。尤其那个著名的示例 WordCount 就是基于 Java 编写。（<http://hadoop.apache.org/docs/r1.2.1/mapred_tutorial.html>）

这一次进步的意义在于：Java开发者可以不用关心数据处理框架，只需要聚焦在如何用 MapReduce 的思想来拆解要做计算任务。

对等的还有Apache Spark及这两年比较火的 Apache Flink。不过不同大数据框架的计算模型有差异。

## 4.0 云计算时代

如今我们处在云计算时代，面临的可选方案就多了很多。善用这些新的 Java 运行环境，会让开发者的效率有质的提升。

### 4.0.1 伪云计算版

伪云计算版就是买一台 ECS，在上面按照单机时代或者 web 时代的模式运行 Java 程序。这种模式的好处很明显。

* 学习成本低，上手快。
* 线下迁移线上速度快，几乎不需要多少改造。
* 初始化阶段的货币化投入少。

这种模式本质上是在利用云计算的虚拟化特性+硬件运维服务外包，对于开发者而言没有什么质的变化，还得不断的发明轮子。

### 4.2 真云时代的运行时

如今公有云厂商提供了很多更多封装的Java 运行环境，以期让开发者专注于更有价值的创造工作。下面以阿里云的产品为例来介绍，如何进一步将非核心业务的开发任务外包给运行环境。

#### 4.2.1 企业级分布式应用服务 EDAS

企业级分布式应用服务（Enterprise Distributed Application Service, 简称 EDAS）以阿里巴巴中间件团队多款久经沙场的分布式产品作为核心基础组件，面向企业级云计算市场提供高可用分布式解决方案，是阿里巴巴企业级互联网架构解决方案的核心产品。EDAS 充分利用阿里云的资源管理和服务体系，引入阿里巴巴中间件整套成熟的分布式产品，帮助企业级客户轻松构建大型分布式应用服务系统。

EDAS是一个应用托管和微服务管理的 PaaS 平台，提供应用开发、部署、监控、运维等全栈式解决方案，同时支持 Spring Cloud、Dubbo 等微服务运行环境。开发者可以选择WAR、JAR、镜像等不同模式来部署引用。

这种模式的好处是：开发者在企业级平台上编写业务代码，代码一经部署，整个系统即拥有了企业级的高可用能力，省去了自选、自学、自建、自管的行业标杆级方案的学费和时间。

#### 4.2.2 Web应用托管服务(WEB+)

Web应用托管服务（Web+）是一款用来运行并管理Web类、移动类和API类应用程序的PaaS产品，可以使用Java编写并构建应用程序。在无需管理底层基础设施的情况下，即可简单、高效、安全而又灵活的对应用进行部署、伸缩、调整和监控。

开发者只需要关注应用代码，即可在零服务器管理和配置的情况下发布一个应用部署环境。在团队内部，可通过文件共享或源代码管理的方式快速分发配置描述文件给所有成员从而快速拉起部署环境。若使用的是开源技术，可使用Web+官方或开源提供方分发的公共配置描述文件来快速搭建测试或生产环境。

这种模式的好处是：开发者可以集中精力编写代码，将管理和配置服务器、数据库、负载均衡器、防火墙和网络等工作交由Web+代劳，相对于 EDAS 会轻量一些。

## 5.0 函数即服务

函数即服务的核心是让开发者进一步聚焦业务代码，其中Serverless 应用引擎略重，函数计算至轻。

### 5.1 Serverless 应用引擎

Serverless 应用引擎（Serverless App Engine，简称 SAE）是面向应用的 Serverless PaaS 平台，帮助 PaaS 层用户免运维 IaaS，按需使用，按量计费，实现低门槛微服务应用上云，有效解决成本及效率问题。支持 Spring Cloud、Dubbo 和 HSF 等流行的开发框架，真正实现了 Serverless 架构和微服务架构的完美融合。除了微服务应用外，后续还会支持更多其它类型的应用。

区别于其它 Serverless 产品，SAE 支持 Spring Cloud、Dubbo 等开发框架，真正实现了 Serverless 架构 + 微服务架构的完美结合。支持 WAR、JAR、镜像三种方式部署，让零容器基础的初级用户也能享受 Kubernetes 的技术红利。

### 5.2 函数计算

函数计算（Function Compute）是一个事件驱动的全托管 Serverless 计算服务。开发者无需管理服务器等基础设施，只需编写代码并上传。函数计算会为开发者准备好计算资源，并以弹性、可靠的方式运行代码。

当前云计算的抽象粒度大多在机器级别，要管理和使用这些计算资源仍然有不小的门槛和成本。阿里云函数计算为解决计算成本和效率问题而生，将计算服务的抽象粒度提高到了函数级别，打造无服务器概念的应用设计模式。

使用函数计算，开发者将业务代码部署到函数计算，并以事件驱动的方式触发函数执行，服务就可以平稳运行。开发者无需再为环境部署、服务器扩容、服务器宕机等问题烦恼，函数计算提供弹性的扩容机制，并按量计费。此外，函数计算提供日志查询、性能监控和报警等功能，帮助快速定位问题、排查故障。

这种模式的意义在于：让开发者回归到函数层面，关注入参、出参、业务逻辑。当然额外的代价是，需要开发者重新基于新的基础设施，来构思服务架构，很多既有的经验都需要重构。

示例如下：

```Java
package example;
import com.aliyun.fc.runtime.Context;
import com.aliyun.fc.runtime.StreamRequestHandler;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
public class HelloFC implements StreamRequestHandler {
    @Override
    public void handleRequest(
            InputStream inputStream, OutputStream outputStream, Context context) throws IOException {
        // 在此编写业务代码
        outputStream.write(new String("hello world").getBytes());
    }
}'
// pom.xml
<dependency>
    <groupId>com.aliyun.fc.runtime</groupId>
    <artifactId>fc-java-core</artifactId>
    <version>1.0.0</version>
</dependency>
```
