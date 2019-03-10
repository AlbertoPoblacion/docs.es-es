---
title: Procedimiento Mostrar una lista de fuentes con el componente FontDialog
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- fonts [Windows Forms], showing list
- FontDialog component [Windows Forms]
- fonts [Windows Forms], attributes
- Font property [Windows Forms], setting with FontDialog component
- Font dialog box [Windows Forms], displaying
- fonts [Windows Forms], selecting
ms.assetid: 35692c1b-0937-4b7a-9207-1ae6bdc244a0
ms.openlocfilehash: 4036b6e12d8c4df2c4edfd5df293160d9197b61a
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2019
ms.locfileid: "57717068"
---
# <a name="how-to-show-a-font-list-with-the-fontdialog-component"></a>Procedimiento Mostrar una lista de fuentes con el componente FontDialog
El [FontDialog](fontdialog-component-windows-forms.md) componente permite a los usuarios seleccionar una fuente, así como cambiar sus características de presentación, como el tamaño y peso.  
  
 Se devuelve la fuente seleccionada en el cuadro de diálogo en el <xref:System.Windows.Forms.FontDialog.Font%2A> propiedad. Por lo tanto, es tan fácil como leer una propiedad que aprovecha la fuente seleccionada por el usuario.  
  
### <a name="to-select-font-properties-using-the-fontdialog-component"></a>Para seleccionar las propiedades de fuente mediante el componente FontDialog  
  
1.  Mostrar el cuadro de diálogo mediante la <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> método.  
  
2.  Use el <xref:System.Windows.Forms.DialogResult> propiedad para determinar cómo se cerró el cuadro de diálogo.  
  
3.  Use el <xref:System.Windows.Forms.FontDialog.Font%2A> propiedad para establecer la fuente deseada.  
  
     En el ejemplo siguiente, la <xref:System.Windows.Forms.Button> del control <xref:System.Windows.Forms.Control.Click> controlador de eventos abre un <xref:System.Windows.Forms.FontDialog> componente. Cuando una fuente es elegido y el usuario hace clic en **Aceptar**, <xref:System.Windows.Forms.FontDialog.Font%2A> propiedad de un <xref:System.Windows.Forms.TextBox> control que está en el formulario se establece en la fuente elegida. En el ejemplo se da por supuesto que el formulario tiene un <xref:System.Windows.Forms.Button> (control), un <xref:System.Windows.Forms.TextBox> control y un <xref:System.Windows.Forms.FontDialog> componente.  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, _  
       ByVal e As System.EventArgs) Handles Button1.Click  
       If FontDialog1.ShowDialog() = DialogResult.OK Then  
          TextBox1.Font = FontDialog1.Font  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       if(fontDialog1.ShowDialog() == DialogResult.OK)  
       {  
          textBox1.Font = fontDialog1.Font;  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       void button1_Click(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          if(fontDialog1->ShowDialog() == DialogResult::OK)  
          {  
             textBox1->Font = fontDialog1->Font;  
          }  
       }  
    ```  
  
     (Visual C# y [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]) coloque el código siguiente en el constructor del formulario para registrar el controlador de eventos.  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
    ```  
  
    ```cpp  
    button1->Click += gcnew System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
## <a name="see-also"></a>Vea también
- <xref:System.Windows.Forms.FontDialog>
- [FontDialog (componente)](fontdialog-component-windows-forms.md)
