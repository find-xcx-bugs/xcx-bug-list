# vConsole 将已清除掉的log记录再次打印出来，造成代码没有生效或者微信扫码错误的错觉

## 作者: [蒋欢](https://github.com/Dragon-Rider)

> 这是一个开发工具 `vConole` 带来的问题。虽然不大，但是如果你早已习惯 chrome 开发面板的使用方法，则很容易在开发中导致误解。

### 问题：vConsole 打开后点击 clear 清除log，再次操作小程序。发现会将之前清除掉的log再次打印出来，然后才打印新的log，造成代码没有生效的错觉。

1、首先，解释下什么是 `vConole` ？     
`vConsole` 是腾讯开发的一个轻量、可拓展、针对手机网页的前端开发者调试面板， 具体介绍见请：[vConsole官方仓库][1]。

2、小程序里的 `vConole` 工具   
微信小程序在开发过程中也可以使用 `vConole` 辅助在手机端进行调试，具体方法是：点击开发版小程序又上角 `...` ，之后选择 `打开调试` ，如下图所示。

<div align="center">
    <img width="50%" src="https://github.com/find-xcx-bugs/xcx-bug-list/blob/master/images/4-vConsole-1.jpeg"/>
    <p style="color: grey">图1 vConsole使用介绍</p>
</div>

3、在使用小程序开发工具中，由于 log 记录过多，我们在一次调试过程中可能会使用 `clear` 来清除log，事实上 `clear` 没有像 chrome 的 “clear console” 一样，做到真正的清除 log。而是将 log 清除后缓存了起来。待你下次刷新页面时会将两次 log 一起打印出来。我们在调试 “[小程序扫码bug][2]” 时就遇到了该问题。

####举例：

a、我们调试时，会在 onload 内将该函数参数打出，读取微信扫码的数据。
````
    onLoad(this: IndexPage, p) {  
        console.log('打印p参数打印p参数打印p参数打印p参数打印p参数打印p参数');  
        console.log(p);  
    }
````
b、当我们第一次扫码调试时，针对商户 “巴蜀传香” 打出的log结果如图所示，之后我们**点击 clear 清除了调试工具的 log 记录**并退出。

<div align="center">
    <img width="50%" src="https://github.com/find-xcx-bugs/xcx-bug-list/blob/master/images/4-vConsole-2.jpeg"/>
    <p style="color: grey">图2 第一次扫描二维码得到的结果</p>
</div>

c、当我们第二次扫不同的二维码进入小程序时，预期onload的参数会变化。然而发现店铺变了，但扫描的结果没有改变（实际上二维码变了，店铺与log也应该会改变）。

<div align="center">
    <img width="50%" src="https://github.com/find-xcx-bugs/xcx-bug-list/blob/master/images/4-vConsole-3.jpeg"/>
    <p style="color: grey">图3 第二次扫描二维码得到的上次缓存结果</p>
</div>

d、事实上，当你将 log 记录继续往下滑会发现，新的 log 记录也已打印出来。**说明即使你之前点击了 clear ，新的 log 也会因为缓存再次打印出来。**

<div align="center">
    <img width="50%" src="https://github.com/find-xcx-bugs/xcx-bug-list/blob/master/images/4-vConsole-4.jpeg"/>
    <p style="color: grey">图4 第二次扫描二维码得到的实际结果</p>
</div>

### 环境：
IOS 和 安卓 均可稳定复现。

### 原因：
vConsole 会将已经 “clear” 的缓存再次打印出来。    

[微信反馈](https://github.com/Tencent/vConsole/issues/131#issuecomment-350980424)：“这是小程序底层的一个问题，正在修复中，不是vConsole的问题哈。”

### 解决方案：
调试的时候需要多往后翻一下，找到各次对应的扫码 log 记录。

### 风险：
开发阶段，可能因为 log 判断错误，而造成误解。

[1]: https://github.com/Tencent/vConsole/blob/dev/README_CN.md
[2]: https://github.com/find-xcx-bugs/xcx-bug-list/blob/master/1-qrcode-history.md
