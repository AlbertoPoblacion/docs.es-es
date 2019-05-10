---
title: 'Tutorial: Hospedar contenido Direct3D9 en WPF'
ms.date: 03/30/2017
helpviewer_keywords:
- Direct3D9 [WPF interoperability], hosting Direct3D9 content
- WPF [WPF], hosting Direct3D9 content
ms.assetid: 60983736-0ab5-42cc-8b16-e9fbde261a43
ms.openlocfilehash: cff14f03a75717c657785cb8fe5a1de2077faf86
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2019
ms.locfileid: "64605406"
---
# <a name="walkthrough-hosting-direct3d9-content-in-wpf"></a>Tutorial: Hospedar contenido Direct3D9 en WPF
En este tutorial se muestra cómo hospedar contenido Direct3D9 en una aplicación de Windows Presentation Foundation (WPF).  
  
 En este tutorial, realizará las tareas siguientes:  
  
- Cree un proyecto WPF para hospedar contenido Direct3D9.  
  
- Importar el contenido Direct3D9.  
  
- Mostrar el contenido Direct3D9 mediante la <xref:System.Windows.Interop.D3DImage> clase.  
  
 Cuando termine, sabrá cómo hospedar contenido Direct3D9 en una aplicación WPF.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Necesita los componentes siguientes para completar este tutorial:  
  
- Visual Studio.  
  
- DirectX SDK 9 o posterior.  
  
- Un archivo DLL que contiene contenido Direct3D9 en un formato compatible con WPF. Para obtener más información, consulte [interoperabilidad entre Direct3D9 y WPF](wpf-and-direct3d9-interoperation.md) y [Tutorial: Crear contenido Direct3D9 para hospedarlo en WPF](walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md).  
  
## <a name="creating-the-wpf-project"></a>Crear el proyecto WPF  
 El primer paso es crear el proyecto para la aplicación de WPF.  
  
#### <a name="to-create-the-wpf-project"></a>Para crear el proyecto de WPF  
  
- Cree un nuevo proyecto de aplicación de WPF en Visual C# denominado `D3DHost`. Para obtener más información, vea [Tutorial: Mi primera aplicación de escritorio de WPF](../getting-started/walkthrough-my-first-wpf-desktop-application.md).  
  
     MainWindow.xaml se abre en el [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)].  
  
## <a name="importing-the-direct3d9-content"></a>Importar el contenido Direct3D9  
 Importar el contenido Direct3D9 desde una DLL no administrada mediante el `DllImport` atributo.  
  
#### <a name="to-import-direct3d9-content"></a>Para importar contenido Direct3D9  
  
1. Abra MainWindow.xaml.cs en el Editor de código.  
  
2. Reemplace el código generado automáticamente por el código siguiente.  
  
     [!code-csharp[System.Windows.Interop.D3DImage#1](~/samples/snippets/csharp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/CS/window1.xaml.cs#1)]  
  
## <a name="hosting-the-direct3d9-content"></a>Hospedar contenido Direct3D9  
 Por último, use la <xref:System.Windows.Interop.D3DImage> clase para hospedar contenido Direct3D9.  
  
#### <a name="to-host-the-direct3d9-content"></a>Para hospedar contenido Direct3D9  
  
1. En MainWindow.xaml, reemplace el XAML generado automáticamente por el XAML siguiente.  
  
     [!code-xaml[System.Windows.Interop.D3DImage#10](~/samples/snippets/csharp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/CS/window1.xaml#10)]  
  
2. Compile el proyecto.  
  
3. Copie el archivo DLL que contiene el contenido Direct3D9 en la carpeta bin/Debug.  
  
4. Presione F5 para ejecutar el proyecto.  
  
     El contenido Direct3D9 aparece dentro de la aplicación de WPF.  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Interop.D3DImage>
- [Consideraciones de rendimiento para la interoperabilidad entre Direct3D9 y WPF](performance-considerations-for-direct3d9-and-wpf-interoperability.md)
