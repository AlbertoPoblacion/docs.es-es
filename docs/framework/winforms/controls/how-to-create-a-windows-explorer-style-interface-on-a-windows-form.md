---
title: Filtrar para crear una interfaz similar a la del Explorador de Windows en formularios Windows Forms
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Explorer [Windows Forms], creating with Windows Forms
- SplitContainer control [Windows Forms], Explorer-style interface
- forms [Windows Forms], Windows Explorer type
ms.assetid: 9a3d5f4f-5dda-4350-9ad5-57ce5976dc47
ms.openlocfilehash: e559702d5fd7f0f56c7b2b010713e3129504746a
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59192139"
---
# <a name="how-to-create-a-windows-explorerstyle-interface-on-a-windows-form"></a>Filtrar para crear una interfaz similar a la del Explorador de Windows en formularios Windows Forms
El Explorador de Windows es una opción de interfaz de usuario común para las aplicaciones debido a su familiaridad inmediata.  
  
 El Explorador de Windows es básicamente un <xref:System.Windows.Forms.TreeView> control y un <xref:System.Windows.Forms.ListView> control en paneles independientes. Los paneles se realizan puede cambiar el tamaño por un divisor. Esta organización de los controles es muy eficaz para mostrar y explorar información.  
  
 Los pasos siguientes muestran cómo organizar controles en un formulario similar al explorador de Windows. No se muestra cómo agregar la funcionalidad de exploración de archivos de la aplicación Explorador de Windows.  
  
> [!NOTE]
>  Los cuadros de diálogo y comandos de menú que se ven pueden diferir de los descritos en la Ayuda, en función de los valores de configuración o de edición activos. Para cambiar la configuración, elija la opción **Importar y exportar configuraciones** del menú **Herramientas** . Para más información, vea [Personalizar el IDE de Visual Studio](/visualstudio/ide/personalizing-the-visual-studio-ide).  
  
### <a name="to-create-a-windows-explorer-style-windows-form"></a>Para crear un formulario de Windows de estilo Explorador de Windows  
  
1.  Cree un nuevo proyecto de aplicación de Windows (**archivo** > **New** > **proyecto** > **Visual C#** o **Visual Basic** > **escritorio clásico de** > **aplicación de Windows Forms**).  
  
2.  Desde el **cuadro de herramientas**:  
  
    1.  Arrastre un <xref:System.Windows.Forms.SplitContainer> control al formulario.  
  
    2.  Arrastre un <xref:System.Windows.Forms.TreeView> controlar en **SplitterPanel1** (el panel de la <xref:System.Windows.Forms.SplitContainer> control marcado **Panel1**).  
  
    3.  Arrastre un <xref:System.Windows.Forms.ListView> controlar en **SplitterPanel2** (el panel de la <xref:System.Windows.Forms.SplitContainer> control marcado **Panel2**).  
  
3.  Presione la tecla CTRL y haciendo clic a su vez, seleccione los tres controles. Cuando se selecciona el <xref:System.Windows.Forms.SplitContainer> de control, haga clic en la barra de división, en lugar de los paneles.  
  
    > [!NOTE]
    >  No utilice el **seleccionar todo** comando el **editar** menú. Si lo hace, la propiedad necesaria en el paso siguiente no aparecerá en el **propiedades** ventana.  
  
4.  En la ventana **Propiedades** , establezca la propiedad <xref:System.Windows.Forms.SplitContainer.Dock%2A> en <xref:System.Windows.Forms.DockStyle.Fill>.  
  
5.  Presione F5 para ejecutar la aplicación.  
  
     El formulario muestra una interfaz de usuario de dos partes, similar a la del explorador de Windows.  
  
    > [!NOTE]
    >  Al arrastrar el divisor, los paneles cambian de tamaño.  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Forms.SplitContainer>
- [Filtrar para crear una interfaz de usuario de varios paneles con formularios Windows Forms](how-to-create-a-multipane-user-interface-with-windows-forms.md)
- [Filtrar para definir el comportamiento de cambio de tamaño y colocación de una ventana dividida](how-to-define-resize-and-positioning-behavior-in-a-split-window.md)
- [Filtrar para dividir una ventana horizontalmente](how-to-split-a-window-horizontally.md)
- [Control SplitContainer](splitcontainer-control-windows-forms.md)
