
### 1. 直接用window.open 和 window.opener.postMessage 

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
