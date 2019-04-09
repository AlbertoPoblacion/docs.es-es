---
title: 'Tutorial: Llevar a cabo una operación de arrastrar y colocar en formularios Windows Forms'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Windows Forms, drag and drop operations
- drag and drop [Windows Forms], Windows Forms
ms.assetid: eb66f6bf-4a7d-4c2d-b276-40fefb2d3b6c
ms.openlocfilehash: e9b21d7bfa188ebb053f36e2637ffce5d6fa0dd7
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59189032"
---
# <a name="walkthrough-performing-a-drag-and-drop-operation-in-windows-forms"></a>Tutorial: Llevar a cabo una operación de arrastrar y colocar en formularios Windows Forms
Para realizar operaciones de arrastrar y colocar en aplicaciones basadas en Windows debe controlar una serie de eventos, sobre todo la <xref:System.Windows.Forms.Control.DragEnter>, <xref:System.Windows.Forms.Control.DragLeave>, y <xref:System.Windows.Forms.Control.DragDrop> eventos. Trabajando con la información disponible en los argumentos de estos eventos, puede facilitar sin problemas las operaciones de arrastrar y colocar.  
  
## <a name="dragging-data"></a>Arrastrar datos  
 Todas las operaciones de arrastrar y colocar comienzan con arrastrar. La funcionalidad para habilitar los datos se recopilan cuando comienza a arrastrar se implementa en el <xref:System.Windows.Forms.Control.DoDragDrop%2A> método.  
  
 En el ejemplo siguiente, la <xref:System.Windows.Forms.Control.MouseDown> eventos se usan para iniciar la operación de arrastre porque es más intuitivo (la mayoría de las acciones de arrastrar y colocar empiezan con el botón del mouse cuando se presiona). Sin embargo, recuerde que podría utilizarse cualquier evento para iniciar un procedimiento de arrastrar y colocar.  
  
> [!NOTE]
>  Determinados controles tienen eventos personalizados específicos para la acción de arrastrar. El <xref:System.Windows.Forms.ListView> y <xref:System.Windows.Forms.TreeView> controles, por ejemplo, tienen un <xref:System.Windows.Forms.TreeView.ItemDrag> eventos.  
  
#### <a name="to-start-a-drag-operation"></a>Para iniciar una operación de arrastrar  
  
1.  En el <xref:System.Windows.Forms.Control.MouseDown> eventos del control donde se iniciará la operación de arrastrar, utilice el `DoDragDrop` tendrán método para establecer los datos que se arrastran y el efecto permitido. Para obtener más información, vea <xref:System.Windows.Forms.DragEventArgs.Data%2A> y <xref:System.Windows.Forms.DragEventArgs.AllowedEffect%2A>.  
  
     En el ejemplo siguiente se muestra cómo iniciar una operación de arrastrar. El control donde comienza la operación de arrastrar es un <xref:System.Windows.Forms.Button> control, los datos que se arrastran es la cadena que representa el <xref:System.Windows.Forms.Control.Text%2A> propiedad de la <xref:System.Windows.Forms.Button> control y los efectos permitidos son copiar o mover.  
  
    ```vb  
    Private Sub Button1_MouseDown(ByVal sender As Object, ByVal e As System.Windows.Forms.MouseEventArgs) Handles Button1.MouseDown  
       Button1.DoDragDrop(Button1.Text, DragDropEffects.Copy Or DragDropEffects.Move)  
    End Sub  
    ```  
  
    ```csharp  
    private void button1_MouseDown(object sender,   
    System.Windows.Forms.MouseEventArgs e)  
    {  
       button1.DoDragDrop(button1.Text, DragDropEffects.Copy |   
          DragDropEffects.Move);  
    }  
    ```  
  
    > [!NOTE]
    >  Se puede usar cualquier dato como parámetro en el `DoDragDrop` método; en el ejemplo anterior, el <xref:System.Windows.Forms.Control.Text%2A> propiedad de la <xref:System.Windows.Forms.Button> se usó el control (en lugar de codificar de forma rígida un valor o recuperar datos de un conjunto de datos) porque la propiedad estaba relacionada con el ubicación que se arrastran desde (el <xref:System.Windows.Forms.Button> control). Téngalo en cuenta cuando incorpore operaciones de arrastrar y colocar en aplicaciones basadas en Windows.  
  
 Mientras una operación de arrastrar está en vigor, se puede controlar la <xref:System.Windows.Forms.Control.QueryContinueDrag> eventos, que "pide permiso" del sistema para continuar la operación de arrastre. Este método de control, es el punto adecuado para llamar a métodos que tengan un efecto en la operación de arrastrar, como expandir un <xref:System.Windows.Forms.TreeNode> en un <xref:System.Windows.Forms.TreeView> controlar cuando el cursor se desplaza sobre él.  
  
