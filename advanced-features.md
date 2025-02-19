---
title: 进阶功能
description: AUTO_MAA 的高级配置指南
date: 2025-02-10
---

# 进阶功能

在了解完基础的用法后，您可以根据教程尝试配置以下功能。

## 代理结果消息推送

在 **通知** 选项中，您可以配置 **代理成功消息推送** 的渠道。

## ServerChan 方式推送

在 **v4.2.2-beta.2** 版本中，新增了 **ServerChan** 的推送方式。

#### 什么是 ServerChan？

「Server酱」，英文名「ServerChan」，是一款 **手机** 与 **服务器/智能设备** 之间的通信工具。它的主要作用是：

- 让服务器、路由器等设备推送消息到手机。
- 在这里，它用于 **AUTO_MAA 代理成功后推送消息到手机**。

更多信息请查看：

<Box :items="[
{ name: 'Server酱Turbo版', link: 'https://sct.ftqq.com/', image: 'https://the7.ft07.com/sct/images/favicon.png' },
{ name: 'Server酱³', link: 'https://sc3.ft07.com/', image: 'https://the7.ft07.com/sct/images/favicon.png' },
]"/>

::: warning 注意
Server酱官方在 2024 年推出了一种新的 App 推送渠道，与原来的 **Server酱·Turbo 版** （SCT）不同，并重新命名为 **Server酱³**
（SC3）。

在以下配置中，我们使用 **SCT** 代指 **Server酱·Turbo版**，**SC3** 代指 **Server酱³**。
:::

### SendKey

SendKey 是 **Server酱** 平台对用户的认证方式。只有 **提供 SendKey**，AUTO_MAA 才能将消息精准推送到您的设备。

SCT
平台获取Key：<Pill name="SCT SendKey" image="https://the7.ft07.com/sct/images/favicon.png" link="https://sct.ftqq.com/sendkey"/>

SC3
平台获取Key：<Pill name="SC3 SendKey" image="https://the7.ft07.com/sct/images/favicon.png" link="https://sc3.ft07.com/sendkey"/>

:::warning 注意
以上两个平台仅需选择一个即可，请根据您的实际情况选择。
:::

#### ServerChanChannel 代码

**SC3 仅支持 App 推送**，因此 **仅 SCT 平台可填写 ServerChanChannel 代码**。

以下是 **可用消息渠道代码**，您需要填写 **对应的数字代码**。

| 渠道             | 代码 |
|----------------|----|
| 官方 Android 版·β | 98 |
| 企业微信应用消息       | 66 |
| 企业微信群机器人       | 1  |
| 钉钉群机器人         | 2  |
| 飞书群机器人         | 3  |
| Bark iOS       | 8  |
| 测试号            | 0  |
| 自定义            | 88 |
| PushDeer       | 18 |
| 方糖服务号          | 9  |

::: tip **多个渠道填写格式**
**多个渠道请用 `|` 分隔，格式如下：**

- ❌ `1 | 0 | 9`
- ✔️ `1|0|9`

如果未正确填写，系统将使用 **默认推送渠道**。
:::

#### Tag 内容

该功能是 **SC3 平台的新特性**，仅适用于 **SC3**。

::: tip **Tag 填写格式**
**多个 Tag 请用 `|` 分隔**，格式如下：

- ❌ `AutoMAA | 代理情况`
- ✔️ `AutoMAA|代理情况`

若留空或填写不正确，则推送消息时不会携带 Tag 信息。
:::

## SMTP 邮件推送

除了 ServerChan，您还可以使用 **SMTP 电子邮件** 方式推送消息。

为了确保您能够顺利发送通知邮件，请按照以下步骤操作，完成必要的设置。

### 如何选择 SMTP 服务器地址

不同的电子邮件服务商有不同的 SMTP 服务器地址。请根据您使用的电子邮件服务提供商选择正确的 SMTP 服务器地址。这里列出一些常用的电子邮件服务及其
SMTP 服务器地址：

```txt
1. Gmail: smtp.gmail.com
2. Outlook/Hotmail: smtp-mail.outlook.com
3. Yahoo Mail: smtp.mail.yahoo.com
4. QQ邮箱: smtp.qq.com
5. 163邮箱: smtp.163.com
```

如果您使用的电子邮件服务不在上述列表中，请访问该邮件服务的帮助中心或搜索其 SMTP 服务器地址。通常可以在邮件服务商的官方网站的帮助文档中找到相关信息。

### 如何申请授权码

授权码是用于替代您的邮箱密码进行第三方客户端登录的一种特殊密码。以下是获取不同邮件服务商授权码的一般步骤，具体步骤可能会因邮件服务商的不同而有所变化，请参考相应服务商的官方说明：

#### 1. Gmail

- 访问您的 Google 账号管理页面。
- 在“安全性”选项中找到“App 密码”，生成一个新的应用专用密码。

#### 2. Outlook/Hotmail

- 登录到您的 Outlook 账户。
- 转到“我的账户” > “安全和隐私” > “更多安全选项”。
- 在“应用程序密码”部分，创建一个新的应用程序密码。

#### 3. Yahoo Mail

- 登录到您的 Yahoo 账户。
- 前往账户的安全设置。
- 找到“生成应用程序密码”或类似选项以创建新的应用密码。

#### 4. QQ邮箱

<Pill name="QQ邮箱官方教程" image="https://res.wx.qq.com/t/webmail/webmail/res/static/images/projects/login/loginpage/qqmail_logo_default_35h.e071fb4.png" link="https://service.mail.qq.com/detail/0/75"/>

- 登录到您的 QQ 邮箱。
- 点击“设置” > “账户”。
- 在“POP3/IMAP/SMTP/Exchange/CardDAV/CalDAV服务”部分，开启对应服务并按提示获取授权码。

#### 5. 163邮箱

<Pill name="163邮箱官方教程" image="https://help.mail.163.com/style/img/logo-163.png" link="https://help.mail.163.com/faqDetail.do?code=d7a5dc8471cd0c0e8b4b8f4f8e49998b374173cfe9171305fa1ce630d7f67ac2a5feb28b66796d3b"/>

- 登录到您的 163 邮箱。
- 点击“设置” > “POP3/SMTP/IMAP”。
- 开启对应的服务后，按照指示获取授权码。

::: warning 注意
请注意，出于安全考虑，强烈建议不要在公共场合泄露您的授权码，并且定期更换它。

AUTO_MAA 已对本地授权码数据使用 Windows DPAPI 加密，这种加密方式使用当前用户的登录凭据作为加密密钥的一部分，这意味着只有同一个用户在同一台计算机上才能解密数据。

如果您需要跨设备迁移配置文件，请重新输入授权码。
:::