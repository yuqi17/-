
2023 年的时候 vite 已经出现了, 之前还有的rollup, 大厂自己的前端打包工具之类的.不过webpack 还是主流, 下面总结一些常见的坑:

1. npm i xxx --legacy-peer-deps [参考](https://juejin.cn/post/6971268824288985118) 这个参数peer 是同辈的意思, peerDependencies 是为了防止多个包有共同依赖的时候安装多次, 不过有时候多个包依赖的同一个包的版本不同会有问题, 这个参数就是为了让它们各自安装对应的版本的包

   
