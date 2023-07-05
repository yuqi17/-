
偶然发现了水印的组件是生成一个 shadow dom ,这个dom 不会影响普通dom
Shadow DOM和Light DOM是两个相互独立的DOM树，它们之间的元素和样式是相互隔离的。Shadow DOM允许将隐藏的DOM树附加到常规的DOM树中，从而实现了组件化和隔离的效果
这里是它的生成方法:
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="myDiv"></div>

    <script>
        const div = document.getElementById('myDiv');
        const shadowRoot = div.attachShadow({ mode: 'open' });

        // 在shadow root中添加内容
        shadowRoot.innerHTML = `
        <style>
          /* 在这里添加样式 */
        </style>
        <p>这是在shadow root中的内容</p>
      `;
    </script>
</body>

</html>
```
