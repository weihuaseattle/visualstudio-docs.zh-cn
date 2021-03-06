---
title: 创建 SharePoint 解决方案包 |Microsoft 文档
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packages
- packages [SharePoint development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 957789c4adfc476429179ed84f87f544c0d37143
ms.sourcegitcommit: 4cd4aef53e7035d23e7d1d0f66f51ac8480622a1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2018
ms.locfileid: "34765266"
---
# <a name="create-sharepoint-solution-packages"></a>创建 SharePoint 解决方案包
  通过使用包设计器，你可以创建和自定义部署包。 例如，你可以添加 SharePoint 项目项和功能，重置 IIS 服务器、 设置功能激活作用域，和识别功能依赖关系。 设计器还会生成一个清单，一个用于描述每个包的 XML 文件。  
  
## <a name="packaging-tools"></a>打包工具
 你可以使用**包设计器**自定义的包并生成清单。 你可以包括多个 SharePoint 项目项、 配置是否应重置，Web 服务器，并将其设置部署服务器类型。 有关详细信息，请参阅[如何： 添加和删除通过使用包设计器的功能和包项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)。  
  
 或者，可以使用**打包资源管理器**要修改的功能和包文件中的项 (*.wsp*)。 有关详细信息，请参阅[如何： 添加和使用打包资源管理器中删除功能和包项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer.md)。  
  
 你可以使用 Visual Studio 和 MSBuild 创建包 (*.wsp*) 要部署 SharePoint 解决方案的文件。 此过程生成所需的 SharePoint 部署的清单文件。 有关详细信息，请参阅[如何： 创建 SharePoint 包](http://msdn.microsoft.com/en-us/b24be45c-e91d-49bb-afb0-7b265404214b)和[如何： 创建 SharePoint 解决方案包使用 MSBuild 任务](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)。  
  
## <a name="package-designer-options"></a>包设计器选项
 下表显示的属性，你可以在 SharePoint 具有自定义**包设计器**。  
  
|包设计器属性|默认设置的说明|  
|-------------------------------|------------------------------------|  
|name|必须的。 包的默认名称设置为*ProjectName*。|  
|重置 web 服务器|可选。 如果你想要重新启动 Web 服务器后的，请选择 *.wsp*文件安装在 SharePoint 服务器上。|  
|部署服务器类型|必须的。 默认情况下，范围设置为应用程序服务器。<br /><br /> 应用程序服务器： 介绍承载服务的服务器。<br /><br /> WebFrontEnd： 介绍承载网站的服务器。|  
|解决方案中的项|所有 SharePoint 项目项和可以添加到包的功能。|  
|包中的项|可选。 所有 SharePoint 项目和你想要部署包中的功能。|  
  
## <a name="configure-the-packaging-process"></a>配置在打包过程
 开发 Visual Studio 中的 SharePoint 解决方案后，你可以自定义项目的打包方式。  
  
 下表显示可用于自定义的两个 MSBuild 目标如何 *.wsp*创建文件。  
  
|目标|描述|  
|------------|-----------------|  
|BeforeLayout|执行任务之前的文件复制到中间目录中的目标。 你可以在创建包文件之前修改的文件 (*.wsp*)。|  
|AfterLayout|文件复制到中间目录后立即执行任务的目标。|  
  
 有关详细信息，[如何： 自定义 SharePoint 解决方案包通过使用 MSBuild 目标](../sharepoint/how-to-customize-a-sharepoint-solution-package-by-using-msbuild-targets.md)。  
  
## <a name="packaging-architecture"></a>打包体系结构
 创建 SharePoint 包时，将执行以下步骤 (*.wsp*) 在 Visual Studio 中。  
  
1.  功能和包进行验证以确保包的物理和语义结构正确。  
  
2.  枚举的功能、 项目项和包中的包文件。 进行转换的包和功能清单文件，以包含部署和激活所需的所有信息。 令牌将替换完全限定的值。  
  
3.  执行可自定义 BeforeLayout MSBuild 目标。 你可以创建此步骤以对进行任何自定义修改的包之前 *.wsp*创建文件。  
  
4.  枚举的文件复制到中间目录中。  
  
5.  执行可自定义的 AfterLayout MSBuild 目标。 你可以创建此步骤以对进行任何自定义修改的包之前 *.wsp*创建文件。  
  
6.  中间目录中的文件添加到 *.wsp*文件。  
  
## <a name="package-folder-structure"></a>包文件夹结构
 当打包你的 SharePoint 项目， *.wsp*文件创建可在*SolutionFolder\bin\{BuildConfiguration}* 文件夹。 例如，如果你的解决方案是在*C:\Visual Studio 2013\Projects\ListDefinition1*和生成配置设置为版本中， *.wsp*文件位于*C:\Visual Studio 2013\Projects\ListDefinition1\bin\Release*。  
  
## <a name="see-also"></a>请参阅
 [如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)  
 [如何： 添加和移除功能和包项使用包设计器](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)   
 [如何： 创建 SharePoint 包](http://msdn.microsoft.com/en-us/b24be45c-e91d-49bb-afb0-7b265404214b)   
 [如何： 使用 MSBuild 任务创建 SharePoint 解决方案包](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)   
 [如何：使用 MSBuild 目标自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package-by-using-msbuild-targets.md)  
  
 