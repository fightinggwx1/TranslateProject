监控微服务的5条原则
====

![](http://thenewstack.io/wp-content/uploads/2016/09/toppicsysdig.jpg)

我们对微服务的需求可以归纳为一个词：速度，提供更多更可靠更快捷的功能的需求，彻底改变了软件开发模式，毫无疑问，这同样改变了软件管理和系统监控的方式。这里，我们着重于有效的监控生产过程中的微服务，我们将为这一新的软件开发模式制定5条原则来调整你的监控方法。

监控是微服务控制系统的关键部分，你的软件越复杂，那么你就越难了解其性能并解决问题。鉴于微服务给软件部署带来的巨大改变，监控系统同样需要进行彻底的改造。文章接下来介绍监控微服务的5条原则，如下：

1. 监控容器和里面的东西
2. 在服务性能上做监控，而不是容器
3. 监控弹性和多变的服务
4. 监控开发接口
5. 将您的监控映射到您的组织结构

利用这5条原则，你可以建立更有效的对微服务的监控。这些原则，可以让你定位微服务的技术变化和组织变化。

### 微服务监控的原则

#### 1.监控容器和里面的东西

容器是微服务重要的积木，容器的速度、可移植性和隔离特性让开发者很方便的建立微服务的模型。容器的好处已经写的够多了，在这里我们不再重复。

容器对于其他的系统来说就像是黑盒子，它的高度的可移植性，对于开发来说简直大有裨益，从开发到生产，甚至从一台笔记本开发直到云端。但是运行起来后，监控和解决服务问题，这个黑盒子让常规的方法失效了，我们会想：容器里到底在运行着什么？这些程序和代码是怎么运行的？它有什么重要的输出指标吗？在开发者的视角，你需要对容器有更深的了解而不是知道一些容器的存在。

![](http://thenewstack.io/wp-content/uploads/2016/09/greatfordev.jpg)

非容器环境的典型特征，一个代理程序运行在一台主机或者虚机的用户空间，但是容器里不一样。容器的有点是小，讲各种进程分离开来，尽可能的减少依赖关系。

在规模上看，成千上万的监测代理，对即使是一个中等大小的部署都是一个昂贵的资源浪费和业务流程的噩梦。对于容器有两个潜在的解决方案：1）要求你的开发人员直接提交他们的代码，或者2）利用一个通用的内核级的检测方法来查看主机上的所有应用程序和容器活动。我们不会在这里深入，但每一种方法都有优点和缺点。

#### 2. 利用业务流程系统提醒服务性能

理解容器中数据的运行方式并不容易，一个容器的度量值比组成函数或服务的所有容器的聚合信息都要低得多。

这特别适用于应用程序级别的信息，就像哪个请求拥有最短响应时间或者哪个URLs有最多的错误，同样也适用于基础设施水平监测，比如哪个服务的容器使用CPU资源超过了事先分配的资源数。

越来越多的软件部署需要一个业务流程系统，将逻辑化的应用程序转化到一个物理的容器中。
常见的转化系统包括Kubernetes、Mesosphere DC/OS和Docker Swarm。团队用一个业务流程系统来定义微服务和理解部署每个服务的当前状态。容器是短暂的，只有满足你的服务需求才会存在。

DevOps团队应该尽可能将重点放到如何更好的监控服务的运行特点上，如果应用受到了影响，这些告警点要放在第一道评估线上。但是能观察到这些告警点也并不容易，除非你的监控系统是容器本地的。

容器原生解决方案利用业务流程元数据来动态聚合容器和应用程序数据，并计算每个服务基础上的监控度量。根据您的业务流程工具，您可能有不同层次的层次结构想检测。比如，在Kubernetes里，你通常有Namespace、ReplicaSets、Pods和一些其他容器。聚集在这些不同的层有助于故障排除，这与构成服务的容器的物理部署无关。

![](http://thenewstack.io/wp-content/uploads/2016/09/servicemonitoring.jpg)

#### 3. 监控弹性和多变的服务

弹性服务不是一个新概念，但是它在本地容器中的变化速度比在虚拟环境中快的多。迅速的变化会严重影响检测系统的正常运行。

经常监测系统所需的手动调整指标和单独部署的软件，这种调整可以是具体的，如定义要捕获的单个指标，或收集应用程序在一个特定的容器中操作的配置数据。小规模上我们可以接受，但是数以万计规模的容器就不行了。微服务的集中监控必须能够自由的监控弹性服务的增长和缩减，而且无人工干预。

比如，开发团队必须手动定义容器包含那个服务做监控使用，他们毫无疑问会把球抛给Kubernetes或者Mesos定期的创建新的容器。同样，如果开发团队需要配置一个自定义的状态点从新代码的产生到付诸生产，那么基础镜像从容器中注册会给开发者带来更多的挑战。

在生产中，建立一个复杂的跨越多个数据中心或多个云部署的监控，会使你的服务跨越你的死人数据中心，具体的应用，比如亚马逊的AWS CloudWatch。通过动态的本地容器环境，这个实时监控系统，会监控不同区域的数据中心。

#### 4.监控开发接口

在微服务环境中，API接口是通用的。它们是一个服务的必备组件，实际上，API的响应和一致性是服务的内部语言，虽然暂时还没人定义它们。

因此，API接口的监控也是必需的。API监控可以有不同的形式，但是它绝对不是简单的上下检查。例如，了解最常使用的点作为时间函数是有价值的。这使得团队可以看到，服务使用的变化，无论是由于设计变更或用户的改变。

你也可以记录服务最缓慢的点，这些可以揭示重大的问题，至少，指向需要在系统中做优化的区域。

最终，跟踪系统服务响应会成为一个很重要的能力，它会帮助开发者了解最终用户体验，同时将信息分成基础设施和应用程序环境两大部分。

#### 5. 将您的监控映射到您的组织结构

这篇文章着重在微服务和监控上，像其他科技文章一样，这是因为很多人都关注软件层面。

对于那些熟悉康威定律的人来说，系统的设计是基于开发团队的组织结构。创造更快，更敏捷的软件的迫力，推动团队思考重新调整他们的组织结构和管理它的规则。

![](http://thenewstack.io/wp-content/uploads/2016/09/mapmonitoring.jpg)

如果他们想从新的软件架构比如微服务上获益，那么他们需要更小的更松散更耦合的团队，可以选择自己的方向只要能够满足整个需求即可。在一个团队中，对于什么开发语言的使用，bug的提交甚至工作职责都会有更大的控制能力。

开发团队可以启用一个监控平台：让每一个微服务团队可以定位自己的警报，指标，和控制面板，同时也要给全局系统的操作一个图表。

### 总结

快捷让微服务流行起来。开发组织要想为客户提供更快的更多的功能，然后微服务技术就来了，架构转向微服务并且容器的流行让快捷开发成为可能，所有相关的进程理所当然的搭上了这辆火车。

最后，基本的监控原则需要适应加入到微服务的技术和结构。越早认识到这种转变的开发团队，能更早更容易的适应微服务这一新的架构。

--------------------------------------------------------------------------------

via: http://linoxide.com/firewall/pfsense-setup-basic-configuration/

作者：[Apurva Dave][a] [Loris Degioanni][b]
译者：[jiajia9linuxer](https://github.com/jiajia9linuxer)
校对：[校对者ID](https://github.com/校对者ID)

本文由 [LCTT](https://github.com/LCTT/TranslateProject) 原创编译，[Linux中国](https://linux.cn/) 荣誉推出

[a]: http://thenewstack.io/author/apurvadave/
[b]: http://thenewstack.io/author/lorisdegioanni/