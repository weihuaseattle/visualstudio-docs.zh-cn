---
title: Dia2dump 示例 |Microsoft 文档
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- sample applications [DIA SDK]
- Dia2dump sample [DIA SDK]
ms.assetid: 492c0893-7043-452f-a020-890a47230d20
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 5559d1ac2a03eaeb1dca57531cd2f19831851d3b
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="dia2dump-sample"></a>Dia2dump 示例
Dia2dump 示例随 Visual Studio 安装，并包含 Dia2dump.cpp 源文件。 已编译可执行文件从命令行中运行，并且显示整个程序数据库 (.pdb) 文件的内容。  
  
### <a name="to-install-the-sample"></a>若要安装示例  
  
1.  验证你的系统满足所有 Visual Studio 安装程序起始页中所述的安装程序要求。  
  
2.  安装 Visual Studio，然后按照文中的示例的所有设置和安装说明。  
  
#### <a name="to-build-the-sample"></a>生成示例  
  
1.  在 Visual Studio 中打开 Dia2dump.sln 文件。 （如有必要，Visual Studio 将首先帮助你升级 Dia2dump 项目。）  
  
2.  在项目属性页中，在**C/c + +** &#124; **常规** &#124; **附加包含目录**属性，指定`..\DIA SDK\include`目录。 这可保证编译器可以找到 dia2.h 文件。  
  
3.  上**生成**菜单上，单击**重新生成解决方案**。  
  
4.  关闭 Visual Studio。  
  
#### <a name="to-run-the-sample"></a>运行示例  
  
1.  打开命令提示符并键入以下命令：  
  
    ```  
    dia2dump filename  
    ```  
  
## <a name="see-also"></a>请参阅  
 [Dia2dump.cpp 源文件](../../debugger/debug-interface-access/dia2dump-cpp-source-file.md)   
 [移植、迁移和升级 Visual Studio 项目](../../porting/port-migrate-and-upgrade-visual-studio-projects.md)