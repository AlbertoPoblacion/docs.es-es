---
title: Procedimiento Agregar columnas al Control de ListView de Windows Forms mediante el diseñador
ms.date: 03/30/2017
helpviewer_keywords:
- ListView control [Windows Forms], adding column headers
- columns [Windows Forms], adding to ListView controls
ms.assetid: 5b1a8b4d-587e-479a-95c1-f9b90884f13a
ms.openlocfilehash: b4daea500d8d61dbfbd1557a4fb3ef69a20b5bdc
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/23/2019
ms.locfileid: "54739357"
---
# <a name="how-to-add-columns-to-the-windows-forms-listview-control-using-the-designer"></a>Procedimiento Agregar columnas al Control de ListView de Windows Forms mediante el diseñador
Los formularios de Windows <xref:System.Windows.Forms.ListView> control puede mostrar varias columnas para cada lista de elementos cuando se encuentra en la **detalles** vista. Puede usar las columnas para mostrar varios tipos de información sobre cada elemento de lista. Por ejemplo, una lista de archivos podría mostrar el nombre de archivo, tipo de archivo, tamaño y fecha de que última modificación del archivo. Para obtener información sobre cómo rellenar las columnas una vez que se crean, vea [Cómo: Mostrar subelementos en columnas con el Windows Forms Control ListView](../../../../docs/framework/winforms/controls/how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md).  
  
 El procedimiento siguiente requiere una **aplicación Windows** proyecto con un formulario que contenga un <xref:System.Windows.Forms.ListView> control. Para obtener información acerca de cómo configurar un proyecto de este tipo, vea [Cómo: Cree un proyecto de aplicación Windows](https://msdn.microsoft.com/library/b2f93fed-c635-4705-8d0e-cf079a264efa) y [Cómo: Agregar controles a Windows Forms](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).  
  
> [!NOTE]
>  Los cuadros de diálogo y comandos de menú que se ven pueden diferir de los descritos en la Ayuda, en función de los valores de configuración o de edición activos. Para cambiar la configuración, elija la opción **Importar y exportar configuraciones** del menú **Herramientas** . Para más información, vea [Personalizar el IDE de Visual Studio](/visualstudio/ide/personalizing-the-visual-studio-ide).  
  
### <a name="to-add-columns-in-the-designer"></a>Para agregar columnas en el diseñador  
  
1.  En el **propiedades** ventana, establezca el control <xref:System.Windows.Forms.ListView.View%2A> propiedad <xref:System.Windows.Forms.View.Details>.  
  
2.  En el **propiedades** ventana, haga clic en el **puntos suspensivos** botón (![de pantalla de VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")) junto a el <xref:System.Windows.Forms.ListView.Columns%2A> propiedad.  
  
     El **Editor de la colección ColumnHeader** aparece.  
  
3.  Use la **agregar** para agregar nuevas columnas. A continuación, puede seleccionar el encabezado de columna y establezca su texto (el título de la columna), la alineación del texto y el ancho.  
  
## <a name="see-also"></a>Vea también
- [Información general del control ListView](../../../../docs/framework/winforms/controls/listview-control-overview-windows-forms.md)
- [Cómo: Agregar y quitar elementos con el Control ListView de formularios de Windows](../../../../docs/framework/winforms/controls/how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)
- [Cómo: Mostrar subelementos en columnas con el Control ListView de formularios de Windows](../../../../docs/framework/winforms/controls/how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md)
- [Cómo: Mostrar iconos para el Control ListView de formularios de Windows](../../../../docs/framework/winforms/controls/how-to-display-icons-for-the-windows-forms-listview-control.md)
- [Cómo: Agregar información personalizada a los controles TreeView o ListView (formularios Windows Forms)](../../../../docs/framework/winforms/controls/add-custom-information-to-a-treeview-or-listview-control-wf.md)
