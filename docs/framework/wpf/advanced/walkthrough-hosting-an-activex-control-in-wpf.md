---
title: 'Tutorial: Hospedar un control ActiveX en WPF'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ActiveX controls [WPF interoperability]
- hosting ActiveX controls [WPF]
ms.assetid: 1931d292-0dd1-434f-963c-dcda7638d75a
ms.openlocfilehash: c27449da5ee0351e472eaba7d930a774979db65f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61781386"
---
# <a name="walkthrough-hosting-an-activex-control-in-wpf"></a>Tutorial: Hospedar un control ActiveX en WPF
Para habilitar la interacción mejorada con los exploradores, puede usar [!INCLUDE[TLA#tla_actx](../../../../includes/tlasharptla-actx-md.md)] controles en su [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-aplicación basada en. Este tutorial muestra cómo puede hospedar el [!INCLUDE[TLA#tla_wmp](../../../../includes/tlasharptla-wmp-md.md)] como un control en un [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] página.

 Las tareas ilustradas en este tutorial incluyen:

- Crear el proyecto.

- Crear el control ActiveX.

- Hospedar el control ActiveX en una página de WPF.

 Cuando haya completado este tutorial, comprenderá cómo usar [!INCLUDE[TLA#tla_actx](../../../../includes/tlasharptla-actx-md.md)] controles en su [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-aplicación basada en.

## <a name="prerequisites"></a>Requisitos previos
 Necesita los componentes siguientes para completar este tutorial:

- [!INCLUDE[TLA#tla_wmp](../../../../includes/tlasharptla-wmp-md.md)] instalado en el equipo donde está instalado Visual Studio.

- Visual Studio 2010.

## <a name="creating-the-project"></a>Crear el proyecto

#### <a name="to-create-and-set-up-the-project"></a>Para crear y configurar el proyecto

1. Cree un proyecto de aplicación WPF denominado `HostingAxInWpf`.

2. Agregar un proyecto de biblioteca de controles de Windows Forms a la solución y denomine al proyecto `WmpAxLib`.

3. En el proyecto WmpAxLib, agregue una referencia al ensamblado de Windows Media Player, que se denomina wmp.dll.

4. Abra el **cuadro de herramientas**.

5. Haga clic en el **cuadro de herramientas**y, a continuación, haga clic en **elegir elementos**.

6. Haga clic en el **componentes COM** ficha, seleccione el **Windows Media Player** controlar y, a continuación, haga clic en **Aceptar**.

     El control de Windows Media Player se agrega a la **cuadro de herramientas**.

7. En el Explorador de soluciones, haga clic en el **UserControl1** de archivo y, a continuación, haga clic en **cambiar el nombre**.

8. Cambie el nombre a `WmpAxControl.vb` o `WmpAxControl.cs`, según el lenguaje.

9. Si se le solicite cambiar el nombre de todas las referencias, haga clic en **Sí**.

## <a name="creating-the-activex-control"></a>Crear el Control ActiveX
 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] genera automáticamente un <xref:System.Windows.Forms.AxHost> clase contenedora para un [!INCLUDE[TLA#tla_actx](../../../../includes/tlasharptla-actx-md.md)] controlar cuando el control se agrega a una superficie de diseño. El procedimiento siguiente crea un ensamblado administrado denominado AxInterop.WMPLib.dll.

#### <a name="to-create-the-activex-control"></a>Para crear el control ActiveX

1. Abra WmpAxControl.vb o WmpAxControl.cs en el Diseñador de Windows Forms.

2. Desde el **cuadro de herramientas**, agregar el control de Windows Media Player a la superficie de diseño.

3. En la ventana Propiedades, establezca el valor del control de Windows Media Player <xref:System.Windows.Forms.Control.Dock%2A> propiedad <xref:System.Windows.Forms.DockStyle.Fill>.

4. Compile el proyecto de biblioteca de control WmpAxLib.

## <a name="hosting-the-activex-control-on-a-wpf-page"></a>Hospedar el Control ActiveX en una página de WPF

#### <a name="to-host-the-activex-control"></a>Para hospedar el control ActiveX

1. En el proyecto HostingAxInWpf, agregue una referencia a generado [!INCLUDE[TLA2#tla_actx](../../../../includes/tla2sharptla-actx-md.md)] ensamblado de interoperabilidad.

     Este ensamblado se denomina AxInterop.WMPLib.dll y se agregó a la carpeta Debug del proyecto WmpAxLib al importar el control de Windows Media Player.

2. Agregue una referencia al ensamblado WindowsFormsIntegration, denominado WindowsFormsIntegration.dll.

3. Agregue una referencia a la [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ensamblado, que se denomina System.Windows.Forms.dll.

4. Abra MainWindow.xaml en el diseñador WPF.

5. Nombre de la <xref:System.Windows.Controls.Grid> elemento `grid1`.

     [!code-xaml[HostingAxInWpf#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingAxInWpf/CSharp/HostingAxInWpf/window1.xaml#1)]

6. En la vista Diseño o la vista XAML, seleccione el <xref:System.Windows.Window> elemento.

7. En la ventana Propiedades, haga clic en el **eventos** ficha.

8. Haga doble clic en el <xref:System.Windows.FrameworkElement.Loaded> eventos.

9. Inserte el código siguiente para controlar el <xref:System.Windows.FrameworkElement.Loaded> eventos.

     Este código crea una instancia de la <xref:System.Windows.Forms.Integration.WindowsFormsHost> controlar y agrega una instancia de la `AxWindowsMediaPlayer` control como su elemento secundario.

     [!code-csharp[HostingAxInWpf#11](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingAxInWpf/CSharp/HostingAxInWpf/window1.xaml.cs#11)]
     [!code-vb[HostingAxInWpf#11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HostingAxInWpf/VisualBasic/HostingAxInWpf/window1.xaml.vb#11)]  
  
10. Presione F5 para compilar y ejecutar la aplicación.  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [Diseño de XAML en Visual Studio](/visualstudio/designers/designing-xaml-in-visual-studio)
- [Tutorial: Hospedar un Control compuesto de Windows Forms en WPF](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)
- [Tutorial: Hospedar un Control compuesto de WPF en Windows Forms](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)
