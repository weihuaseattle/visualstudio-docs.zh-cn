---
title: 演练： 使用快捷键编辑器扩展名 |Microsoft 文档
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - link keystrokes to commands
ms.assetid: cf6cc6c6-5a65-4f90-8f14-663decf74672
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: f8f8a310832f0691b4bc4056baddeb1fbbad78f8
ms.sourcegitcommit: fe5a72bc4c291500f0bf4d6e0778107eb8c905f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2018
---
# <a name="walkthrough-using-a-shortcut-key-with-an-editor-extension"></a>演练： 使用快捷键编辑器扩展名
您可以在你的编辑器扩展响应快捷键。 下面的演练演示如何将视图修饰添加到文本视图中，通过使用快捷方式的键。 本演练基于视区修饰编辑器模板，并且它使你使用添加修饰 + 字符。  
  
## <a name="prerequisites"></a>系统必备  
 从 Visual Studio 2015 开始，你并不安装 Visual Studio SDK 从下载中心。 它将包括作为 Visual Studio 安装程序中的可选功能。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
## <a name="creating-a-managed-extensibility-framework-mef-project"></a>创建 Managed Extensibility Framework (MEF) 项目  
  
1.  创建 C# VSIX 项目。 (在**新项目**对话框中，选择**Visual C# / 可扩展性**，然后**VSIX 项目**。)将解决方案命名`KeyBindingTest`。  
  
