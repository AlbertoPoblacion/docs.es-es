---
title: Filtrar Agregar y quitar elementos de menú con el componente ContextMenu de formularios Windows Forms
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- context menus [Windows Forms], removing items
- ContextMenu component [Windows Forms], adding items
- shortcut menus [Windows Forms], removing items
- shortcut menus [Windows Forms], examples
- context menus [Windows Forms], adding items
- shortcut menus [Windows Forms], adding items
- ContextMenu component [Windows Forms], removing items
- context menus [Windows Forms], examples
- examples [Windows Forms], context menus
ms.assetid: 426d1eaf-7fb8-4b0b-8a33-5e8721786ea4
ms.openlocfilehash: 8b63182bdb37e47a71bee2d22500263cd4889ac9
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2019
ms.locfileid: "57725069"
---
# <a name="how-to-add-and-remove-menu-items-with-the-windows-forms-contextmenu-component"></a>Filtrar Agregar y quitar elementos de menú con el componente ContextMenu de formularios Windows Forms
Explica cómo agregar y quitar elementos del menú contextual en Windows Forms.  
  
 Los formularios de Windows <xref:System.Windows.Forms.ContextMenu> componente proporciona un menú de comandos usados frecuentemente que son relevantes para el objeto seleccionado. Puede agregar elementos al menú contextual mediante la adición de <xref:System.Windows.Forms.MenuItem> objetos a la <xref:System.Windows.Forms.Menu.MenuItems%2A> colección.  
  
 Se pueden quitar elementos de un menú contextual de forma permanente; Sin embargo, en tiempo de ejecución puede ser más adecuado ocultar o deshabilitar los elementos en su lugar.  
  
> [!IMPORTANT]
>  Aunque <xref:System.Windows.Forms.MenuStrip> y <xref:System.Windows.Forms.ContextMenuStrip> reemplazan y agregan funcionalidad a la <xref:System.Windows.Forms.MainMenu> y <xref:System.Windows.Forms.ContextMenu> controles de versiones anteriores, <xref:System.Windows.Forms.MainMenu> y <xref:System.Windows.Forms.ContextMenu> se conservan para compatibilidad con versiones anteriores y uso futuro, si elige.  
  
### <a name="to-remove-items-from-a-shortcut-menu"></a>Para quitar elementos de un menú contextual  
  
1.  Use la <xref:System.Windows.Forms.Menu.MenuItemCollection.Remove%2A> o <xref:System.Windows.Forms.Menu.MenuItemCollection.RemoveAt%2A> método de la <xref:System.Windows.Forms.Menu.MenuItems%2A> colección de los <xref:System.Windows.Forms.ContextMenu> componente para quitar un elemento de menú concreto.  
  
    ```vb  
    ' Removes the first item in the shortcut menu.  
    ContextMenu1.MenuItems.RemoveAt(0)  
    ' Removes a particular object from the shortcut menu.  
    ContextMenu1.MenuItems.Remove(mnuItemNew)  
    ```  
  
    ```csharp  
    // Removes the first item in the shortcut menu.  
    contextMenu1.MenuItems.RemoveAt(0);  
    // Removes a particular object from the shortcut menu.  
    contextMenu1.MenuItems.Remove(mnuItemNew);  
    ```  
  
    ```cpp  
    // Removes the first item in the shortcut menu.  
    contextMenu1->MenuItems->RemoveAt(0);  
    // Removes a particular object from the shortcut menu.  
    contextMenu1->MenuItems->Remove(mnuItemNew);  
    ```  
  
     O bien  
  
2.  Use la `Clear` método de la `MenuItems` colección de los <xref:System.Windows.Forms.ContextMenu> componente para quitar todos los elementos del menú.  
  
    ```vb  
    ContextMenu1.MenuItems.Clear()  
    ```  
  
    ```csharp  
    contextMenu1.MenuItems.Clear();  
    ```  
  
    ```cpp  
    contextMenu1->MenuItems->Clear();  
    ```  
  
## <a name="see-also"></a>Vea también
- <xref:System.Windows.Forms.ContextMenu>
- [ContextMenu (componente)](contextmenu-component-windows-forms.md)
- [Información general sobre ContextMenu](contextmenu-component-overview-windows-forms.md)
