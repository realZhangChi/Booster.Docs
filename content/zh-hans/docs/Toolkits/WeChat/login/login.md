---
title: 登录
linkTitle: 登录
date: 2021-10-21
weight: "1"
description: '通过微信登录你的应用。

'

---
在移动应用中，调用微信登录将唤起微信APP并请求用户授权；在桌面应用中，将访问微信网页应用授权网址以展示二维码。

## 开始使用

Maui.Toolkit.WeChat 在`IAuthorizationService`接口中定义了微信登录，它位于`Maui.Toolkit.WeChat.Services.Identity`名称空间。

注入接口`IAuthorizationService`并调用`AuthorizeAsync()`方法，即可唤起微信登录。

## 回调

_首先请阅读_[_开始使用_](https://docs.mauitoolkit.com/zh-hans/docs/toolkits/wechat/get-started/#配置)_章节确保完成与微信交互所需的配置。_

用户在微信中授权登录后，将携带授权码回调到Maui应用程序中。接收到回调请求后，将调用`IAuthorizationService`上的`AuthorizationCallback`方法来完成通过微信登录及后续步骤。