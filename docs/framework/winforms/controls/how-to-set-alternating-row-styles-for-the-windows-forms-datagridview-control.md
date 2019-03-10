---
title: Filtrar Establecer estilos de fila alternos para el Control DataGridView de Windows Forms
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGridView control [Windows Forms], row styles
- data grids [Windows Forms], row styles
- rows [Windows Forms], data grids
ms.assetid: 699ef759-458c-426d-ac87-7c7e71b018ae
ms.openlocfilehash: 56fe5de9c69d14368508a7f6ccdd6c3becd8ff5b
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2019
ms.locfileid: "57710256"
---
# <a name="how-to-set-alternating-row-styles-for-the-windows-forms-datagridview-control"></a>Filtrar Establecer estilos de fila alternos para el Control DataGridView de Windows Forms
Los datos tabulares suelen presentarse a los usuarios en un formato de doble carta en el que las filas alternas tienen distintos colores de fondo. Este formato permite a los usuarios saber fácilmente qué celdas están en cada fila, especialmente con tablas anchas que tienen muchas columnas.  
  
 Con el control <xref:System.Windows.Forms.DataGridView>, puede especificar la información de estilo completa para las filas alternas. Esto permite usar características de estilo tales como el color de primer plano y la fuente, además del color de fondo, para diferenciar las filas alternas.  
  
 Visual Studio es compatible con esta tarea.  Consulte también [Cómo: Establecer estilos de fila alternos para los Windows Forms Control DataGridView de formularios mediante el diseñador](set-alternating-row-styles-for-the-datagrid-using-the-designer.md).  
  
### <a name="to-set-alternating-row-styles-programmatically"></a>Para establecer estilos de fila alternos mediante programación  
  
-   Establezca las propiedades de los objetos <xref:System.Windows.Forms.DataGridViewCellStyle> devueltos por las propiedades <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A> y <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A> de <xref:System.Windows.Forms.DataGridView>.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#068](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#068)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#068](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#068)]  
  
    > [!NOTE]
    >  Los estilos especificados con las propiedades <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A> y <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A> invalidan los estilos especificados en el nivel de columna y de <xref:System.Windows.Forms.DataGridView>, pero son invalidados por los estilos establecidos en el nivel de cada fila y celda. Para obtener más información, consulte [estilos de celda en el DataGridView Control de Windows Forms](cell-styles-in-the-windows-forms-datagridview-control.md).  
  
## <a name="compiling-the-code"></a>Compilar el código  
 Para este ejemplo se necesita:  
  
-   Un control <xref:System.Windows.Forms.DataGridView> llamado `dataGridView1`.  
  
-   Referencias a los ensamblados <xref:System?displayProperty=nameWithType>, <xref:System.Drawing?displayProperty=nameWithType> y <xref:System.Windows.Forms?displayProperty=nameWithType>.  
  
## <a name="robust-programming"></a>Programación sólida  
 Para conseguir la máxima escalabilidad, debe compartir objetos <xref:System.Windows.Forms.DataGridViewCellStyle> entre varias filas, columnas o celdas que usen los mismos estilos, en lugar de establecer las propiedades de estilo de cada elemento por separado. Para obtener más información, consulte [mejores prácticas para escalar el DataGridView Control de Windows Forms](best-practices-for-scaling-the-windows-forms-datagridview-control.md).  
  
## <a name="see-also"></a>Vea también
- <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridViewCellStyle>
- [Estilo y formato básicos del control DataGridView en formularios Windows Forms](basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)
- [Estilos de celda en el control DataGridView de Windows Forms](cell-styles-in-the-windows-forms-datagridview-control.md)
- [Procedimientos recomendados para ajustar la escala del control DataGridView en formularios Windows Forms](best-practices-for-scaling-the-windows-forms-datagridview-control.md)
- [Cómo: Establecer estilos de colores y fuentes en el Control DataGridView de Windows Forms](how-to-set-font-and-color-styles-in-the-windows-forms-datagridview-control.md)
