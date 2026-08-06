+++
date = '2026-08-06T14:54:25+08:00'
draft = true
title = 'AWS 开发环境搭建'
+++

# AWS 开发环境搭建

## 1. Windows 安装 AWS CLI

## 下载并验证

https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html

安装完成后，启动终端，输入

```shell
aws --version
```

## 配置环境 ID & Key

使用终端，输入

```shell
aws configure
```

按照要求输入`AWS Access Key ID`，`AWS Secret Access Key`，`Default region name`，`Default output format`
完成后会生成在 C:\Users\<username>\.aws

![图片说明](/static/aws/aws_path.png)

## 2. Linux 安装 AWS CLI

https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

安装完成后，启动终端，输入

```shell
aws --version
```

## 配置环境 ID & Key

使用终端，输入

```shell
aws configure
```

如果有多套，可以使用如下，xxx 为环境名称

```shell
aws configure --profile xxx
```

按照要求输入`AWS Access Key ID`，`AWS Secret Access Key`，`Default region name`，`Default output format`

验证文件生成

```shell
ls -a ~/.aws/
```

查看

```shell
cat ~/.aws/credentials
```
