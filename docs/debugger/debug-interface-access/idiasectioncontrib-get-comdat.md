---
title: 'Idiasectioncontrib:: Get_comdat |Microsoft 文档'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_comdat method
ms.assetid: 8bd9be8d-59ee-4698-b055-daba354b8dcc
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 578314d0771d156fe66bdfbf661ffca98844207f
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="idiasectioncontribgetcomdat"></a>IDiaSectionContrib::get_comdat
检索一个标志，指示部分是否 COMDAT 记录。  
  
## <a name="syntax"></a>语法  
  
```C++  
HRESULT get_comdat (   
   BOOL* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 [out]返回`TRUE`如果明 COMDAT 记录; 否则，返回`FALSE`。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`。 返回`S_FALSE`如果不支持此属性。 否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 COMDAT 记录是使封装的函数的链接器可见的通用对象文件格式 (COFF) 记录。  
  
## <a name="see-also"></a>请参阅  
 [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)