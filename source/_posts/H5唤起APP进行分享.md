---
title: H5唤起APP进行分享
date: 2020-07-07 10:50:57
tags:
- H5
categories:
- H5
---



# 分析实现方式

要实现在H5唤起APP的主要采用

1. URL Scheme | Intent | Universal Link（也称：深度链接）
2. 通过浏览器的内置native分享接口

## URLScheme

我们来看一下 URL 的组成：

```
[scheme:][//authority][path][?query][#fragment]
```

我们拿`https://www.baidu.com` 来举例，scheme 自然就是 `https`了。

就像给服务器资源分配一个 URL，以便我们去访问它一样，我们同样也可以给手机APP分配一个特殊格式的 URL，用来访问这个APP或者这个APP中的某个功能(来实现通信)。APP得有一个标识，好让我们可以定位到它，它就是 URL 的 Scheme 部分。

## 常用APP的 URL Scheme
| AP P| 微信 | 支付宝 | 淘宝 | 微博 | QQ | 知乎 |短信 |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|URL Scheme|weixin://|alipay://|taobao://|sinaweibo://|mqq://|zhihu://|sms://|

## URL Scheme 语法
```
     行为(应用的某个功能)    
            |
scheme://[path][?query]
   |               |
应用标识       功能需要的参数
```

## 搜集到的常用Scheme
| **应用名称**      | **URL Scheme**                                               |
| ----------------- | ------------------------------------------------------------ |
| 微博              | weibo://                                                     |
| QQ                | mqq://                                                       |
| QQ群组            | [mqqapi://card/show_pslcard?src_type=internal&version=1&card_type=group&uin=](mqqapi://card/show_pslcard?src_type=internal&version=1&card_type=group&uin=){QQ群号} |
| QQ联系人          | [mqqapi://card/show_pslcard?src_type=internal&version=1&uin=](mqqapi://card/show_pslcard?src_type=internal&version=1&uin=){QQ号码} |
| 支付宝            | alipay://                                                    |
| 微信              | weixin://                                                    |
| 微信              | wechat://                                                    |
| 微信-扫一扫       | [weixin://dl/scan](weixin://dl/scan)                         |
| 微信-反馈         | [weixin://dl/feedback](weixin://dl/feedback)                 |
| 微信-朋友圈       | [weixin://dl/moments](weixin://dl/moments)                   |
| 微信-设置         | [weixin://dl/settings](weixin://dl/settings)                 |
| 微信-消息通知设置 | [weixin://dl/notifications](weixin://dl/notifications)       |
| 微信-聊天设置     | [weixin://dl/chat](weixin://dl/chat)                         |
| 微信-通用设置     | [weixin://dl/general](weixin://dl/general)                   |
| 微信-公众号       | [weixin://dl/officialaccounts](weixin://dl/officialaccounts) |
| 微信-游戏         | [weixin://dl/games](weixin://dl/games)                       |
| 微信-帮助         | [weixin://dl/help](weixin://dl/help)                         |
| 微信-个人信息     | [weixin://dl/profile](weixin://dl/profile)                   |
| 微信-功能插件     | [weixin://dl/features](weixin://dl/features)                 |
| 虾米音乐          | xiami://                                                     |
| chrome            | googlechrome://                                              |
| 微博国际版        | weibointernational://                                        |
| 摩拜单车          | mobike://                                                    |
| ofo               | ofoapp://                                                    |
| 有道云笔记        | youdaonote://                                                |
| 印象笔记          | evernote://                                                  |
| 今日头条          | snssdk141://                                                 |
| 网易新闻          | newsapp://                                                   |
| 网易云音乐        | orpheuswidget://                                             |
| QQ音乐            | qqmusic://                                                   |
| QQ音乐最近播放    | [qqmusic://today?mid=31&k1=2&k4=0](qqmusic://today?mid=31&k1=2&k4=0) |
| 美团外卖          | meituanwaimai://                                             |
| 美团              | imeituan://                                                  |
| Gmail             | googlegmail://                                               |
| 网易邮箱          | neteasemail://                                               |
| QQ邮箱            | qqmail://                                                    |
| 腾讯视频          | tenvideo://                                                  |
| 爱奇艺            | iqiyi://                                                     |
| 12306             | cn.12306://                                                  |
| 有道词典          | yddict://                                                    |
| 钉钉              | dingtalk://                                                  |


# 参考文章

[H5唤起APP进行分享的尝试](https://www.jianshu.com/p/500f4be528e3)

[常用URL Scheme](https://blog.csdn.net/xttxqjfg/article/details/76019824)

[H5唤起APP指南](https://suanmei.github.io/2018/08/23/h5_call_app/)


