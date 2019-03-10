---
title: Filtrar Agregar y quitar elementos con el Control de ListView de Windows Forms mediante el diseñador
ms.date: 03/30/2017
helpviewer_keywords:
- ListView control [Windows Forms], populating
- ListView control [Windows Forms], adding list items
ms.assetid: 217611ee-fd11-4d39-9a54-a37c3e781be1
ms.openlocfilehash: 04fe8b1add938f4e7aaa35e08d9924102c91cb9b
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2019
ms.locfileid: "57721234"
---
# <a name="how-to-add-and-remove-items-with-the-windows-forms-listview-control-using-the-designer"></a>Filtrar Agregar y quitar elementos con el Control de ListView de Windows Forms mediante el diseñador
El proceso de agregar un elemento a un formulario Windows Forms <xref:System.Windows.Forms.ListView> control consta principalmente de especificar el elemento y asignarle propiedades. Agregar o quitar elementos de lista puede realizarse en cualquier momento.  
  
 El procedimiento siguiente requiere una **aplicación Windows** proyecto con un formulario que contenga un <xref:System.Windows.Forms.ListView> control. Para obtener información acerca de cómo configurar un proyecto de este tipo, vea [Cómo: Cree un proyecto de aplicación de Windows Forms](/visualstudio/ide/step-1-create-a-windows-forms-application-project) y [Cómo: Agregar controles a Windows Forms](how-to-add-controls-to-windows-forms.md).  
  
> [!NOTE]
>  Los cuadros de diálogo y comandos de menú que se ven pueden diferir de los descritos en la Ayuda, en función de los valores de configuración o de edición activos. Para cambiar la configuración, elija la opción **Importar y exportar configuraciones** del menú **Herramientas** . Para más información, vea [Personalizar el IDE de Visual Studio](/visualstudio/ide/personalizing-the-visual-studio-ide).  
  
### <a name="to-add-or-remove-items-using-the-designer"></a>Para agregar o quitar elementos mediante el diseñador  
  
1.  Seleccione el control <xref:System.Windows.Forms.ListView>.  
  
2.  En el **propiedades** ventana, haga clic en el **puntos suspensivos** (![de pantalla de VisualStudioEllipsesButton](../media/vbellipsesbutton.png "vbEllipsesButton")) situado junto a el <xref:System.Windows.Forms.ListView.Items%2A> propiedad.  
  
     El **Editor de la colección ListViewItem** aparece.  
  
3.  Para agregar un elemento, haga clic en el **agregar** botón. A continuación, puede establecer las propiedades del nuevo elemento, tales como la <xref:System.Windows.Forms.ListView.Text%2A> y <xref:System.Windows.Forms.ListViewItem.ImageIndex%2A> propiedades.  
  
4.  Para quitar un elemento, selecciónelo y haga clic en el **quitar** botón.  
  
## <a name="see-also"></a>Vea también
- [Información general del control ListView](listview-control-overview-windows-forms.md)
- [Cómo: Agregar columnas al Control de ListView de Windows Forms](how-to-add-columns-to-the-windows-forms-listview-control.md)
- [Cómo: Mostrar subelementos en columnas con el Control ListView de formularios de Windows](how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md)
- [Cómo: Mostrar iconos para el Control ListView de formularios de Windows](how-to-display-icons-for-the-windows-forms-listview-control.md)
- [Cómo: Agregar información personalizada a los controles TreeView o ListView (formularios Windows Forms)](add-custom-information-to-a-treeview-or-listview-control-wf.md)
- [Cómo: Agrupar elementos en un Control ListView de formularios de Windows](how-to-group-items-in-a-windows-forms-listview-control.md)
