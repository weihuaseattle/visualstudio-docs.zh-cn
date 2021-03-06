---
title: IDebugManagedObject |Microsoft 文档
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugManagedObject
helpviewer_keywords:
- IDebugManagedObject interface
ms.assetid: 3ae09d34-112c-4285-80ee-9f7f8dc414d7
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: a7127d2583093ae06b52712cc6aacb0ea1adffc8
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="idebugmanagedobject"></a>IDebugManagedObject
> [!IMPORTANT]
>  在 Visual Studio 2015 中，已弃用这种方式实施表达式计算器。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 此接口允许表达式计算器 (EE) 值类实例调用属性或方法 (例如， `System.Decimal`) 并设置其值而不调用[评估](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)上被调试的程序。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugManagedObject : IDebugObject  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 表达式计算器实现此接口来表示一个托管的代码对象，如变量。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 若要获取此接口，调用[GetManagedDebugObject](../../../extensibility/debugger/reference/idebugobject-getmanageddebugobject.md)上[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)表示值类的实例。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 除了从继承的方法[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)、`IDebugManagedObject`接口公开以下方法。  
  
|方法|描述|  
|------------|-----------------|  
|[GetManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject-getmanagedobject.md)|返回表示托管的代码对象，可以从哪些任何适当的托管代码获取接口的接口。|  
|[SetFromManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject-setfrommanagedobject.md)|将此对象的值设置为指定的托管的代码对象的值。|  
  
## <a name="remarks"></a>备注  
 表达式计算器使用此接口以将托管的代码对象存储在分析树。  
  
## <a name="requirements"></a>要求  
 标头： ee.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [表达式评估接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [评估](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)