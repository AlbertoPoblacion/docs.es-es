---
title: Filtrar Copiar ToolStripMenuItems
ms.date: 03/30/2017
helpviewer_keywords:
- menu items [Windows Forms], copying and pasting
- MenuStrip control [Windows Forms], arranging items
- ToolStripMenuItems [Windows Forms], copying and pasting
ms.assetid: 17ef4207-e92e-4db2-b648-27246e6517ad
ms.openlocfilehash: 18077f542b1b49f8e81e68fc1e7a5d3e1e417a21
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2019
ms.locfileid: "57713883"
---
# <a name="how-to-copy-toolstripmenuitems"></a>Procedimiento Copiar ToolStripMenuItems
Durante el diseño, puede copiar menús de nivel superior completos y sus elementos de submenú en un lugar diferente en la <xref:System.Windows.Forms.MenuStrip>. También puede copiar elementos de menú individuales entre los menús de nivel superior o cambiar la posición de los elementos de menú dentro de un menú.  
  
### <a name="to-copy-a-top-level-menu-and-its-submenu-items-to-another-top-level-location"></a>Para copiar un menú de nivel superior y sus elementos de submenú en otra ubicación de nivel superior  
  
1.  Haga clic en el menú que desea copiar y presione CTRL+C o haga clic con el botón derecho en el menú y seleccione **Copiar** en el menú contextual.  
  
2.  Haga clic en el menú de nivel superior que está después de la nueva ubicación deseada y presione CTRL+V o haga clic con el botón derecho en el elemento de menú de nivel superior anterior a la nueva ubicación deseada y seleccione **Pegar** en el menú contextual.  
  
     El menú copiado se inserta delante del menú de nivel superior seleccionado.  
  
### <a name="to-copy-a-top-level-menu-and-its-submenu-items-to-a-drop-down-location"></a>Para copiar un menú de nivel superior y sus elementos de submenú en una ubicación desplegable  
  
1.  Haga clic en el menú que desea mover y presione CTRL+C o haga clic con el botón derecho en el menú y seleccione **Copiar** en el menú contextual.  
  
2.  En el menú de nivel superior de destino, haga clic en el elemento de submenú que está encima de la nueva ubicación deseada y presione CTRL+V o haga clic con el botón derecho en el elemento de submenú que está encima de la nueva ubicación deseada y seleccione **Pegar** en el menú contextual.  
  
     El menú copiado se inserta delante del elemento de submenú seleccionado.  
  
### <a name="to-copy-a-submenu-item-to-another-menu"></a>Para copiar un elemento de submenú en otro menú  
  
1.  Haga clic en el elemento de submenú que desea copiar y presione CTRL+C o haga clic con el botón derecho en el elemento de submenú y seleccione **Copiar** en el menú contextual.  
  
2.  Haga clic en el menú que contendrá el elemento de submenú que ha cortado.  
  
3.  Haga clic en el elemento de submenú que está antes de la nueva ubicación deseada y presione CTRL+V o haga clic con el botón derecho en el elemento de submenú anterior a la nueva ubicación deseada y seleccione **Pegar** en el menú contextual.  
  
     El elemento de submenú copiado se inserta delante del elemento de submenú seleccionado.  
  
## <a name="see-also"></a>Vea también
- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ToolStripMenuItem>
- [Información general sobre el control MenuStrip](menustrip-control-overview-windows-forms.md)
