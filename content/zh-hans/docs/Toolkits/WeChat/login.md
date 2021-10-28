+++
date = 2021-10-28T12:19:52Z
description = "通过微信登录并获取用户信息"
draft = true
linkTitle = "登录"
title = "登录"
weight = "3"

+++
{{% pageinfo %}}

此文档将介绍如何使用 Maui.Toolkit.WeChat 来调用微信登录等功能。微信登录功能的详细文档参见<a href='[https://developers.weixin.qq.com/doc/oplatform/Mobile_App/WeChat_Login/Development_Guide.html](https://developers.weixin.qq.com/doc/oplatform/Mobile_App/WeChat_Login/Development_Guide.html "https://developers.weixin.qq.com/doc/oplatform/Mobile_App/WeChat_Login/Development_Guide.html")' target='_blank'>微信开放文档</a>。

{{% /pageinfo %}}

## 登录

在移动应用中，调用微信登录将唤起微信APP并请求用户授权；在桌面应用中，将访问微信网页应用授权网址以展示二维码。

Maui.Toolkit.WeChat 在`IAuthorizationService`接口中定义了微信登录，它位于`Maui.Toolkit.WeChat.Services.Identity`名称空间。注入接口`IAuthorizationService`并调用`AuthorizeAsync()`，即可唤起微信登录。

用户在微信中授权后，将携带授权码回调，Maui.Toolkit.WeChat将会自动处理回调，根据授权码获取Token，获取用户在微信中的个人信息UserInfo。Token和UserInfo都将存储在设备安全存储空间中。

## Token

## 用户信息

Maui.Toolkit.WeChat中定义并实现了了IUserInfoStore接口。在使用Maui.Toolkit进行微信登录后，即可在任意位置注入接口并调用GetOrNullAsync方法，获取到用户信息UserInfo实例。