2.  向项目添加编辑器文本修饰项模板并将其命名`KeyBindingTest`。 有关详细信息，请参阅[带有编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。  
  
3.  添加以下引用和设置**CopyLocal**到`false`:  
  
     Microsoft.VisualStudio.Editor  
  
     Microsoft.VisualStudio.OLE.Interop  
  
     Microsoft.visualstudio.shell.14.0 的引用  
  
     Microsoft.VisualStudio.TextManager.Interop  
  
 在 KeyBindingTest 类文件中，将类名更改为 PurpleCornerBox。 使用的左边距中显示的电灯泡进行其他相应的更改。 在构造函数中，更改从修饰层的名称**KeyBindingTest**到**PurpleCornerBox**:  
  
```csharp  
this.layer = view.GetAdornmentLayer("PurpleCornerBox");  
```  

在 KeyBindingTestTextViewCreationListener.cs 类文件中，更改的名称从 AdornmentLayer **KeyBindingTest**到**PurpleCornerBox**:
  
    ```csharp  
    [Export(typeof(AdornmentLayerDefinition))]  
    [Name("PurpleCornerBox")]  
    [Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]  
    public AdornmentLayerDefinition editorAdornmentLayer;  
    ```  

## <a name="handling-typechar-command"></a>处理 TYPECHAR 命令
在 Visual Studio 2017 版本 15.6 以处理命令的编辑器扩展中的唯一方法实现之前<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>基于命令筛选器。 Visual Studio 2017 15.6 版引入了基于编辑器命令处理程序的现代简化的方法。 接下来的两部分演示如何处理采用同时旧和现代方法的命令。

## <a name="defining-the-command-filter-prior-to-visual-studio-2017-version-156"></a>定义命令筛选器 （之前 Visual Studio 2017 版本 15.6)

 命令筛选器是实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>，可通过实例化修饰处理该命令。  
  
1.  添加一个类文件并将其命名`KeyBindingCommandFilter`。  
  
2.  添加下面的 using 语句。  
  
    ```csharp  
    using System;  
    using System.Runtime.InteropServices;  
    using Microsoft.VisualStudio.OLE.Interop;  
    using Microsoft.VisualStudio;  
    using Microsoft.VisualStudio.Text.Editor;  
  
    ```  
  
3.  名为 KeyBindingCommandFilter 的类应从继承<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>。  
  
    ```csharp  
    internal class KeyBindingCommandFilter : IOleCommandTarget  
    ```  
  
4.  添加为文本视图的私有字段下, 一个命令中的命令链和一个标志，用于表示是否已添加的命令筛选器。  
  
    ```csharp  
    private IWpfTextView m_textView;  
    internal IOleCommandTarget m_nextTarget;  
    internal bool m_added;  
    internal bool m_adorned;  
    ```  
  
5.  添加设置文本视图的构造函数。  
  
    ```csharp  
    public KeyBindingCommandFilter(IWpfTextView textView)  
    {  
        m_textView = textView;  
        m_adorned = false;  
    }  
    ```  
  
6.  实现`QueryStatus()`方法，如下所示。  
  
    ```csharp  
    int IOleCommandTarget.QueryStatus(ref Guid pguidCmdGroup, uint cCmds, OLECMD[] prgCmds, IntPtr pCmdText)  
    {  
        return m_nextTarget.QueryStatus(ref pguidCmdGroup, cCmds, prgCmds, pCmdText);  
    }  
    ```  
  
7.  实现`Exec()`方法，以便它将一个紫色框添加到视图如果 + 类型字符。  
  
    ```csharp  
    int IOleCommandTarget.Exec(ref Guid pguidCmdGroup, uint nCmdID, uint nCmdexecopt, IntPtr pvaIn, IntPtr pvaOut)  
    {  
        if (m_adorned == false)  
        {  
            char typedChar = char.MinValue;  
  
            if (pguidCmdGroup == VSConstants.VSStd2K && nCmdID == (uint)VSConstants.VSStd2KCmdID.TYPECHAR)  
            {  
                typedChar = (char)(ushort)Marshal.GetObjectForNativeVariant(pvaIn);  
                if (typedChar.Equals('+'))  
                {  
                    new PurpleCornerBox(m_textView);  
                    m_adorned = true;  
                }  
            }  
        }  
        return m_nextTarget.Exec(ref pguidCmdGroup, nCmdID, nCmdexecopt, pvaIn, pvaOut);  
    }  
  
    ```  
  
## <a name="adding-the-command-filter-prior-to-visual-studio-2017-version-156"></a>添加 （之前 Visual Studio 2017 版本 15.6) 命令筛选器
 修饰提供程序必须将命令筛选器添加到文本视图。 在此示例中，提供程序实现<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>来侦听文本视图创建事件。 此修饰提供程序还将导出修饰层，它定义的修饰的 Z 顺序。  
  
1.  在 KeyBindingTestTextViewCreationListener 文件中，添加以下 using 语句：  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.ComponentModel.Composition;  
    using Microsoft.VisualStudio;  
    using Microsoft.VisualStudio.OLE.Interop;  
    using Microsoft.VisualStudio.Utilities;  
    using Microsoft.VisualStudio.Editor;  
    using Microsoft.VisualStudio.Text.Editor;  
    using Microsoft.VisualStudio.TextManager.Interop;  
  
    ```  
  
2.  若要获取文本视图适配器，必须导入<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>。  
  
    ```csharp  
    [Import(typeof(IVsEditorAdaptersFactoryService))]  
    internal IVsEditorAdaptersFactoryService editorFactory = null;  
  
    ```  
  
3.  更改<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A>方法，以便它将添加`KeyBindingCommandFilter`。  
  
    ```csharp  
    public void TextViewCreated(IWpfTextView textView)  
    {  
        AddCommandFilter(textView, new KeyBindingCommandFilter(textView));  
    }  
    ```  
  
4.  `AddCommandFilter`处理程序获取文本视图适配器，并添加命令筛选器。  
  
    ```csharp  
    void AddCommandFilter(IWpfTextView textView, KeyBindingCommandFilter commandFilter)  
    {  
        if (commandFilter.m_added == false)  
        {  
            //get the view adapter from the editor factory  
            IOleCommandTarget next;   
            IVsTextView view = editorFactory.GetViewAdapter(textView);  
  
            int hr = view.AddCommandFilter(commandFilter, out next);  
  
            if (hr == VSConstants.S_OK)  
            {      
                commandFilter.m_added = true;  
                 //you'll need the next target for Exec and QueryStatus   
                if (next != null)  
                commandFilter.m_nextTarget = next;  
            }  
        }  
    }  
    ```  

## <a name="implement-a-command-handler-starting-in-visual-studio-2017-version-156"></a>实现 （从 Visual Studio 2017 15.6 版开始） 是命令处理程序

首先，更新项目的 Nuget 引用以引用最新的编辑器 API:

1. 右键单击项目并选择**管理 Nuget 包**。

2. 在**Nuget 包管理器**，选择**更新**选项卡上，选择**选择所有包**复选框，然后选择**更新**。

该命令处理程序的实现<xref:Microsoft.VisualStudio.Commanding.ICommandHandler%601>，可通过实例化修饰处理该命令。  
  
1.  添加一个类文件并将其命名`KeyBindingCommandHandler`。  
  
2.  添加下面的 using 语句。  
  
    ```csharp  
    using Microsoft.VisualStudio.Commanding;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Text.Editor.Commanding.Commands;
    using Microsoft.VisualStudio.Utilities;
    using System.ComponentModel.Composition;   
    ```  
  
3.  名为 KeyBindingCommandHandler 的类应从继承`ICommandHandler<TypeCharCommandArgs>`，并将其作为导出<xref:Microsoft.VisualStudio.Commanding.ICommandHandler>:
  
    ```csharp  
    [Export(typeof(ICommandHandler))]
    [ContentType("text")]
    [Name("KeyBindingTest")]
    internal class KeyBindingCommandHandler : ICommandHandler<TypeCharCommandArgs>  
    ```  
  
4.  添加的命令处理程序的显示名称：  
  
    ```csharp  
    public string DisplayName => "KeyBindingTest";
    ```  
    
5.  实现`GetCommandState()`方法，如下所示。 因为此命令处理程序处理核心编辑器 TYPECHAR 命令，它可以将委托启用到核心编辑器命令。
  
    ```csharp  
    public CommandState GetCommandState(TypeCharCommandArgs args)
    {
        return CommandState.Unspecified;
    } 
    ```  
  
6.  实现`ExecuteCommand()`方法，以便它将一个紫色框添加到视图如果 + 类型字符。 
  
    ```csharp  
    public bool ExecuteCommand(TypeCharCommandArgs args, CommandExecutionContext executionContext)
    {
        if (args.TypedChar == '+')
        {
            bool alreadyAdorned = args.TextView.Properties.TryGetProperty(
                "KeyBindingTextAdorned", out bool adorned) && adorned;
            if (!alreadyAdorned)
            {
                new PurpleCornerBox((IWpfTextView)args.TextView);
                args.TextView.Properties.AddProperty("KeyBindingTextAdorned", true);
            }
        }

        return false;
    }
    ```  
 7. 将修饰层定义从 KeyBindingTestTextViewCreationListener.cs 文件复制到 KeyBindingCommandHandler.cs，然后删除 KeyBindingTestTextViewCreationListener.cs 文件：
 
    ```csharp  
    /// <summary>
    /// Defines the adornment layer for the adornment. This layer is ordered
    /// after the selection layer in the Z-order.
    /// </summary>
    [Export(typeof(AdornmentLayerDefinition))]
    [Name("PurpleCornerBox")]
    [Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]
    private AdornmentLayerDefinition editorAdornmentLayer;    
    ```  

## <a name="making-the-adornment-appear-on-every-line"></a>进行修饰出现在每个行中  

原始修饰出现在每个字符 'a' 在文本文件中。 现在，我们已更改用于修饰添加到 + 字符的响应中的代码，它将修饰添加仅在行上，+ 类型化。 我们可以更改修饰代码，以便修饰一次将出现在每个 a。  
  
在 KeyBindingTest.cs 文件中，更改要循环访问修饰 a 字符的视图中的所有行的 CreateVisuals() 方法。  
  
```csharp  
private void CreateVisuals(ITextViewLine line)  
{  
    IWpfTextViewLineCollection textViewLines = this.view.TextViewLines;  
  
    foreach (ITextViewLine textViewLine in textViewLines)  
    {  
        if (textViewLine.ToString().Contains("a"))  
        {  
            // Loop through each character, and place a box around any 'a'   
            for (int charIndex = textViewLine.Start; charIndex < textViewLine.End; charIndex++)  
            {  
                if (this.view.TextSnapshot[charIndex] == 'a')  
                {  
                    SnapshotSpan span = new SnapshotSpan(this.view.TextSnapshot, Span.FromBounds(charIndex, charIndex + 1));  
                    Geometry geometry = textViewLines.GetMarkerGeometry(span);  
                    if (geometry != null)  
                    {  
                        var drawing = new GeometryDrawing(this.brush, this.pen, geometry);  
                        drawing.Freeze();  
  
                        var drawingImage = new DrawingImage(drawing);  
                        drawingImage.Freeze();  
  
                        var image = new Image  
                        {  
                            Source = drawingImage,  
                        };  
  
                        // Align the image with the top of the bounds of the text geometry  
                        Canvas.SetLeft(image, geometry.Bounds.Left);  
                        Canvas.SetTop(image, geometry.Bounds.Top);  
  
                        this.layer.AddAdornment(AdornmentPositioningBehavior.TextRelative, span, null, image, null);  
                    }  
                }  
            }  
        }  
    }  
}  
```  
  
## <a name="building-and-testing-the-code"></a>生成和测试代码  
  
1.  生成 KeyBindingTest 解决方案并在实验实例中运行它。  
  
2.  创建或打开一个文本文件。 键入包含字符某些字词 a，然后键入 + 文本视图中的任意位置。  
  
     紫色正方形应显示在文件中的每个 a 字符。
