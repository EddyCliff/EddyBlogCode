---
title: "【Hugo网站搭建】图床工具PicGo-bug日志"
date: 2023-08-30T00:17:58+08:00
lastmod: 2023-08-30T00:17:58+08:00
author: ["Eddy"]
keywords: 
- PicGo
- error
- bug
- image host
categories: 
- 
tags: 
- SSL证书验证机制
- bug日志
- 图床工具PicGo
description: '解决 PicGo 图床工具中的 "unable to verify the first certificate" 错误。了解错误原因、网络加速工具可能引发的问题，并探讨关闭 fastgithub 解决方案。同时介绍 PicGo 官方文档中的常见问题和解决方法，确保图床上传稳定可靠。'
weight:
slug: ""
draft: false # 是否为草稿
comments: false
reward: false # 打赏
mermaid: true #是否开启mermaid
showToc: true # 显示目录
TocOpen: true # 自动展开目录
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
showbreadcrumbs: true #顶部显示路径
cover:
    image: "https://testingcf.jsdelivr.net/gh/EddyCliff/ChartBed/BlogCover/pc.jpg" #图片路径例如：posts/tech/123/123.png
    caption: "" #图片底部描述
    alt: ""
    relative: false
---
## 项目场景：

在使用 `PicGo` 进行图床上传时，出现了一个错误，具体的错误信息如下：

```JSON
[PicGo ERROR] {
  "method": "PUT",
  "statusCode": 0,
  "message": "unable to verify the first certificate",
  "stack": "Error: unable to verify the first certificate\n"
}
```

这个错误让我对图床上传产生了困惑，于是我进行了一些分析和研究，尝试找出问题的原因，并寻求解决方案。

## 问题描述：

在使用 `PicGo` 进行图床上传时，出现了一个与 `SSL` 证书验证相关的错误。具体的错误信息显示无法验证第一个证书，导致了上传失败。这个问题的发生使我无法顺利地上传图片到我所使用的图床，让我感到困扰。

## 原因分析：

经过我的分析，我发现这个问题可能与网络加速工具有关。尤其是在使用类似 `fastgithub` 这样的网络加速工具时，可能会出现这种问题。尽管这些工具在一些情况下可以提高访问速度，但它们有时也可能引发一些网络通信问题，特别是涉及到 `SSL` 证书验证的情况。

在网络通信中，`SSL` 证书是确保通信安全的关键组成部分。服务器使用 `SSL` 证书来证明其身份，并加密传输的数据，以防止第三方窃听或篡改。当访问一个使用 `SSL`（或其继任者 `TLS`）加密的网站或服务时，浏览器会验证服务器的 `SSL` 证书，确保连接安全。

然而，某些网络加速工具可能会修改网络流量，甚至可能与 `SSL`证书验证机制发生冲突。这可能导致 `SSL` 证书验证失败，因为服务器的证书无法正常验证，从而出现类似 `"unable to verify the first certificate"` 的错误。

## 解决方案：

根据我自己的实际尝试和一些资料的学习，我找到了一个解决方案来解决这个问题。在我的情况下，关闭 `fastgithub` 工具后，问题得到了解决。这可能是因为关闭该工具后，网络通信不再受到其影响，恢复了正常的 `SSL` 证书验证过程。

要解决类似问题，您也可以尝试以下方法：

1. **更新工具：** 如果您发现网络加速工具版本较旧，可能存在已知的问题，尝试更新到最新版本以获得修复。

2. **工具配置：** 某些工具可能允许您自定义其操作和影响。检查工具的配置选项，看看是否可以调整它们的行为以避免与 `SSL` 证书验证冲突。

3. **备用加速工具：** 如果一个工具存在问题，您可以尝试其他类似的网络加速工具，看看是否会更好地适应您的环境。

4. **不使用加速工具：** 如果问题无法解决，可能最好的方法是不使用网络加速工具，以避免潜在的网络通信问题。

最终，为了确保通信的安全和稳定，建议使用经过验证和可信赖的网络通信方式，避免引入可能的不稳定因素。

## PicGo 官方文档中的相关 FAQ

在 `PicGo` 官方文档的 `FAQ` 中，也提到了一些关于 `GitHub` 图床上传的常见问题和解决方案，您也可以参考这些内容：

### 7. GitHub 图床有时能上传，有时上传失败

1. `GitHub` 图床不支持上传同名文件，如果有同名文件上传，会报错。建议开启 `时间戳重命名` 避免同名文件。

2. `GitHub` 服务器和国内 `GFW` 的问题会导致有时上传成功，有时上传失败，无解。想要稳定请使用付费云存储，如阿里云、腾讯云等，价格也不会贵。

### 9. 上传失败，或者是服务器出错

1. `PicGo` 自带的图床都经过测试，上传出错一般都不是 `PicGo` 自身的原因。如果您用的是 `GitHub` 图床，请参考 `FAQ` 中的相关内容。

2. 检查 `PicGo` 的日志（报错日志可以在 `PicGo` 设置 -> 设置日志文件 -> 点击打开 后找到），看看 `[PicGo Error]` 的报错信息里有什么关键信息：

- 先自行搜索 `error` 里的报错信息，往往您可以通过搜索引擎找到问题的原因，不必立即提交问题。

- 如果报错信息带有 `401`、`403` 等 `40X` 状态码字样，不用怀疑，很可能是配置信息有误，仔细检查配置，确保没有多余的空格等。

- 如果报错信息带有 `HttpError`、`RequestError`、`socket hang up` 等字样，说明这是网络问题。在这种情况下，您需要检查自己的网络，是否存在代理、`DNS` 设置是否正常等。

- 通常情况下，上传失败很可能是因为网络问题导致的。如果您开启了系统代理，建议同时在 `PicGo` 的代理设置中设置对应的 `HTTP` 代理，详情请参考相关文档。

通过我的研究和实践，我找到了解决这个 `"unable to verify the first certificate"` 问题的方法，也了解了一些关于 `PicGo` 的官方文档中提供的解决方案。希望这些信息能够帮助到您解决类似问题，确保您能够顺利地使用 `PicGo` 进行图床上传。如果您遇到了类似问题，不妨尝试我的解决方案，也可以参考官方文档中的相关内容，找到适合您的解决方法。

## 资料参考

![PicGo FAQ.md](https://github.com/Molunerfinn/PicGo/blob/dev/FAQ.md)



