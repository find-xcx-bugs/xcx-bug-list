# xcx-bugs-list（微信小程序踩坑集合）

## 这个仓库的意义在于？
帮助开发小程序的前端工程师们避免再次进坑.

本周（2017.11.24）因为我们的小程序在线上出现了一例case,用户通过普通二维码调起小程序后传参错误，
起初我们自己排查日志后难以定位问题，找到微信侧从日志查询告知没有问题。后来同摩拜的前端小伙伴  [binnng](https://github.com/binnng) 
咨询，发现他们也存在相同的问题，跨业务间存在相同的问题可能是微信的问题，因而push了微信协助解决。
所以，建立这个组织和仓库的意义更多是希望促进跨工程间相互沟通，也希望帮助后来的人走更少的路吧。


## 参与共建这个仓库的人都有哪些？
目前主要由[我](https://github.com/chenyaoswu)在维护，因为刚入坑，暂时没有太多的可贡献案例。欢迎大家有空也能一起贡献。

## 如何贡献
提pr即可。



# buglist集合：

[1.小程序扫普通二维码调起小程序 码地址传为历史地址](./docs/1-qrcode-history.md) —— Author: [陈小二](https://github.com/chenyaoswu)

[2.小程序内多重调用原生promise，无返回，无报错，代码卡住](./docs/2-multiple-promise-block.md) —— Author: [蒋欢](https://github.com/Dragon-Rider)

[3.小程序页面pv统计数过高，导致页面转化率低](./docs/3-pv-error.md) —— Author: [陈小二](https://github.com/chenyaoswu)

4.小程序分包加载，待补充

[5.vConsole 将已清除掉的log记录再次打印出来，造成代码没有生效或者微信扫码错误的错觉](./docs/5-vConsole.md) —— Author: [蒋欢](https://github.com/Dragon-Rider)
