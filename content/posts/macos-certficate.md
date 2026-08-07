+++
date = '2026-08-06T16:56:02+08:00'
draft = false
title = 'macos 分发证书'
+++

# macOS 应用分发需要哪些证书

## 官网、企业内部或第三方渠道下载

### 创建相关证书

https://developer.apple.com/help/account/certificates/create-developer-id-certificates/

使用：

- Developer ID Application：签名 .app
- Developer ID Installer：签名 .pkg 安装包

注意：需要根账号创建
![图片说明](/macos/create-cert.jpg)

## 发布到 Mac App Store

使用：

- Mac App Distribution：签名 App
- Mac Installer Distribution：签名提交到商店的安装包

## 各种证书用途

Apple 官方对这些证书用途的分类如下：https://developer.apple.com/help/account/certificates/certificates-overview/