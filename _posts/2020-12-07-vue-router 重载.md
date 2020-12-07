---
layout: post
title: 关于vue-router 重载
date: 2020-12-07
categories: cutomizer
tags: vue vue-router
---
# 关于vue-router 重载
## route mode 
mode
类型: string

默认值: "hash" (浏览器环境) | "abstract" (Node.js 环境)

可选值: "hash" | "history" | "abstract"

配置路由模式:

hash: 使用 URL hash 值来作路由。支持所有浏览器，包括不支持 HTML5 History Api 的浏览器。

history: 依赖 HTML5 History API 和服务器配置。查看 HTML5 History 模式。

abstract: 支持所有 JavaScript 运行环境，如 Node.js 服务器端。如果发现没有浏览器的 API，路由会自动强制进入这个模式。

## 如果目的地和当前路由相同，只有参数发生了改变
```
1. watch $route 对象

2. beforeRouteUpdate (vue-router 2.2之后)
    组件内的守卫：
    beforeRouteEnter
    beforeRouteUpdate (2.2 新增)
    beforeRouteLeave

3. <view-router :key="$route.fullpath" /> 刷新整个组件 

```

## 如果目的地和当前路由相同，且参数一致
```
主动刷新
1. window.location.reload()
2. 点击按钮跳转一个空白页，然后再马上跳回来
3. <router-view v-if="isRouterAlive"></router-view>  provide/inject 向子组件提供方法

带时间参数：new Date().getTime()
```