+++
date = 2021-10-28T12:19:52Z
description = "通过微信登录并获取用户信息"
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

    public partial class MainPage : ContentPage
    {
        private readonly IAuthorizationService _authorizationService;
    
        public MainPage(IAuthorizationService authorizationService)
        {
            _authorizationService = authorizationService;
        }
    
        private async void OnAuthorizeClicked(object sender, EventArgs e)
        {
            await _authorizationService.AuthorizeAsync();
        }
    }

用户在微信中授权后，微信会携带授权码进行回调。Maui.Toolkit会自动处理微信回调，根据授权码获取`Token`，获取用户在微信中的个人信息`UserInfo`。`Token`和`UserInfo`都将存储在设备安全存储空间中。

## Token

Maui.Toolkit中定义并实现了ITokenStore接口。在使用Maui.Toolkit进行微信登录后，即可在任意位置注入接口并调用`GetOrNullAsync`方法，获取到用户信息`UserInfo`实例。

    public partial class MainPage : ContentPage
    {
        private readonly ITokenStore _tokenStore;
        public MainPage(ITokenStore tokenStore)
        {
            _tokenStore = tokenStore;
        }
    
        public async Task<Token> GetToken()
        {
            return await _tokenStore.GetOrNullAsync();
        }
    }

## 用户信息

Maui.Toolkit中定义并实现了`IUserInfoStore`接口。在使用Maui.Toolkit进行微信登录后，即可在任意位置注入接口并调用`GetOrNullAsync`方法，获取到用户信息`UserInfo`实例。

    public partial class UserInfoPage : ContentPage
    {
        private readonly IUserInfoStore _userInfoStore;
        public UserInfoPage(IUserInfoStore userInfoStore)
        {
            _userInfoStore = userInfoStore;
        }
    
        public async Task<UserInfo> GetUserInfo()
        {
            return await _userInfoStore.GetOrNullAsync();
        }
    }

## 自定义

Maui.Toolkit.WeChat已默认实现了微信登录的相关功能，一般情况下，只需注入并调用接口即可。当需要更复杂的处理的时候，可以轻松对服务进行扩展或替换为自定义实现。