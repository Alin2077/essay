## 临时实例和持久实例
* 临时实例只会注册到内存中；持久实例不仅注册到内存中，还会持久化到磁盘。
* 临时实例的健康检查机制是Client模式，即Client主动向Server上报其健康状态。默认心跳间隔为5秒，在15秒内Server未收到Client心跳，就会将其标记为“不健康”，若30秒内收到心跳，则恢复为“健康”状态，否则从内存中清除。
* 持久实例的健康检查机制是Server模式。即Server主动去检测Client的健康状态。默认每20秒检测一次。失败后会被标记成“不健康”，但永远不会清除。
* 设置持久实例的方法：spring.cloud.nacos.discovery.ephemeral = false。注意，已经注册成为过临时实例的应用将不能再被注册为持久实例。
## 数据存储
nacos默认将数据存储在内置的数据库中，0.7版本之后新增了外置数据库的支持，目前仅支持mysql。
# CAP模式
* 默认情况下，nacos discovery集群的数据一致性采用的是AP模式。
* 也支持CP模式，需要进行转化，通过提交PUT请求完成转换。
    > http://localhost:8848/nacos/v1/ns/operator/switches?entry=serverMode&value=CP