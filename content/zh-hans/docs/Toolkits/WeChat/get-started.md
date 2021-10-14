---
title: "开始使用"
linkTitle: "开始使用"
date: 2021-10-14
weight: 2
description: >
  轻松配置您的项目使用开箱即用的 Maui.Toolkit.WeChat 工具包来集成微信开放平台功能。
---

## 前提条件

已经通过<a href="https://open.weixin.qq.com/cgi-bin/index?t=home/index&lang=zh_CN" target="_blank">微信开放平台</a>创建移动应用及网页应用，并获取他们的**AppId**和**AppSecret**。

## 引用

*TODO: 添加Nuget包引用。*

## 配置

在您的Maui项目中的`MauiProgram.cs`中添加少量的代码即可开始使用Maui.Toolkit.WeChat：

``` C#
public static class MauiProgram
{
    public static MauiApp CreateMauiApp()
    {
        var builder = MauiApp.CreateBuilder();

        builder
            .UseMauiApp<App>()

            // 添加以下代码
            .UseWeChat(
                new WeChatWebOptions
                {
                    AppId = "网页应用的AppId",
                    AppSecret = "网页应用的AppSecret",
                    RedirectUrl = "网页应用的授权回调地址"
                },
                new WeChatMobileOptions()
                {
                    AppId = "移动应用的AppId",
                    AppSecret = "移动应用的AppSecret"
                })

            .ConfigureFonts(fonts =>
            {
                fonts.AddFont("OpenSans-Regular.ttf", "OpenSansRegular");
            });


        builder.Services.AddSingleton<MainPage>();

        return builder.Build();
    }
}
```

为使您的应用正常与微信进行交互，还需要针对移动平台进行一些特殊配置：

{{< tabs Android iOS>}}

{{% codetab %}}

1. 在你的Maui项目的`/Platforms/Android/`目录下新建文件夹，命名为`WeChatApi`
2. 在`WeChatApi`目录下新建类文件`WeChatEntryActivity.cs`
3. 更改`WeChatEntryActivity.cs`的代码如下：

``` C#

[Activity(Name = "Maui.Toolkit.Sample.WeChatApi.WeChatEntryActivity", Exported = true, TaskAffinity = "Maui.Toolkit.Sample", LaunchMode = LaunchMode.SingleTask)]
public class WeChatEntryActivity : WeChat.Platforms.Android.WeChatApi.WeChatEntryActivity
{
}

```

{{% /codetab %}}

{{% codetab %}}

*TODO*

{{% /codetab %}}

{{< /tabs >}}