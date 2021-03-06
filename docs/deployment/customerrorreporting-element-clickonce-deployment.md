---
title: '&lt;customErrorReporting&gt;元素 （ClickOnce 部署） |Microsoft 文档'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <customErrorReporting> element [ClickOnce deployment manifest]
ms.assetid: 7d31816e-c692-46b5-9cc9-753284b3bcda
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 41ade854a37127443735e1c197c080aad3d5bd93
ms.sourcegitcommit: 42ea834b446ac65c679fa1043f853bea5f1c9c95
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
---
# <a name="ltcustomerrorreportinggt-element-clickonce-deployment"></a>&lt;customErrorReporting&gt;元素 （ClickOnce 部署）
指定发生错误时所显示的 URI。  
  
## <a name="syntax"></a>语法  
  
```  
<customErrorReporting  
   uri  
/>  
```  
  
## <a name="remarks"></a>备注  
 此元素为可选元素。 否则，[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]显示错误对话框显示异常堆栈。 如果`customErrorReporting`元素是否存在、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]将改为显示由 URI`uri`参数。 目标 URI 将包括外部异常类、 内部异常类和内部异常消息作为参数。  
  
 使用此元素添加到你的应用程序报告功能的错误。 由于生成的 URI 包含有关错误类型的信息，可以分析您的网站，该信息和显示，例如，相应的故障排除屏幕。  
  
## <a name="example"></a>示例  
 下面的代码段演示`customErrorReporting`元素，以及生成可能会产生的 URI。  
  
```  
<customErrorReporting uri=http://www.contoso.com/applications/error.asp />  
  
Example Generated Error:  
http://www.contoso.com/applications/error.asp? outer=System.Deployment.Application.InvalidDeploymentException&&inner=System.Deployment.Application.InvalidDeploymentException&&msg=The%20application%20manifest%20is%20signed,%20but%20the%20deployment%20manifest%20is%20unsigned.%20Both%20manifests%20must%20be%20either%20signed%20or%20unsigned.  
```  
  
## <a name="see-also"></a>请参阅  
 [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)