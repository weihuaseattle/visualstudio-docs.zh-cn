---
title: IDebugFunctionObject2::CreateObject |Microsoft 文档
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- IDebugFunctionObject2::CreateObject
- CreateObject
ms.assetid: 148de615-941e-4b64-ab11-75b692aae465
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: c5283d72972e1ba579cafa82648cbf0ec0fcf80c
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="idebugfunctionobject2createobject"></a>IDebugFunctionObject2::CreateObject
创建使用给定评估标志设置和超时值的构造函数的对象。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT CreateObject (  
   IDebugFunctionObject* pConstructor,  
   DWORD                 dwArgs,  
   IDebugObject*         pArgs[],  
   DWORD                 dwEvalFlags,  
   DWORD                 dwTimeout,  
   IDebugObject**        ppObject  
);  
```  
  
```csharp  
int CreateObject (  
   IDebugFunctionObject pConstructor,  
   uint                 dwArgs,  
   IDebugObject[]       pArgs,  
   uint                 dwEvalFlags,  
   uint                 dwTimeout,  
   out IDebugObject**   ppObject  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pConstructor`  
 [in][IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)对象，表示要创建的对象的构造函数。  
  
 `dwArgs`  
 [in]中的参数数目`pArg`数组。 表示传递给构造函数的参数的数目。  
  
 `pArgs`  
 [in]数组[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)表示的参数的对象传递给构造函数。  
  
 `dwEvalFlags`  
 [in]中的标志的组合[EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)指定如何执行计算的枚举。  
  
 `dwTimeout`  
 [in]以毫秒为单位，从此方法返回前等待的最长时间。 使用**无限**无限期等待。  
  
 `ppObject`  
 [out]返回**IDebugObject**表示新创建的对象。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 调用此方法以创建一个对象，表示一个类或其他复杂类型的要求的构造函数的参数的实例。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)