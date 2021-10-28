---
title: 登录
linkTitle: 登录
date: 2021-10-21
weight: "1"
description: '通过微信登录你的应用。

'

---
{{% pageinfo %}}
首先请阅读[开始使用](https://docs.mauitoolkit.com/zh-hans/docs/toolkits/wechat/get-started/#配置)章节确保完成与微信交互所需的配置。
{{% /pageinfo %}}

在移动应用中，调用微信登录将唤起微信APP并请求用户授权；在桌面应用中，将访问微信网页应用授权网址以展示二维码。

## 开始使用

Maui.Toolkit.WeChat 在`IAuthorizationService`接口中定义了微信登录，它位于`Maui.Toolkit.WeChat.Services.Identity`名称空间。

注入接口`IAuthorizationService`并调用`AuthorizeAsync()`方法，即可唤起微信登录。

一般地，了解以上知识即可通过Maui.Toolkit.WeChat使用微信登录，Maui.Toolkit.WeChat将会自动处理登录回调并从微信获取用户信息。

## **下一步**

* [用户信息](docs/toolkits/wechat/login/user-info/)：通过`IUserInfoStore`获取用户信息