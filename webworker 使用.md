

- 1. webwork 仅仅只能用于纯粹的计算, 必须是那种剥离项目逻辑的计算,如果跟项目逻辑关系太紧密,则不适合使用, 而且不能直接用来导入npm 包,使用起来不方便.
#### [webworker import 第三方 参考1](https://blog.csdn.net/qq_33040483/article/details/109574777)
#### [webworker import 第三方 参考2](https://juejin.cn/post/6844903935908675598)

- 2. Dedicated Worker, Service Worker, Shared Worker
- 3. service worker [http请求也可以缓存](https://www.jianshu.com/p/0121d1793d01) 不过,这个是需要把缓存的的请求先请求一遍才行, 最后才会变快, 甚至离线访问.
