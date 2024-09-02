# toGooood说明
## 关于某个著名的白p小破站代码失效的说明
- 大家如果发现网上一堆的白p教程，来源是xx小破站的，上传以后反代失败的，主要原因是p的太厉害小破站被人开he了。
- 主要小破站哪个家伙跑路了，然后被人悬赏追追追，另外他分享的代码不是fock开源作者的，是down下来后自己再上传所以有些地方就没有维护和更新。
+ 然后运营商修改了 主要的几个服务的网址
比如doh服务，dos服务的主要入口地址，所以就永远的是失败的
+ 所以修改成正确的doh就正常了，或者自己部署doh服务
+ 就是toGoPP这个组件的由来，在cf上部署一个纯净的属于自己的doH-doS-https服务，推荐自建，感谢原作者的开源。
+ Tree
├─toGoPP/(doH-doS-https服务) └─toGoVV/(vless + tls + clash 节点)

###  toGoVV：vless + tls + ws + sb + clash节点
worke部署选择git或者update，即可运行 本地拉取后，先输入 npm install 安装组件 然后在 npm run bud 编译重新上传worker即可

###  toGoHH：doH-doS-dns-https服务，基于浏览器的纯净dns服务
worke部署选择git或者update，即可运行 本地拉取后，先输入 npm install 安装组件 然后在 npm run bud 编译重新上传worker即可

###  toGoPP：Google的反代，能搜索，能查询，被墙的还需要梯子
worke部署选择git或者update，即可运行 本地拉取后，先输入 npm install 安装组件 然后在 npm run bud 编译重新上传worker即可
### 如何建立自己的高可用反代服务
git 代码以后，在自己所配置cf worker点设置，点使用变量，先将关键变量发布到cf中，并配置加密模式。

#### 1、首先建立doH-doS-dns-https服务

- 将 toGoHH 的代码先上传在一个 cf-worker下进行部署，然后
修改代码中的这个部分，如下：
```js
const doh = "https://security.cloudflare-dns.com/dns-query";
const dohjson = "https://security.cloudflare-dns.com/dns-query";
```
或者其他地址。

- 绑定域名及路由到toGoHH对应的cf-worker上，等待可以访问，正常访问返回403、404错误是正常的。

#### 2、建立ws反代通路
- 将 toGoVV 的代码先下载到本地
- src目录下有三个脚本文件，分别是纯净ws-反代，纯净tls-反代，和vless + tls + ws + sb + clash多合一反代，
- 以上代码来源不同的开源作者，我只是集合在一起了
- 根据自己的需要修改全局变量或者在脚本文件中修改关键的变量
- 使用wrangler deploy命令进行上传
- 比如要上传多合一脚本命令是
```js
 wrangler dev src/worker-vless-tls-base64-clash-sb.js
```

+ 给小白的话，这些命令都在IDE中使用，比如vscode，我们默认你是会的，如果不知道怎么用就当我没说
+ 给小白的话，有些脚本本地调试失效，不一定是代码问题，可能你没有“pnpm install” 依赖
+ 而pnpm install依赖下载超时报错，有可能你没换源。

#### 3、保护自身服务纯净性
- 在自己所配置cf worker点设置，点使用变量，先将关键变量发布到cf中，并配置加密模式。
- 只有先配置了cf-worker的全局变量，然后wrangler.toml中才能设置全局变量值，不然上传调试必须报错。

#### 4、奇怪的错误
- js的代码有时格式问题，会有奇怪错误，所以上传前先用
```
prettier --write 'src/*.{js,css,json,md}'
```
格式化你的代码再上传，如果不能格式化，先查查是不是按照了这个prettier 组件

#### 5、https://github.com/aspnmy/toGooood.git
