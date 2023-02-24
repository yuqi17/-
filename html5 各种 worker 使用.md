

- 1. webwork 仅仅只能用于纯粹的计算, 必须是那种剥离项目逻辑的计算,如果跟项目逻辑关系太紧密,则不适合使用, 而且不能直接用来导入npm 包,使用起来不方便.
#### [webworker import 第三方 参考1](https://blog.csdn.net/qq_33040483/article/details/109574777)
#### [webworker import 第三方 参考2](https://juejin.cn/post/6844903935908675598)

- 2. Service Worker, Dedicated Worker,  Shared Worker 三者的区别: service 是客户端和服务端的代理, decicated 和 shared 在于是否可以多脚本共享数据
  
  ```
  
  There are mainly 3 types of workers :
  Dedicated Worker: accessible to a single script. 
  Shared Worker: can be accessed by multiple scripts. Service Worker: serves as a  proxy between client and server
  
  A shared worker can work with multiple connections. It posts messages to ports to allow communication between various scripts.
  A dedicated worker on the other hand is `simply tied to its main connection and cannot post messages to other scripts (workers).
  ```
  
### [create-react-app 中 registerServiceWorker.js 的使用](https://blog.csdn.net/u010565037/article/details/102916848)
[PWA 图标等相关的manifest.json配置](https://blog.csdn.net/zemprogram/article/details/102989404)

- 3. 缓存不同于存储, 缓存一定是先要请求一遍才行, 而存储则可以利用请求的多线程偷偷的进行存储.

- 4. [关于浏览器缓存的位置,强缓存和协商缓存](https://cloud.tencent.com/developer/article/1523550) 可以通过随机数的方式来去除对应的缓存
- 5. manifest.json 也是一种静态缓存的方法, 不过很少用到 application cache (往返缓存), 离线应用
- 6. 缓存空间: PWA 机制的一种应用, 下面是一个例子:

```js

  

function test1() {
    self.addEventListener("install", (event) => {
        event.waitUntil(
            caches
                .open("v1")
                .then((cache) =>
                    cache.addAll([
                        "/",
                        "/index.html",
                        "/style.css",
                        "/app.js",
                        "/image-list.js",
                        "/star-wars-logo.jpg",
                        "/gallery/bountyHunters.jpg",
                        "/gallery/myLittleVader.jpg",
                        "/gallery/snowTroopers.jpg",
                    ])
                )
        );
    });

    self.addEventListener("fetch", (event) => {
        event.respondWith(
            caches.match(event.request).then((response) => {
                // caches.match() always resolves
                // but in case of success response will have value
                if (response !== undefined) {
                    return response;
                } else {
                    return fetch(event.request)
                        .then((response) => {
                            // response may be used only once
                            // we need to save clone to put one copy in cache
                            // and serve second one
                            let responseClone = response.clone();

                            caches.open("v1").then((cache) => {
                                cache.put(event.request, responseClone);
                            });
                            return response;
                        })
                        .catch(() => caches.match("/gallery/myLittleVader.jpg"));
                }
            })
        );
    });

}


async function test2() {
    // Try to get data from the cache, but fall back to fetching it live.
    async function getData() {
        const cacheVersion = 1;
        const cacheName = `myapp-${cacheVersion}`;
        const url = "https://jsonplaceholder.typicode.com/todos/1";
        let cachedData = await getCachedData(cacheName, url);

        if (cachedData) {
            console.log("Retrieved cached data");
            return cachedData;
        }

        console.log("Fetching fresh data");

        const cacheStorage = await caches.open(cacheName);
        await cacheStorage.add(url);
        cachedData = await getCachedData(cacheName, url);
        await deleteOldCaches(cacheName);

        return cachedData;
    }

    // Get data from the cache.
    async function getCachedData(cacheName, url) {
        const cacheStorage = await caches.open(cacheName);
        const cachedResponse = await cacheStorage.match(url);

        if (!cachedResponse || !cachedResponse.ok) {
            return false;
        }

        return await cachedResponse.json();
    }

    // Delete any old caches to respect user's disk space.
    async function deleteOldCaches(currentCache) {
        const keys = await caches.keys();

        for (const key of keys) {
            const isOurCache = key.startsWith("myapp-");
            if (currentCache === key || !isOurCache) {
                continue;
            }
            caches.delete(key);
        }
    }

    try {
        const data = await getData();
        console.log({ data });
    } catch (error) {
        console.error({ error });
    }

}
```

### WEBSQL 支持的浏览器不多,适合客户端大量数据的存储,慎用
```js
    var db = openDatabase(' mydatabase ', '1.0', 'Test DB', 2 * 1024 * 1024); 

   db.transaction(function (tx) { 
      tx.executeSql('CREATE TABLE IF NOT EXISTS t1 (id unique, log)');  
      tx.executeSql('INSERT INTO t1 (id, log) VALUES (1, "foobar")');  
      tx.executeSql('INSERT INTO t1 (id, log) VALUES (2, "logmsg")');  
   });
```
