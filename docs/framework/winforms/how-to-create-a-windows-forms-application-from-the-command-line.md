---
title: 'Cómo: crear una aplicación de Windows Forms desde la línea de comandos'
ms.date: 03/14/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Windows Forms, application development from command line
- Windows Forms, getting started
- Windows Forms, creating basic form
ms.assetid: 45ad3f8b-1c26-4c9f-91a9-3bb0759a47a4
ms.openlocfilehash: af1548602ece8ea0f5720a836ec05648854e198f
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2019
ms.locfileid: "73127245"
---
# <a name="how-to-create-a-windows-forms-application-from-the-command-line"></a>Cómo: crear una aplicación de Windows Forms desde la línea de comandos

Los procedimientos siguientes describen los pasos básicos que debe seguir para crear y ejecutar una aplicación de Windows Forms desde la línea de comandos. Visual Studio es altamente compatible con estos procedimientos.  Vea también [Tutorial: hospedar un control de Windows Forms en WPF](../wpf/advanced/walkthrough-hosting-a-windows-forms-control-in-wpf.md).
  
## <a name="procedure"></a>Procedimiento  
  
#### <a name="to-create-the-form"></a>Para crear el formulario  
  
1. En un archivo de código vacío, escriba las instrucciones `Imports` o `using` siguientes:  
  
     [!code-csharp[System.Windows.Forms.BasicForm#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.BasicForm#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/VB/Form1.vb#2)]  
  
2. Declare una clase denominada `Form1` que herede de la clase de formulario:
  
     [!code-csharp[System.Windows.Forms.BasicForm#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.BasicForm#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/VB/Form1.vb#3)]  
  
3. Cree un constructor sin parámetros para `Form1`.
  
     Agregará más código al constructor en un procedimiento posterior.
  
     [!code-csharp[System.Windows.Forms.BasicForm#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.BasicForm#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/VB/Form1.vb#4)]  
  
4. Agregue un método `Main` a la clase.
  
    1. Aplique el <xref:System.STAThreadAttribute> al método C# `Main` para especificar que la aplicación Windows Forms es un contenedor uniproceso. (El atributo no es necesario en Visual Basic, ya que las aplicaciones de Windows Forms desarrolladas con Visual Basic usan de forma predeterminada un modelo de apartamento de un solo subproceso).  
  
    2. Llame a <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> para aplicar estilos de sistema operativo a la aplicación.  
  
    3. Cree una instancia del formulario y ejecútela.  
  
     [!code-csharp[System.Windows.Forms.BasicForm#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/CS/Form1.cs#5)]
     [!code-vb[System.Windows.Forms.BasicForm#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/VB/Form1.vb#5)]  
  
#### <a name="to-compile-and-run-the-application"></a>Para compilar y ejecutar la aplicación  
  
1. En el símbolo del sistema de .NET Framework, vaya al directorio donde creó la clase `Form1`.  
  
2. Compile el formulario.  
  
    - Si usa C#, escriba: `csc form1.cs`  
  
         `-or-`  
  
    - Si está utilizando Visual Basic, escriba: `vbc form1.vb`  
  
3. En el símbolo del sistema, escriba: `Form1.exe`  
  
## <a name="adding-a-control-and-handling-an-event"></a>Agregar un control y controlar un evento

Los pasos del procedimiento anterior muestran cómo crear un Windows Form básico que se compila y se ejecuta. El procedimiento siguiente mostrará cómo crear y agregar un control al formulario y cómo controlar un evento del control. Para obtener más información sobre los controles que se pueden agregar a Windows Forms, vea [controles de Windows Forms](./controls/index.md).
  
 Además de comprender cómo se crean las aplicaciones de Windows Forms, debe conocer la programación basada en eventos y cómo controlar la entrada de datos del usuario. Para obtener más información, vea [crear controladores de eventos en Windows Forms](creating-event-handlers-in-windows-forms.md)y [controlar los datos proporcionados](./controls/handling-user-input.md) por el usuario.  
  
#### <a name="to-declare-a-button-control-and-handle-its-click-event"></a>Para declarar un control de botón y controlar su evento de clic  
  
1. Declare un control de botón llamado `button1`.  
  
2. En el constructor, cree el botón y establezca sus propiedades <xref:System.Windows.Forms.Control.Size%2A>, <xref:System.Windows.Forms.Control.Location%2A> y <xref:System.Windows.Forms.Control.Text%2A>.  
  
3. Agregue el botón al formulario.  
  
     En el ejemplo de código siguiente se muestra cómo declarar el control de botón:
  
     [!code-csharp[System.Windows.Forms.FormWithButton#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.FormWithButton#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/VB/Form1.vb#2)]  
  
4. Cree un método para controlar los eventos <xref:System.Windows.Forms.Control.Click> del botón.  
  
5. En el controlador de eventos de clic, muestre un <xref:System.Windows.Forms.MessageBox> con el mensaje "Hello World".  
  
     En el ejemplo de código siguiente se muestra cómo controlar el evento click del control Button:
  
     [!code-csharp[System.Windows.Forms.FormWithButton#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.FormWithButton#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/VB/Form1.vb#3)]  
  
6. Asocie el evento <xref:System.Windows.Forms.Control.Click> con el método que se ha creado.  
  
     En el ejemplo de código siguiente se muestra cómo asociar el evento con el método.  
  
     [!code-csharp[System.Windows.Forms.FormWithButton#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.FormWithButton#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/VB/Form1.vb#4)]  
  
7. Compile y ejecute la aplicación tal y como se describe en el procedimiento anterior.  
  
## <a name="example"></a>Ejemplo  
 
El ejemplo de código siguiente es el ejemplo completo de los procedimientos anteriores:
  
 [!code-csharp[System.Windows.Forms.FormWithButton#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.FormWithButton#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/VB/Form1.vb#1)]  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Forms.Form>
- <xref:System.Windows.Forms.Control>
- [Cambiar la apariencia de Windows Forms](changing-the-appearance-of-windows-forms.md)
- [Mejorar las aplicaciones de Windows Forms](./advanced/index.md)
- [Introducción a los formularios Windows Forms](getting-started-with-windows-forms.md)
