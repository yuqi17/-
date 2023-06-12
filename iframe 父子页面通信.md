
### 跨域的情况下, 下面的代码是无法访问得到结果的, 即便设置了服务器的跨域也没用; postmessage, document.domain = '共同主域' 
```
var doc = document.getElementById("myFrame").contentDocument || document.getElementById("myFrame").contentWindow.document;
```


### 父页面 http://127.0.0.1:8080/
```html

<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>

<script>
    window.frames[0].postMessage('hello, world', '*');// * 这个参数必须设置不然发不出去; 设置有两个值: *  和  ```http://127.0.0.1:3000``` 必须把协议IP端口都写清楚 可以保证发送成功
</script>

<body>
    <iframe src="http://127.0.0.1:3000/"  />
</body>
</html>
```

### iframe 内嵌页面 http://127.0.0.1:3000
```html

<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<script>
    function test(e) {
        console.log(e.target.contentDocument || e.target.contentWindow.document)
    }

    window.addEventListener('message', (e) => {// 可以在这个地方过滤一下, 不是所有的容器页面都可以发信息过来
       console.log(e)// isTrusted: true, data: 'hi', origin: 'http://127.0.0.1:8080', lastEventId: '', source: Window, // 这个打印也只有在容器页面可以打印, 如果单独打开容器里面的页面是不会打印的
    })
</script>

<body>
    I am a page in iframe
</body>
</html>
```

#### iframe 高度自适应不出现滚动条(下面的子页面的两个按钮可以完全去掉, ResizeObserver 可以完全自动的发送高度给父页面)
##### 父页面
```html
    <!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<script>
   function load(){
      window.frames[0].postMessage('hello, world', "*");
   }
   
	window.addEventListener('message', (e)=>{
		document.getElementById('iframe').style.height = `${e.data}px`
	});
</script>

<body>
    <iframe id='iframe' src="http://127.0.0.1:3000/" onload="load()" />
</body>
</html>
```


##### 子页面
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #test {
            height: 600px;
        }
    </style>
</head>
<script>
    function send(e) {
        // window.top.postMessage(document.documentElement.scrollHeight, "*")
        window.parent.postMessage(document.documentElement.scrollHeight, "*")
    }

    function change() {
        document.getElementById('test').style.height = '700px'
    }

    window.addEventListener('message', (e) => {
        console.log(e, '<<<====')
    })


    function onload() {
        // 创建观察者对象
        var observer = new ResizeObserver(function (entries) {
            entries.forEach(function (entry) {
                window.parent.postMessage(document.documentElement.scrollHeight, "*")
                console.log(entry.contentRect.height, '*****')
            });
        });
        // 观察指定的 DOM 元素
        var target = document.getElementById('test');
        observer.observe(document.documentElement);
    }

</script>

<body onload="onload()">
    <div id="test">
        <button onclick="send()">send message to container page</button>
        <button onclick="change()">高度变成 700px</button>
    </div>
</body>


</html>
```

####  总结
所以postMessage 通信的必要条件是: 通信对象之间必须存在 引用的关系, 比如 window 可以索引到 iframe, 子窗口. 
1. 容器向iframe 传递消息 window.iframes[0] 或者其它办法只要能得到 iframe 的引用就可以给iframe 发消息, 注意要等iframe 完全加载好再用, 否则会空指针
2. iframe 中的页面向容器发消息  window.top.postMessage(document.documentElement.scrollHeight, "*")    或者  window.parent.postMessage(document.documentElement.scrollHeight, "*") 
3. 监听message 可以 通过 e.origin 过滤其它的域名, e.data 获得传递的数据, 数据可以是任意的js类型
4. 容器 还是 iframe 直接用window.addEventListener('message',xxx)
#### iframe 自适应核心代码
```js
	// iframe 页面
        var observer = new ResizeObserver(function (entries) {
            entries.forEach(function (entry) {
                window.parent.postMessage(document.documentElement.scrollHeight, "*")
            });
        });
        observer.observe(document.documentElement);
	
	
	window.addEventListener('message', (e)=>{
		document.getElementById('iframe').style.height = `${e.data}px`
	});

```

