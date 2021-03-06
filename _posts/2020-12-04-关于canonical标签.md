---
layout: post
title: 关于canonical标签
date: 2020-12-04
categories: seo
tags: seo
---
# canonical 标签
canonical是 Google、雅虎、微软等搜索引擎一起推出的一个标签，它的主要作用是用来解决由于网址形式不同内容相同而造成的内容重复问题。这个标签对搜索引擎作用非常大，简单的说它可以让搜索引擎只抓取你想要强调的内容。

举个简单的例子，来看下如下的网址：
```
https://www.yzznl.cn/archives/2011-snow.html
https://www.yzznl.cn/archives/2011-snow.html?comments=true
https://www.yzznl.cn/archives/2011-snow.html?postcomment=true
```
这三个网址形式不同，第一个才是我们想显示给搜索引擎和用户的网址，但是打开它们网站的内容却是相同的。一般像这种状况搜索引擎是很难分辨出来哪个才是网站主想要强调的网址，这样会直接造成搜索引擎在你的站里面收录到大量重复的内容，现在我们通过 canonical 标签就可以解决这些棘手的问题了。

像上面的状况，我们只需要在网址的 head 区域添加如下代码：
```
<link rel='canonical' href='https://www.yzznl.cn/archives/2011-snow.html' />
```
这样的话 Google 等搜索引擎最终都会只收录 canonical 标签指定的这个网址，搜索引擎会将其它页面作为重复内容，这些重复的内容不再参与页面的权重分配（如 Google 的 PR 值）。

# 添加方法
由于我们的项目是vue应用,推荐使用vue-meta 进行mate动态管理HTML head信息

```

<script>
  export default {
    metaInfo () {
      return {
        title: this.title,
        link: 
        [
            {
                rel: 'canonical',
                href: 'https://xxx/xxx'
            }
        ]
      }
    }
  }
</script>
    
```
nuxt使用的也是vue-meta 使用方法一致


# head标签含义
 1. title
```
网页唯一标题标签
```
 2. base
```
<base> 标签为页面上的所有链接规定默认地址或默认目标。

通常情况下，浏览器会从当前文档的 URL 中提取相应的元素来填写相对 URL 中的空白。

使用<base> 标签可以改变这一点。浏览器随后将不再使用当前文档的 URL，而使用指定的基本 URL 来解析所有的相对 URL。这其中包括 <a>、<img>、<link>、<form> 标签中的 URL, target属性只影响当前页面内链接的打开方式

<base href="http://localhost/test/" target="_self"> 

```
 3. link
```
link是一个链接标签，包括外部css文件引用、js文件引用、favicon.ico图标引用等作用

<link rel="icon" href="/favicon.ico" > 图标
【但是对于IOS的图标，icon属性无效，需使用 apple-touch-icon and apple-touch-startup-image 。】

<link rel="alternate" href="url"  >，方便了浏览器插件（例如翻译插件，下载插件）和搜索引擎的搜索

<link rel="author license" href="url"  >,url所指向的就是这些信息所在的文档。

<link rel="canonical" href="url"  >,url所指向的html文档，即使权威版本，内容更加正确，方便搜索引擎的分析。

<link rel="preconnect" href="">

    rel="preconnect"或者rel="prefetch"或者rel="preload"等都是用于加快网页的一个加载速度的类型，只有部分浏览器实现了。
    
    preconnect是告知浏览器提前连接指定的url，以便在后面需要使用该连接的时候，连接已经形成，节省了时间。
    
    prefetch是告知浏览器立刻取来url所指向的资源，这个适用于该资源立刻需要被用户使用。

    preload是告知浏览器预加载一些url指定的资源，这些资源可能立刻会被使用。
    

```
 4. meta
```
总结起来，meta标签共有两个属性，分别是http-equiv属性和name属性。

1.name属性

A. keywords(关键字)

B. description(网站内容的描述)

C. viewport(移动端的窗口)

D. robots(定义搜索引擎爬虫的索引方式)

    举例：

    <meta name="robots" content="none">
    
    具体参数如下：
    
    1.none : 搜索引擎将忽略此网页，等价于noindex，nofollow。
    2.noindex : 搜索引擎不索引此网页。
    3.nofollow: 搜索引擎不继续通过此网页的链接索引搜索其它的网页。
    4.all : 搜索引擎将索引此网页与继续通过此网页的链接索引，等价于index，follow。
    5.index : 搜索引擎索引此网页。
    6.follow : 搜索引擎继续通过此网页的链接索引搜索其它的网页。
    
E. author(作者)

F. generator(网页制作软件)

G. copyright(版权)

H. revisit-after(搜索引擎爬虫重访时间)

I. renderer(双核浏览器渲染方式)

    说明：renderer是为双核浏览器准备的，用于指定双核浏览器默认以何种方式渲染页面。比如说360浏览器。举例：
    
    <meta name="renderer"content="webkit"> //默认webkit内核
    
    <meta name="renderer"content="ie-comp"> //默认IE兼容模式
    
    <meta name="renderer"content="ie-stand"> //默认IE标准模式

2.http-equiv属性 相当于HTTP的作用

A. content-Type

B. X-UA-Compatible(浏览器采取何种版本渲染当前页面)

C. cache-control(指定请求和响应遵循的缓存机制)

    1.no-cache: 先发送请求，与服务器确认该资源是否被更改，如果未被更改，则使用缓存。
    
    2.no-store: 不允许缓存，每次都要去服务器上，下载完整的响应。（安全措施）

    3.public : 缓存所有响应，但并非必须。因为max-age也可以做到相同效果

    4.private : 只为单个用户缓存，因此不允许任何中继进行缓存。（比如说CDN就不允许缓存private的响应）

    5. maxage : 表示当前请求开始，该响应在多久内能被缓存和重用，而不去服务器重新请求。例如：max-age=60表示响应可以再缓存和重用 60 秒。

D. expires(网页到期时间)

    <meta http-equiv="expires" content="Sunday26 October 2016 01:00 GMT" />
    
    说明:用于设定网页的到期时间，过期后网页必须到服务器上重新传输。举例：

E. refresh(自动刷新并指向某页面)

    <metahttp-equiv="refresh" content="2；URL=http://www.lxxyx.win/"> //意思是2秒后跳转向我的博客

F. Set-Cookie(cookie设定)
    
    说明：如果网页过期。那么这个网页存在本地的cookies也会被自动删除。
    
    <metahttp-equiv="Set-Cookie" content="name, date"> //格式

    <metahttp-equiv="Set-Cookie" content="User=Lxxyx; path=/;expires=Sunday, 10-Jan-16 10:00:00 GMT">



``` 
 5. script
```
<scripttype="text/javascript"></script>
script是引入外部js文件作用
``` 
 6. style
```
<styletype="text/css"> </style>
style直接嵌入网页的js或css文件标签。
```