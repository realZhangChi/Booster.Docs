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

Booster.WeChat 在`IAuthorizationService`接口中定义了微信登录，它位于`Booster.WeChat.Services.Identity`名称空间。注入接口`IAuthorizationService`并调用`AuthorizeAsync()`以进行微信登录。

``` C#
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
```

用户在微信中授权后，微信会携带授权码进行回调。Booster处理微信回调，自动获取`Token`和个人信息`UserInfo`。`Token`和`UserInfo`都将存储在设备安全存储空间中。使用Booster进行登录后可获取`Token`和用户信息`UserInfo`。

### 消息

在处理微信回调时，会尝试从微信获取AccessToken并利用Token获取用户在微信中的个人信息。

完成回调处理后，会通过`MessagingCenter`发送消息。

    MessagingCenter.Send(
        (IAuthorizationService)this,
        AuthorizationMessages.Success,
        AuthorizationMessageArgs.SuccessInstance());

可以在适当的位置订阅`IAuthorizationService`发送的`AuthorizationMessages.Success`消息以获取登录成功的通知。

    MessagingCenter.Subscribe<IAuthorizationService, AuthorizationMessageArgs>(
        this,
        AuthorizationMessages.Success,
        (sender, args) =>
        {
    
        });

如果回调获取Token失败，会通过`MessagingCenter`发送消息。

    MessagingCenter.Send(
        (IAuthorizationService)this,
        AuthorizationMessages.Failed,
        AuthorizationMessageArgs.FailedInstance("Token is NULL!"));

可以在适当的位置订阅`IAuthorizationService`发送的`AuthorizationMessages.Failed`消息以处理登录失败的场景。

    MessagingCenter.Subscribe<IAuthorizationService, AuthorizationMessageArgs>(
        this,
        AuthorizationMessages.Failed,
        (sender, args) =>
        {
    
        });

## Token

注入`ITokenStore`接口并调用`GetOrNullAsync`方法来获取`Token`。

```C#
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
```

## 用户信息

注入`IUserInfoStore`接口并调用`GetOrNullAsync`方法来获取用户信息。

```C#
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
```