---
title: 用户信息
linkTitle: 用户信息
date: 2021-10-21
weight: "2"
description: '获取微信中的用户信息。

'

---
使用Maui.Toolkit.WeChat进行微信登录后，会自动获取并保存用户在微信中的个人信息。

## IUserInfoStore

Maui.Toolkit.WeChat中定义并实现了了IUserInfoStore接口。在使用Maui.Toolkit进行微信登录后，即可在任意位置注入接口并调用GetOrNullAsync方法，获取到用户信息UserInfo实例。

## 下一步

* 自定义IUserInfoStore：TODO