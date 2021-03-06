---
title: IDebugExceptionEvent2::CanPassToDebuggee |Microsoft 文档
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugExceptionEvent2::CanPassToDebuggee
helpviewer_keywords:
- IDebugExceptionEvent2::CanPassToDebuggee
ms.assetid: ae4bbe0a-fbe1-49be-a310-ea64279a434b
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: f0ffea7be736cbf6d04c368ba6124d0faf22be61
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="idebugexceptionevent2canpasstodebuggee"></a>IDebugExceptionEvent2::CanPassToDebuggee
确定的调试引擎 (DE) 支持将此异常传递给执行恢复时被调试的程序的选项。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT CanPassToDebuggee(  
   void  
);  
```  
  
```csharp  
int CanPassToDebuggee();  
```  
  
## <a name="return-value"></a>返回值  
 返回`S_OK`（此异常可以传递到该程序） 或`S_FALSE`（该异常无法传递上）。  
  
## <a name="remarks"></a>备注  
 DE 必须具有传递给调试对象的默认操作。 IDE 可能会收到[IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)事件并调用[继续](../../../extensibility/debugger/reference/idebugprocess3-continue.md)方法而不调用`CanPassToDebuggee`方法。 因此，DE 应具有或不将异常传递对默认大小写。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)   
 [Continue](../../../extensibility/debugger/reference/idebugprocess3-continue.md)