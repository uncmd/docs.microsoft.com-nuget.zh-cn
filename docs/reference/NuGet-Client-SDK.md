---
title: NuGet 客户端 SDK
description: 此 API 已发展，但尚未记录在 Dave Glick 的博客上。
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 39a4de4071eec70c88a2add158f2a3a734f7d7b7
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622923"
---
# <a name="nuget-client-sdk"></a>NuGet 客户端 SDK

*Nuget 客户端 SDK*引用一组 NuGet 包：

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -用于与基于 HTTP 和文件的 NuGet 源交互
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -用于与 NuGet 包交互。 `NuGet.Protocol` 依赖于此包

你可以在 [NuGet/nuget。客户端](https://github.com/NuGet/NuGet.Client) GitHub 存储库中找到这些包的源代码。

> [!Note]
> 有关 NuGet 服务器协议的文档，请参阅 [Nuget 服务器 API](~/api/overview.md)。

## <a name="getting-started"></a>入门

### <a name="install-the-packages"></a>安装包

```ps1
dotnet add package NuGet.Protocol  # interact with HTTP and folder-based NuGet package feeds, includes NuGet.Packaging

dotnet add package NuGet.Packaging # interact with .nupkg and .nuspec files from a stream
```

## <a name="examples"></a>示例

你可以在 GitHub 上的 [nuget.exe](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) 项目上找到这些示例。

### <a name="list-package-versions"></a>列出包版本

使用 [NuGet V3 包内容 API](../api/package-base-address-resource.md#enumerate-package-versions)查找 Newtonsoft.Js的所有版本：

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>下载包

使用 [NuGet V3 包内容 API](../api/package-base-address-resource.md)在12.0.1 上下载 Newtonsoft.Js：

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>获取包元数据

使用 [NuGet V3 包元数据 API](../api/registration-base-url-resource.md)获取 "Newtonsoft.Json" 包的元数据：

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>搜索包

使用 [NuGet V3 搜索 API](../api/search-query-service-resource.md)搜索 "json" 包：

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="create-a-package"></a>创建包

使用创建包、设置元数据并添加依赖项 [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) 。

> [!IMPORTANT]
> 强烈建议使用官方 NuGet 工具创建 NuGet 包，而 **不** 是使用此低级别 API。 很多特性对于格式正确的包都很重要，最新版本的工具有助于合并这些最佳做法。
> 
> 有关创建 NuGet 包的详细信息，请参阅 [包创建工作流](../create-packages/overview-and-workflow.md) 概述和官方包工具文档 (例如， [使用 dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)) 。

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a>读取包

使用从文件流中读取包 [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) 。

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a>第三方文档

可以在以下博客系列中的 Dave Glick （已发布2016：

- [浏览 NuGet v3 库，第1部分：简介和概念](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [浏览 NuGet v3 库，第2部分：搜索包](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [浏览 NuGet v3 库，第3部分：安装包](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> **3.4.3**版本的 NuGet 客户端 SDK 包发布后，不久就会编写这些博客文章。
> 较新版本的包可能与博客文章中的信息不兼容。

圣马丁 Björkström 对 Dave Glick 的博客系列进行了跟进博客文章，其中介绍了使用 NuGet 客户端 SDK 安装 NuGet 包的不同方法：

- [重新进行 NuGet v3 库](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
