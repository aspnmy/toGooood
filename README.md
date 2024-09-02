# toGooood说明
# 关于某个著名的白p小破站代码失效的说明

+ 大家如果看过 小破站的代码 发现网上一堆的教程，没办法部署成功，主要原因是p的太厉害被人开he了。
+ 然后运营商修改了 主要的几个服务的网址
+ 比如doh服务，dos服务的主要入口地址，所以就永远的是失败的

- 所以修改成正确的doh就正常了，或者自己部署doh服务
- 就是toGoPP这个组件的由来，在cf上部署一个纯净的属于自己的doH-doS-https服务，推荐自建，感谢原作者的开源。



## Tree
├─toGoPP/(doH-doS-https服务)
└─toGoVV/(vless + tls + clash 节点)


## toGoVV：vless + tls + ws + sb + clash节点

worke部署选择git或者update，即可运行
本地拉取后，先输入 npm install 安装组件
然后在 npm run bud 编译重新上传worker即可

## toGoPP：doH-doS-dns-https服务，基于浏览器的纯净dns服务

worke部署选择git或者update，即可运行
本地拉取后，先输入 npm install 安装组件
然后在 npm run bud 编译重新上传worker即可

## 更新源 https://github.com/aspnmy/toGooood.git

