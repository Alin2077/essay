## 响应式编程
* Reactive Programming，是一种新的编程范式、编程思想。
* 最早由.Net平台上的Reactive eXtensions(Rx)库来实现，后来被迁移到java平台，产生了著名的Rxjava，后来又产生了Reactive Streams规范。
## Reactive Streams
* 响应式编程的规范，定义了响应式编程的相关接口；只要符合该规范的开发，就成为Reactive响应式编程库。
## Rxjava2
* 是一个响应式编程库。产生于Reactive Streams规范之后。但由于其是在Rxjava基础以上进行开发，所以在设计时不仅遵循了Reactive Streams规范，同时为了兼容Rxjava，使得Rxjava2使用非常不方便。
## Reactor
* 是一种全新的响应式编程库，完全遵循Reactive Streams规范，又与Rxjava没有任何关系，使用起来方便。