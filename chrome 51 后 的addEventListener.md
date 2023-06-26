
#### addEventListener 的三个参数: 默认 capture:false once:fase passive:true 
##### 1. capture 如果为false 默认相当于 第二个参数为false 或者不加, 如下,如果capture:true, 则标识捕获阶段就开始触发监听,既点击了div,会先触发父节点的监听器, 反之是先触发子元素的,然后冒泡到父元素
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="div" style="width:100%;height:2000px;background:lavender"></div>
    <script src="https://cdn.staticfile.org/jquery/1.10.2/jquery.min.js"></script>
    <script>
        document.addEventListener('click', function (event) {
            console.log("document被点击啦！")
        }, { capture: false })
        document.getElementById("div").addEventListener("click", function () {
            console.log("div被点击啦！")
        }, false)
    </script>
</body>
</html>
```

##### 2. once:true 这个比较好理解就是触发一次之后就失效

##### 3. passive:true 用来优化手机端的滚动 告诉浏览器不调用 preventDefault 函数来阻止事件事件行为, 因为执行默认行为需要时间, 这样就可以避免白等的时间而产生的卡顿
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="div" style="width:100%;height:2000px;background:lavender"></div>
    <script src="https://cdn.staticfile.org/jquery/1.10.2/jquery.min.js"></script>
    <script>
        let event = new Event("foo", {// 所谓可以阻止,比如点击a标签的默认行为是跳转,可以阻止标识调用preventDefault()会阻止跳转
            cancelable: true
        })

        document.addEventListener("foo", function (event) { // 在 document 上绑定 foo 事件的监听函数
            console.log(event.defaultPrevented) // false
            event.preventDefault()
            console.log(event.defaultPrevented) // 还是 false，preventDefault() 无效
        }, { passive: true }); // passive 是被动的, 用来阻止默认行为的

        document.dispatchEvent(event) // 派发自定义事件

        window.addEventListener('wheel', console.log, { passive: true })
        document.addEventListener('touchstart', console.log, { passive: true });

    </script>
</body>

</html>
```
