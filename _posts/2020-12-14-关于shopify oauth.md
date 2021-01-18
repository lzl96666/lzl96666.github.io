---
layout: post
title: 关于shopify oauth
date: 2020-12-14
categories: cutomizer
tags: shopify oauth
---
### shopify oauth 授权流程
1. 点击安装 跳转至授权页面 并携带 {hmac}{shop} {timestamp}
2. 用这三个参数请求去授权url     
```
https://{shop}.myshopify.com/admin/oauth/authorize?client_id={api_key}&scope={scopes}&redirect_uri={redirect_uri}&state={nonce}&grant_options[]={access_mode}  
可获得code state
```
3. 商户授权之后， 回到你的 url，有个 code， 你要用这个 code 去 shopify 换取 access token， 这个 token 需要保存下来。

```
POST https://{shop}.myshopify.com/admin/oauth/access_token

client_id: The API key for the app, as defined in the Partner Dashboard.
client_secret: The API secret key for the app, as defined in the Partner Dashboard.
code: The authorization code provided in the redirect.

```

测试号 83413770 a19950326.




### 应用加载时 /store/index
1. 是否登陆
2. 登陆的情况下是否已授权
3. 已授权的情况下 保存授权信息

### Shopify/login
/shopify/login?hmac={hmac}&shop={hmac}&timestamp={hmac}

1.中间件 shopify-not-authenticated 
    
    shopify根据授权信息判断已授权？ 跳回shopify后台||进入

2.登录
    
    1.是否授权 
    2.是=>跳回shopify后台||进入
    2.否=>是否含有授权参数
    3.有授权参数=>登录=>跳回shopify后台||进入
    3.没有授权参数=>获取授权URL=>页面整个跳转



https://shop/admin/apps/test-forudesigns-app


### [流程图](https://www.edrawsoft.cn/viewer/public/s/max/c6485344785822)


### 其他登陆权限
- [x] 商店名称：y@yopmail.com-子账号。Jael.123

- [x] 商店名称：test1218@yopmail.com-审核失败用户。123456 

- [x] 商店名称：test01@yopmail.com-试用过期等待审核用户。123456

- [x] 商店名称：16082700864111garciamark@wright.net——C端普通用户。123456
- 




https://forudesigns-spy-test2.myshopify.com/admin/oauth/authorize?
client_id=b98929ccdad545f296c41da25391fcb8&
scope=read_orders%2Cwrite_orders%2Cread_products%2Cwrite_products%2Cread_inventory%2Cwrite_inventory&
redirect_uri=https%3A%2F%2Fb.forudesigns.cn%2Fshopify%2Flogin&
state=QVzYlmXzVkfzVYp8