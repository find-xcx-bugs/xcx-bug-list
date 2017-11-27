# 小程序页面pv统计数过高，导致页面转化率低

### 作者：[陈小二](https://github.com/chenyaoswu)

### 问题： 小程序使用微信支付的单页面pv数偏高，致页面转化率低

对于业务开发者来说，业务数据和数据监控是不可缺失的。

图例是我们小程序扫码付业务在数据体系搭建过程中的其中一步：技术流程拆解。


![技术流程拆解](https://github.com/find-xcx-bugs/xcx-bugs-list/blob/master/images/3-qrcode.png)


在数据选型上，我同时使用了微信自定义数据统计和公司内部第三方数据统计，并将之与微信主动上报的数据分析进行对比，  
来确保数据准确性。

    微信自定义数据统计和公司内部第三方数据统计方法：
    ![第三方数据统计代码](https://github.com/find-xcx-bugs/xcx-bugs-list/blob/master/images/3-onshow-report.png)

    #### 微信主动上报数据查询参见MP后台 微信实时统计:
    ![微信实时统计](https://github.com/find-xcx-bugs/xcx-bugs-list/blob/master/images/3-mp-data.png)


在数据的收集过程中，我发现支付按钮点击率（点击支付次数/页面展示次数）仅有50%+。

对比我们内部相同的H5服务，转化率过低，远远不符合我们对业务预期效果。

核查3种数据分析，我发现页面展示次数过高，并且三种方法的页面展示次数有较大差异，其中：

        微信自定义数据统计pv(页面展示次数) 约等于 公司内部第三方数据统计pv（页面展示次数）
        微信实时统计pv(页面展示次数) <  自定义数据统计 （包括微信自定义和公司内部第三方字数据统计）

微信实时统计pv的统计方法不得而知，而另外两种方法均是在onshow事件中触发。



### 原因：
排查过程中，发现页面在涉及到支付时，微信调起弹窗，会再次触发onshow事件，从而导致pv数重复发送。

对于微信来说，支付完以后会触发支付完成页，如图所示：

![微信支付完成页](https://github.com/find-xcx-bugs/xcx-bugs-list/blob/master/images/3-wechat-success.jpg)

点击完成后再次回到页面会继续触发onshow事件。

### 解决方案：
从技术上来说，onshow事件本应设计如此。页面再次展示应该触发onshow。

从业务上来说，onshow事件是应该用来做pv统计的。但因为涉及到类似支付的事情，业务方需要自己控制pv发送时机。

目前我的解决方案：onload中统计。

![第三方数据统计代码](https://github.com/find-xcx-bugs/xcx-bugs-list/blob/master/images/3-onload-report.png)




