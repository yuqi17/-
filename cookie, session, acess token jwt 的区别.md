
### [参考1](https://zhuanlan.zhihu.com/p/110480687)
可以知道: ```允许一个子域可以设置或获取其父域的 Cookie```, 所以像网易这样的门户网站,登陆一次就可以在别的网易门户直接作为登陆用户了, 应该是这个原理;
而OAuth 则是解决不同域之间如何共享资源的办法, 比如使用github 登陆网站就是OAuth, 还提到了LDAP 这种协议可以用户电脑登录后, 所有绑定的网站就自动登陆,
我所知道的是使用windows系统 + 内部系统的公司很喜欢这么干. 使用httponly 设置, 比如是http 请求到的cookie才能访问, 缓解了xss 跨站脚本攻击.

## [参考2](https://juejin.cn/post/7077540836229152775) 
这里主要详细讲解了:cookie, jwt, session; 新的东西是jwt 这个凭证是一直存在客户端的, 服务器端并没有其他的对应凭证存储,比如session_id. 还有一个 refresh token 是为了
防止刷新的时候要重新登陆获得 acess token 设置的.

## [参考3](https://juejin.cn/post/6844903938953576456)
token 是需要查询数据库来验证的, 而JWT 则是直接在服务器验证就可以

OAuth 以qq 登陆 豆瓣为例:
![image](https://user-images.githubusercontent.com/10356819/222033254-bac659ce-bebe-4ece-b009-9ad22a5c3113.png)


### OAuth 和 JWT 的区别
```
oauth2有client和scope的概念，jwt没有。如果只是拿来用于颁布token的话，二者没区别。 常用的 bearer(送信人)算法   oauth、jwt都可以用
```
