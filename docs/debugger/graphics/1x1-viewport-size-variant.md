---
title: 1x1 视口大小变量 |Microsoft 文档
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 3dbc3247-00f5-4644-8ff9-72e9febcf09a
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0c2f97793c838316d252aa56dcadd9fbb045decf
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="1x1-viewport-size-variant"></a>1x1 视口大小变量
将所有呈现器目标上的视口尺寸缩小为 1x1 像素。  
  
## <a name="interpretation"></a>解释  
 较小的视口会减少必须着色的像素数，但是不会减少必须处理的顶点数。 将视口尺寸设置为 1x1 像素可有效地消除应用中的像素着色。  
  
 如果此变体显示较大的性能提升，则可能表示你的应用使用了太多填充率。 这可能表示你已经选择的分辨率对于目标平台而言太高，或者你的应用花费了大量时间来为之后覆盖（过度绘制）的像素着色。 结果表明，减小帧缓冲区的大小或减少过度绘制量将提升应用的性能。  
  
## <a name="remarks"></a>备注  
 在每次调用 `ID3D11DeviceContext::OMSetRenderTargets` 或 `ID3D11DeviceContext::RSSetViewports` 之后，视口尺寸将重置为 1x1 像素。  
  
## <a name="example"></a>示例  
 通过使用如下代码，可重现此变体：  
  
```  
D3D11_VIEWPORT viewport;  
viewport.TopLeftX = 0;  
viewport.TopLeftY = 0;  
viewport.Width = 1;  
viewport.Height = 1;  
d3d_context->RSSetViewports(1, &viewport);  
```