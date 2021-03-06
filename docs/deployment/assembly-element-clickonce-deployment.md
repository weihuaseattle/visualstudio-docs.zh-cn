---
title: '&lt;程序集&gt;元素 （ClickOnce 部署） |Microsoft 文档'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#assembly
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <assembly> element [ClickOnce deployment manifest]
ms.assetid: b8e3362a-f821-4696-b98d-571d4bbfe431
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e6b12f1a5d50e2636d3c8478e6b6a9efe50384a5
ms.sourcegitcommit: 1b9c1e333c2f096d35cfc77e846116f8e5054557
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2018
ms.locfileid: "34815660"
---
# <a name="ltassemblygt-element-clickonce-deployment"></a>&lt;程序集&gt;元素 （ClickOnce 部署）
部署清单的的顶级元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
      <assembly    
   manifestVersion  
/>  
```  
  
## <a name="elements-and-attributes"></a>元素和属性  
 `assembly`元素是根元素，它需要。 其第一个包含的元素必须是`assemblyIdentity`元素。 清单元素必须在以下命名空间： `urn:schemas-microsoft-com:asm.v1`， `urn:schemas-microsoft-com:asm.v2`，和`http://www.w3.org/2000/09/xmldsig#`。 程序集的子元素也必须通过继承或使用标记这些命名空间中。  
  
 `assembly`元素具有以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`manifestVersion`|必须的。 此属性必须设置为`1.0`。|  
  
## <a name="example"></a>示例  
 下面的代码示例阐释了`assembly`部署使用的应用程序的部署清单中的元素[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]。 此代码示例摘自更大的示例为提供[ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)主题。  
  
```xml  
<asmv1:assembly   
  xsi:schemaLocation="urn:schemas-microsoft-com:asm.v1 assembly.adaptive.xsd"  
  manifestVersion="1.0"  
  xmlns:asmv3="urn:schemas-microsoft-com:asm.v3"  
  xmlns:dsig=http://www.w3.org/2000/09/xmldsig#  
  xmlns:co.v1="urn:schemas-microsoft-com:clickonce.v1"  
  xmlns:co.v2="urn:schemas-microsoft-com:clickonce.v2"  
  xmlns="urn:schemas-microsoft-com:asm.v2"  
  xmlns:asmv1="urn:schemas-microsoft-com:asm.v1"  
  xmlns:asmv2="urn:schemas-microsoft-com:asm.v2"  
  xmlns:xrml="urn:mpeg:mpeg21:2003:01-REL-R-NS"  
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
```  
  
## <a name="see-also"></a>请参阅  
 [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)   
 [\<程序集 > 元素](../deployment/assembly-element-clickonce-application.md)