---
title: 使用作为用于查找源代码管理插件的键的字符串 |Microsoft 文档
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, strings used for finding
ms.assetid: c1e31f76-42a1-4c3d-afb2-664044ef12fd
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: a42eebe67ce1f611cf6e48883bc09139f241e658
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="strings-used-as-keys-for-finding-a-source-control-plug-in"></a>使用作为用于查找源代码管理插件的键的字符串
以下字符串是用于访问注册表来查找有关源代码管理信息插件的项。  
  
 `STR_SCC_PROVIDER_REG_LOCATION``STR_PROVIDERREGKEY`， `STR_SCCPROVIDERPATH`，和`STR_SCCPROVIDERNAME`注册表项或值用于将注册 DLL 的源代码管理插件为 Visual Studio。  
  
 `SCC_PROJECTNAME_KEY``SCC_PROJECTAUX_KEY`， `SCC_KEY, SCC_FILE_SIGNATURE`，和`SCC_STATUS_FILE`用于描述 MSSCCPRJ 的格式。SCC 文件。  
  
## <a name="string-keys-and-values"></a>字符串键和值  
  
|键|值|  
|---------|-----------|  
|`STR_SCC_PROVIDER_REG_LOCATION`|Software\SourceCodeControlProvider|  
|`STR_PROVIDERREGKEY`|ProviderRegKey|  
|`STR_SCCPROVIDERPATH`|SCCServerPath|  
|`STR_SCCPROVIDERNAME`|SCCServerName|  
|`STR_SCC_INI_SECTION`|源代码管理|  
|`STR_SCC_INI_KEY`|SourceCodeControlProvider|  
|`SCC_PROJECTNAME_KEY`|SCC_Project_Name|  
|`SCC_PROJECTAUX_KEY`|SCC_Aux_Path|  
|`SCC_STATUS_FILE`|MSSCCPRJ。SCC|  
|`SCC_KEY`|SCC|  
|`SCC_FILE_SIGNATURE`|源代码控制文件|  
|`SCC_NSE`|Namespace 扩展|  
|`SCC_NSE_PREFIX`|Protocal 前缀|  
|`SCC_NSE_DisableOpenSCC`|DisableOpenFromSourceControl|  
|`STR_SCCHELPCOLLECTION`|HelpCollection|  
|`STR_UI_LANGUAGE`|G u a g|  
|`STR_SRCSAFE_ROOT_KEY`|Software\Microsoft\SourceSafe|  
  
## <a name="see-also"></a>另请参阅  
 [源控件插件](../extensibility/source-control-plug-ins.md)   
 [如何： 安装了源代码管理插件](../extensibility/internals/how-to-install-a-source-control-plug-in.md)   
 [MSSCCPRJ.SCC 文件](../extensibility/mssccprj-scc-file.md)