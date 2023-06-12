
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
    window.frames[0].postMessage('hello, world', '*');
</script>

<body>
    <iframe src="http://127.0.0.1:3000/"  />
</body>
</html>
```

### iframe 内嵌页面
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

    window.addEventListener('message', (e) => {
        alert('111')
    })
</script>

<body>
    I am a page in iframe
</body>


</html>
```