## <a name="dropping-data"></a>Colocar datos  
 Una vez que haya empezado a arrastrar datos desde una ubicación a un control o Windows Forms, naturalmente deseará colocarlos en algún lugar. El cursor cambiará cuando cruce una zona de un formulario o control que esté configurada correctamente para la colocación de datos. ¿Se pueden hacer cualquier zona dentro de un formulario de Windows o un control para aceptar datos colocados estableciendo el <xref:System.Windows.Forms.Control.AllowDrop%2A> propiedad y el control de la <xref:System.Windows.Forms.Control.DragEnter> y <xref:System.Windows.Forms.Control.DragDrop> eventos.  
  
#### <a name="to-perform-a-drop"></a>Para llevar a cabo la operación de colocar  
  
1.  Establecer el <xref:System.Windows.Forms.Control.AllowDrop%2A> propiedad en true.  
  
2.  En el `DragEnter` eventos para el control donde tendrá lugar la operación de colocar, asegúrese de que los datos que se arrastran son de un tipo aceptable (en este caso, <xref:System.Windows.Forms.Control.Text%2A>). El código, a continuación, Establece el efecto que tendrá lugar cuando se produce la entrega a un valor en el <xref:System.Windows.Forms.DragDropEffects> enumeración. Para obtener más información, consulta <xref:System.Windows.Forms.DragEventArgs.Effect%2A>.  
  
    ```vb  
    Private Sub TextBox1_DragEnter(ByVal sender As Object, ByVal e As System.Windows.Forms.DragEventArgs) Handles TextBox1.DragEnter  
       If (e.Data.GetDataPresent(DataFormats.Text)) Then  
         e.Effect = DragDropEffects.Copy  
       Else  
         e.Effect = DragDropEffects.None  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    private void textBox1_DragEnter(object sender,   
    System.Windows.Forms.DragEventArgs e)  
    {  
       if (e.Data.GetDataPresent(DataFormats.Text))   
          e.Effect = DragDropEffects.Copy;  
       else  
          e.Effect = DragDropEffects.None;  
    }  
    ```  
  
    > [!NOTE]
    >  Puede definir sus propios <xref:System.Windows.Forms.DataFormats> especificando su propio objeto como el <xref:System.Object> parámetro de la <xref:System.Windows.Forms.DataObject.SetData%2A> método. Cuando lo haga, asegúrese de que el objeto especificado sea serializable. Para obtener más información, consulta <xref:System.Runtime.Serialization.ISerializable>.  
  
3.  En el <xref:System.Windows.Forms.Control.DragDrop> eventos del control donde tendrá lugar la operación de colocar, utilice el <xref:System.Windows.Forms.DataObject.GetData%2A> método para recuperar los datos que se está arrastrando. Para obtener más información, consulta <xref:System.Security.Cryptography.Xml.DataObject.Data%2A>.  
  
     En el ejemplo siguiente, un <xref:System.Windows.Forms.TextBox> control es el control que se está arrastrando (donde tendrá lugar la operación de colocar). El código establece la <xref:System.Windows.Forms.Control.Text%2A> propiedad de la <xref:System.Windows.Forms.TextBox> controlar igual a los datos que se está arrastrando.  
  
    ```vb  
    Private Sub TextBox1_DragDrop(ByVal sender As Object, ByVal e As System.Windows.Forms.DragEventArgs) Handles TextBox1.DragDrop  
       TextBox1.Text = e.Data.GetData(DataFormats.Text).ToString  
    End Sub  
    ```  
  
    ```csharp  
    private void textBox1_DragDrop(object sender,   
    System.Windows.Forms.DragEventArgs e)  
    {  
       textBox1.Text = e.Data.GetData(DataFormats.Text).ToString();  
    }  
    ```  
  
    > [!NOTE]
    >  Además, puede trabajar con el <xref:System.Windows.Forms.DragEventArgs.KeyState%2A> propiedad, por lo que, en función de las teclas presionadas durante la operación de arrastrar y colocar, tengan lugar ciertos efectos (por ejemplo, es estándar copiar los datos arrastrados cuando se presiona la tecla CTRL).  
  
## <a name="see-also"></a>Vea también

- [Filtrar para agregar datos al Portapapeles](how-to-add-data-to-the-clipboard.md)
- [Filtrar para recuperar datos del Portapapeles](how-to-retrieve-data-from-the-clipboard.md)
- [Compatibilidad con las operaciones de arrastrar y colocar y con el Portapapeles](drag-and-drop-operations-and-clipboard-support.md)
