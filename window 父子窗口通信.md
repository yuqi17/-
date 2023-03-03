
### 1. localStorage 和 其监听器; indexdb 也是相同原理;

### 2. 直接用window.open 和 window.opener.postMessage 

主窗口:
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>index</title>
</head>

<body>
    index:
    <button onclick="func()">open test page</button>
    <script>
        function func() {
            const w = window.open('/test.html', '_blank');
            window.addEventListener('message', e => console.log(e));// 这里w 和 window 是同一个对象
        }
    </script>
</body>

</html>
```

子窗口:

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>test</title>
</head>

<body>
    test
    <button onclick="test()">send a message to page index</button>
</body>
<script>
    function test() {
        console.log('test...')
        window.opener.postMessage({ msg: 'hahah' });// 用opener 就不会向子窗口本身发送消息
    }

    window.addEventListener('message', e => {
        alert(e);
    })
</script>

</html>
```

### 3.  BroadcastChannel
[参考](https://juejin.cn/post/6844903811228663815) 比window.postMessage 好的一点是可以在多个同源窗口之间广播.要注意使用的是同一个对象.
```js
// A.html
const channel = new BroadcastChannel('tabs')
channel.onmessage = evt => {
// evt.data
}

// B.html
const channel = new BroadcastChannel('tabs')
channel.postMessage('hello')
```

### 4.  SharedWorker 不是很常用
[各种跨页通信的比较](https://zhuanlan.zhihu.com/p/29368435)
