---
title: 开始使用
linkTitle: 开始使用
date: 2021-10-14
weight: "2"
description: '轻松配置并开始使用 Booster.WeChat'
---

## 前提条件

已经通过<a href="https://open.weixin.qq.com/cgi-bin/index?t=home/index&lang=zh_CN" target="_blank">微信开放平台</a>创建移动应用及网页应用，并获取他们的**AppId**和**AppSecret**。

## 引用

将`Booster.WeChat`包添加到项目引用。

{{< tabs "Package Manager" ".NET CLI">}}

{{% codetab %}}

    Install-Package Booster.WeChat -Version 1.0.0-preview1

{{% /codetab %}}

{{% codetab %}}

    dotnet add package Booster.WeChat --version 1.0.0-preview1

{{% /codetab %}}

{{< /tabs >}}

## 配置

1. 在您的Maui项目中的`MauiProgram.cs`中添加少量的代码即可开始使用Booster.WeChat：

    ```C#
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

2. 编辑Maui项目文件*.csproj，加入以下内容：
    ``` xml
    <ItemGroup>
        <CompilerVisibleProperty Include="ApplicationId" />
    </ItemGroup>
    ```
   此步骤将允许Booster.WeChat在编译期间获取到`ApplicationId`属性，并根据`ApplicationId`在Android平台中生成与微信交互所必须的`Activity`。

以上就是使用Booster.WeChat所需的全部配置，注入服务并开始使用吧！

## 下一步

* [登录](/docs/wechat/login/): 通过微信登录您的应用
