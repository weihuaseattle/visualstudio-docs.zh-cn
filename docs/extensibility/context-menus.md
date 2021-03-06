---
title: 上下文菜单 |Microsoft 文档
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - context menus
ms.assetid: 44fd9e6a-6d42-4aba-80ba-f37fa0070f1d
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: fa957e949127663eca7d4e619919edcc07c7a29b
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="context-menus"></a>上下文菜单
上下文菜单在活动区域的客户端区域中右键单击用户时，会显示，并清除当释放鼠标右键按钮。  
  
## <a name="editor-context-menus"></a>编辑器上下文菜单  
 可通过截获过程`ECMD_SHOWCONTEXTMENU`，语言服务可以控制将在编辑器中显示的上下文菜单。 若要显示您自己的上下文菜单，请先处理此命令，当它传递到你<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowContextMenu%2A>。 如果不处理此命令，则 IDE 将显示为编辑器提供标准的上下文菜单。 你还可以控制基于每个标记的上下文菜单的内容。 有关此的详细信息，请参阅[使用旧版 API 使用文本标记](../extensibility/using-text-markers-with-the-legacy-api.md)和[截获旧语言服务命令](../extensibility/internals/intercepting-legacy-language-service-commands.md)。  
  
## <a name="see-also"></a>另请参阅  
 [开发旧语言服务](../extensibility/internals/developing-a-legacy-language-service.md)   
 [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)