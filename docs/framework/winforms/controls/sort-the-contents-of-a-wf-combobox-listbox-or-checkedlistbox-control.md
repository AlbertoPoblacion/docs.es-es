---
title: Procedimiento para ordenar el contenido de un control ComboBox, CheckedListBox o ListBox de formularios Windows Forms
ms.date: 03/30/2017
helpviewer_keywords:
- CheckedListBox control [Windows Forms], sorting
- ComboBox control [Windows Forms], sorting contents
- combo boxes [Windows Forms], sorting contents
- list boxes [Windows Forms], sorting contents
- ListBox control [Windows Forms], sorting contents
ms.assetid: c268e387-3d1d-4d86-a940-19f6673c8d06
ms.openlocfilehash: bd26d396c238bfc53858320b8f4487df84b3436a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61902998"
---
# <a name="how-to-sort-the-contents-of-a-windows-forms-combobox-listbox-or-checkedlistbox-control"></a>Procedimiento para ordenar el contenido de un control ComboBox, CheckedListBox o ListBox de formularios Windows Forms
Controles de formularios Windows Forms no se ordenan cuando están enlazados a datos. Para mostrar datos ordenados, utilice un origen de datos que admite la ordenación y, a continuación, tiene el origen de datos ordenarlo. Orígenes de datos que admiten la ordenación son vistas de datos, ver administradores de datos y ordenan las matrices.  
  
 Si el control no está enlazado a datos, se puede ordenar.  
  
### <a name="to-sort-the-list"></a>Para ordenar la lista  
  
1. Establezca la propiedad `Sorted` en `true`.  
  
     Esta configuración ordenarán en todos los elementos de lista existente.  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Forms.ComboBox>
- <xref:System.Windows.Forms.ListBox>
- <xref:System.Windows.Forms.CheckedListBox>
- [Enlace de datos en Windows Forms](../windows-forms-data-binding.md)
- [Cómo: Agregar y quitar elementos de un Windows Forms control ComboBox, ListBox o CheckedListBox (Control)](add-and-remove-items-from-a-wf-combobox.md)
- [Cuándo utilizar un control ComboBox de formularios Windows Forms en lugar de un control ListBox](when-to-use-a-windows-forms-combobox-instead-of-a-listbox.md)
- [Controles de formularios Windows Forms usados para mostrar opciones](windows-forms-controls-used-to-list-options.md)
