---
title: "简介"
linkTitle: "简介"
date: 2021-10-14
weight: 1
description: >
  Maui.Toolkit.WeChat 将微信官方提供的SDK进行了绑定类库转换，并基于转换后的类库，实现了微信开放平台的功能，使其开箱即用。
---

{{% pageinfo %}}
我们的文档将介绍如何通过 Maui.Toolkit.WeChat 来使用微信开放平台功能。微信开放平台的详细信息及流程原理等参见<a href='https://developers.weixin.qq.com/doc/oplatform/Mobile_App/Resource_Center_Homepage.html' target='_blank'>微信开放平台官方文档</a>。
{{% /pageinfo %}}

我们将微信开放平台的功能抽象成为一系列接口，并为不同的平台提供了默认的实现。开发人员只需调用我们定义的接口即可使用微信开放平台的功能，无需针对不同平台进行特殊处理。

微信开放平台支持移动应用和网页应用的对接。在Maui.Toolkit.WeChat中，对于Android和iOS等移动端，默认的功能实现是遵循了移动应用的方案；对于Windows及Mac等桌面端，默认的功能实现是遵循了网页应用的方案。
