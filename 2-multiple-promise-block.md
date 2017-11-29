# 小程序内多重调用原生promise，无返回，无报错，代码卡住

## 作者: [JiangHuan](https://github.com/Dragon-Rider)

### 问题：
---
在部分IOS机型上，小程序内使用原生promise实现异步，在嵌套四层后，Promise的resolve和reject均无返回。

### 环境：
用户机型：iPhone 7  
系统版本：IOS 10.3.3  
微信版本：6.5.21  
`部分ios用户可以稳定复现。`  

### 原因：
微信侧表示IOS 10下小程序使用的是原生的promise，[页面由 WKWebView 来渲染的](https://mp.weixin.qq.com/debug/wxadoc/dev/devtools/details.html)。因此网页也会有同样的问题，但我们还未在H5下得到验证。  
之前微信曾修复过IOS 8 下类似[问题记录](https://mp.weixin.qq.com/debug/wxadoc/dev/devtools/uplog.html)。

### 解决方案：
换成第三方库[pinkie.js](https://github.com/floatdrop/pinkie/blob/master/index.js)，实现promise，用户问题得到解决。

### 风险：
目前还没有遇到任何兼容性问题上报，但pinkie里手动实现的promise比系统原生promise要慢一点。 如果进行异步操作并全局赋值时，要注意异步返回生效的时机。

