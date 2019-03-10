---
title: Filtrar Agregar elementos de menú a ContextMenuStrip
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ContextMenuStrips [Windows Forms], adding menu items
- shortcut menus [Windows Forms], adding items
- context menus [Windows Forms], adding menu items
ms.assetid: 1ec14776-3ea2-4752-bd22-4fae0fd19e1a
ms.openlocfilehash: a12a201ac73c86bf391d39f47baa47c87bf96095
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2019
ms.locfileid: "57716767"
---
# <a name="how-to-add-menu-items-to-a-contextmenustrip"></a>Procedimiento Agregar elementos de menú a ContextMenuStrip
Puede agregar simplemente un elemento de menú o varios elementos a la vez a un <xref:System.Windows.Forms.ContextMenuStrip>.  
  
### <a name="to-add-a-single-menu-item-to-a-contextmenustrip"></a>Para agregar un solo elemento de menú a ContextMenuStrip  
  
-   Use la <xref:System.Windows.Forms.ToolStripItemCollection.Add%2A> método para agregar un elemento de menú a un <xref:System.Windows.Forms.ContextMenuStrip>.  
  
    ```vb  
    Me.contextMenuStrip1.Items.Add(Me.toolStripMenuItem1)  
    ```  
  
    ```csharp  
    this.contextMenuStrip1.Items.Add(toolStripMenuItem1);  
    ```  
  
### <a name="to-add-several-menu-items-to-a-contextmenustrip"></a>Para agregar varios elementos de menú a ContextMenuStrip  
  
-   Use la <xref:System.Windows.Forms.ToolStripItemCollection.AddRange%2A> método para agregar varios elementos de menú a un <xref:System.Windows.Forms.ContextMenuStrip>.  
  
    ```vb  
    Me.contextMenuStrip1.Items.AddRange(New _  
       System.Windows.Forms.ToolStripItem() {Me.toolStripMenuItem1, _  
          Me.toolStripMenuItem2})  
    ```  
  
    ```csharp  
    this.contextMenuStrip1.Items.AddRange(new   
       System.Windows.Forms.ToolStripItem[] {  
          this.toolStripMenuItem1, this.toolStripMenuItem2});  
    ```  
  
## <a name="see-also"></a>Vea también
- [ContextMenuStrip (Control)](contextmenustrip-control.md)
