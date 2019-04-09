---
title: Filtrar para seleccionar las impresoras conectadas al equipo de un usuario en formularios Windows Forms
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- printing [Windows Forms], choosing printers
- printers [Windows Forms], choosing
ms.assetid: 63c1172b-2931-4ac0-953f-37f629494bbf
ms.openlocfilehash: bebb879020e6e45e77f109bf9c377b7322d5e8f3
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59184033"
---
# <a name="how-to-choose-the-printers-attached-to-a-users-computer-in-windows-forms"></a>Filtrar para seleccionar las impresoras conectadas al equipo de un usuario en formularios Windows Forms
A menudo, los usuarios quieren elegir una impresora que no sea la predeterminada. Para que los usuarios puedan elegir una impresora de entre las que están instaladas, use el componente <xref:System.Windows.Forms.PrintDialog> . Con el componente <xref:System.Windows.Forms.PrintDialog> , se captura el <xref:System.Windows.Forms.DialogResult> del componente <xref:System.Windows.Forms.PrintDialog> y se usa para seleccionar la impresora.  
  
 En el siguiente procedimiento se selecciona un archivo de texto para imprimirlo en la impresora predeterminada y luego se crea una instancia de la clase <xref:System.Windows.Forms.PrintDialog> .  
  
### <a name="to-choose-a-printer-and-then-print-a-file"></a>Para elegir una impresora e imprimir un archivo  
  
1.  Seleccione la impresora que se usará con el <xref:System.Windows.Forms.PrintDialog> componente.  
  
     En el siguiente ejemplo de código se tratan dos eventos. En el primero, un <xref:System.Windows.Forms.Button> del control <xref:System.Windows.Forms.Control.Click> eventos, el <xref:System.Windows.Forms.PrintDialog> se crea una instancia de clase y la impresora seleccionada por el usuario se captura en el <xref:System.Windows.Forms.DialogResult> propiedad.  
  
     En el segundo evento, el <xref:System.Drawing.Printing.PrintDocument.PrintPage> eventos de la <xref:System.Drawing.Printing.PrintDocument> , componente, se imprime un documento de ejemplo en la impresora especificada.  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button1.Click  
       Dim PrintDialog1 As New PrintDialog()  
       PrintDialog1.Document = PrintDocument1  
       Dim result As DialogResult = PrintDialog1.ShowDialog()  
  
       If (result = DialogResult.OK) Then  
         PrintDocument1.Print()  
       End If   
  
    End Sub  
  
    Private Sub PrintDocument1_PrintPage(ByVal sender As Object, ByVal e As System.Drawing.Printing.PrintPageEventArgs) Handles PrintDocument1.PrintPage  
       e.Graphics.FillRectangle(Brushes.Red, New Rectangle(500, 500, 500, 500))          
    End Sub  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       PrintDialog printDialog1 = new PrintDialog();  
       printDialog1.Document = printDocument1;  
       DialogResult result = printDialog1.ShowDialog();  
       if (result == DialogResult.OK)  
       {  
          printDocument1.Print();  
       }  
    }  
  
    private void printDocument1_PrintPage(object sender,   
    System.Drawing.Printing.PrintPageEventArgs e)  
    {  
       e.Graphics.FillRectangle(Brushes.Red,   
         new Rectangle(500, 500, 500, 500));  
    }  
    ```  
  
    ```cpp  
    private:  
       void button1_Click(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          PrintDialog ^ printDialog1 = gcnew PrintDialog();  
          printDialog1->Document = printDocument1;  
          System::Windows::Forms::DialogResult result =   
             printDialog1->ShowDialog();  
          if (result == DialogResult::OK)  
          {  
             printDocument1->Print();  
          }  
       }  
    private:  
       void printDocument1_PrintPage(System::Object ^ sender,  
          System::Drawing::Printing::PrintPageEventArgs ^ e)  
       {  
          e->Graphics->FillRectangle(Brushes::Red,  
             Rectangle(500, 500, 500, 500));  
       }  
    ```  
  
     (Visual C# y [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]) coloque el código siguiente en el constructor del formulario para registrar el controlador de eventos.  
  
    ```csharp  
    this.printDocument1.PrintPage += new  
       System.Drawing.Printing.PrintPageEventHandler  
       (this.printDocument1_PrintPage);  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
    ```  
  
    ```cpp  
    this->printDocument1->PrintPage += gcnew  
       System::Drawing::Printing::PrintPageEventHandler  
       (this, &Form1::printDocument1_PrintPage);  
    this->button1->Click += gcnew  
       System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
## <a name="see-also"></a>Vea también

- [Funcionalidad para imprimir en formularios Windows Forms](windows-forms-print-support.md)
