---
title: Procedimiento para extraer el icono asociado a un archivo en formularios Windows Forms
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- displaying a file name and its file type icon in a ListView control [Windows Forms]
- file name extension icons [Windows Forms], displaying in a ListView
- extracting icons associated with a file type [Windows Forms]
ms.assetid: 88e2ad8b-c34f-415a-84f2-dad756b5c928
ms.openlocfilehash: d754dc5e8a57b3c4e2e5439bb2524a22d44813c6
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62004047"
---
# <a name="how-to-extract-the-icon-associated-with-a-file-in-windows-forms"></a>Procedimiento para extraer el icono asociado a un archivo en formularios Windows Forms
Muchos archivos tienen iconos incrustados que proporcionan una representación visual del tipo de archivo asociado. Por ejemplo, documentos de Microsoft Word contienen un icono que se identifica como documentos de Word. Al mostrar los archivos en un control de lista o tabla, desea mostrar el icono que representa el tipo de archivo junto a cada nombre de archivo. Puede hacerlo fácilmente utilizando el <xref:System.Drawing.Icon.ExtractAssociatedIcon%2A> método.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo de código siguiente se muestra cómo extraer el icono asociado a un archivo y mostrar el nombre de archivo y el icono asociado en un <xref:System.Windows.Forms.ListView> control.  
  
 [!code-csharp[System.Drawing.Icon.ExtractAssociatedIconEx#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Icon.ExtractAssociatedIconEx/CS/Form1.cs#1)]
 [!code-vb[System.Drawing.Icon.ExtractAssociatedIconEx#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Icon.ExtractAssociatedIconEx/VB/Form1.vb#1)]  
  
## <a name="compiling-the-code"></a>Compilar el código  
 Para compilar el ejemplo:  
  
- Pegue el código anterior en un formulario de Windows y llaman a la `ExtractAssociatedIconExample` método desde el constructor del formulario o <xref:System.Windows.Forms.Form.Load> el método de control de eventos.  
  
     Deberá asegurarse de que el formulario se importa el <xref:System.IO> espacio de nombres.  
  
## <a name="see-also"></a>Vea también

- [Imágenes, mapas de bits y metarchivos](images-bitmaps-and-metafiles.md)
- [ListView (Control)](../controls/listview-control-windows-forms.md)
