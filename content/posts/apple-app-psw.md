+++
date = '2026-08-06T17:39:21+08:00'
draft = false
title = 'Apple App 专用密码'
+++

# 创建 App 专用密码

Apple App 专用密码用于第三方应用登录你的 Apple 账户，例如在 Outlook、Thunderbird 或其他邮件客户端中添加 iCloud 邮箱；它不是你的 Apple 账户主密码。生成前需要开启“双重认证”

## 如何创建

登录网站 https://account.apple.com/sign-in 用 Apple 开发者账号登录

- 登录之后，会跳转至 https://account.apple.com/account/manage
![图片说明](/apple_app/manage_1-compressed.webp)
- 点击`+`
![图片说明](/apple_app/manage_2-compressed.webp)
- 出现弹窗，输入标题(字符串自己定义)，然后点击创建
![图片说明](/apple_app/manage_3-compressed.webp)
- 最后会打印的专用密码，一定要记住和保存好专用密码(点击完成后不能再次查看)
![图片说明](/apple_app/manage_4-compressed.webp)

## 凭证存入 macOS 钥匙串

```Bash
xcrun notarytool store-credentials "my-app-notary(钥匙串凭证配置名称)" \
               --apple-id "你的Apple账户邮箱(你刚才登录的账号)" \
               --team-id "你的TEAM_ID(你的团队id)"  \
               --password "App专用密码(刚才需要记住的专用密码)"
```

以后提交公证时，通过相同名称读取凭证：

```Bash
xcrun notarytool submit MyApp.zip \
  --keychain-profile "my-app-notary" \
  --wait
```
