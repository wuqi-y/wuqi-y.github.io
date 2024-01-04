---
abbrlink: ''
aplayer: null
aside: null
categories:
- 分享转载
comments: null
cover: https://s11.ax1x.com/2023/12/27/pib7r9O.jpg
date: 2023/10/15
description: null
highlight_shrink: null
katex: null
keywords: null
mathjax: null
random: null
recommend: '100'
swiper: '80'
tags: []
title: 关于微信前端支付在微信环境如何支付
type: null
updated: 2023-12-27T18:9:49.259+8:0
---
### 关于微信前端支付在微信环境如何支付

我们都知道在微信环境中是无法直接使用 H5 支付的，需要调取微信浏览器一些相关 API 去唤醒支付,相关链接如下：

[https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=7_7&index=6](https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=7_7&index=6)

**注意：WeixinJSBridge 内置对象在其他浏览器中无效。**

```javascript
function onBridgeReady() {
  WeixinJSBridge.invoke(
    "getBrandWCPayRequest",
    {
      appId: "wx2421b1c4370ec43b", //公众号ID，由商户传入
      timeStamp: "1395712654", //时间戳，自1970年以来的秒数
      nonceStr: "e61463f8efa94090b1f366cccfbbb444", //随机串
      package: "prepay_id=u802345jgfjsdfgsdg888",
      signType: "MD5", //微信签名方式：
      paySign: "70EA570631E4BB79628FBCA90534C63FF7FADD89", //微信签名
    },
    function (res) {
      if (res.err_msg == "get_brand_wcpay_request:ok") {
        // 使用以上方式判断前端返回,微信团队郑重提示：
        //res.err_msg将在用户支付成功后返回ok，但并不保证它绝对可靠。
      }
    }
  );
}
if (typeof WeixinJSBridge == "undefined") {
  if (document.addEventListener) {
    document.addEventListener("WeixinJSBridgeReady", onBridgeReady, false);
  } else if (document.attachEvent) {
    document.attachEvent("WeixinJSBridgeReady", onBridgeReady);
    document.attachEvent("onWeixinJSBridgeReady", onBridgeReady);
  }
} else {
  onBridgeReady();
}
```

那后端支付的时候是需要用户的**appid**的那这时候我们在客户端应该如何获取呢？其实微信官方文档有很详细的解说：

[https://developers.weixin.qq.com/doc/offiaccount/OA_Web_Apps/Wechat_webpage_authorization.html](https://developers.weixin.qq.com/doc/offiaccount/OA_Web_Apps/Wechat_webpage_authorization.html)

我们是要走网页授权的方式只获取 appid 的话可以走无感授权，如果需要获取用户详细信息则需要用户手动点击

> 网页授权流程分为四步：
> 引导用户进入授权页面同意授权，获取 code
> 通过 code 换取网页授权 access_token（与基础支持中的 access_token 不同）
> 如果需要，开发者可以刷新网页授权 access_token，避免过期
> 通过网页授权 access_token 和 openid 获取用户基本信息（支持 UnionID 机制）

然后我们可以通过 H5 静默授权获得到唯一的**code**码然后传给后端，后端去拿这个**code**码去换取用户的**appid**（因为前端优有跨域），然后就可以调取我前面说的 API 去唤醒支付了
