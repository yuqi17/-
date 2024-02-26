### 1. 制作iconfont 
去网站[https://www.iconfont.cn/manage](https://www.iconfont.cn/manage) 上传  svg文件, 制作iconfont 下载即可

### 2. 编写代码, icontfont.js 对显示不是必须的; 直接可以修改color 来修改文字颜色
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8"/>
  <title>iconfont Demo</title>
  <link rel="stylesheet" href="iconfont.css">
  <!-- <script src="iconfont.js"></script> -->
  <style>

    .iconfont{
      color: red;
    }
  </style>
</head>
<body>
  <span class="icon iconfont icon-clear"></span>
</body>
</html>

```

### 3. iconfont 网站上也有 Lottie动效图标库, 可以去下载json 文件
[使用参考](https://blog.csdn.net/weixin_44000173/article/details/127171147), 安装库: lottie-web, 然后设置一下html元素作为容器, 再设置一下json路径和其它参数即可
