---
title: 注册 .NET Framework 的扩展 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- Add References dialog box, registering extensions of the .NET Framework
- MSBuild, registering extensions of the .NET Framework
- .NET Framework extensions, registering
ms.assetid: deee6f53-ea87-4b88-a120-bea589822e03
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: cad3d2d02ed27ab46410be6edc024b137bbca7bd
ms.sourcegitcommit: 42ea834b446ac65c679fa1043f853bea5f1c9c95
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
---
# <a name="registering-extensions-of-the-net-framework"></a>注册 .NET Framework 的扩展
可开发一个扩展特定版本的 .NET Framework 的程序集。 为确保该程序集出现在 Visual Studio“添加引用”对话框中，必须将包含程序集的文件夹添加到系统注册表。  
  
 例如，假定 Trey Research 公司开发出了一个可扩展 .NET Framework 4 的库，且希望当项目以 .NET Framework 4 为目标时，该库程序集可出现在“添加引用”对话框中。 同时假定该程序集是在 32 位计算机上运行的 32 位程序集或在 64 位计算机上运行的 64 位程序集，且会将其安装在 C:\TreyResearch\Extensions4\ 文件夹。  
  
 使用此密钥注册此文件夹：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework\v4.0.21006\AssemblyFoldersEx\TreyResearch\\。 为密钥赋予此默认值：C:\TreyResearch\Extensions4。  
  
> [!NOTE]
>  .NET Framework 版本的生成号可能不同。  
  
 若要在 64 位计算机上注册 32 位的程序集，请使用 Wow6432 节点，例如：HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework\v4.0.21006\AssemblyFoldersEx\TreyResearch\\。  
  
## <a name="see-also"></a>请参阅  
 [Visual Studio 集成](../msbuild/visual-studio-integration-msbuild.md)