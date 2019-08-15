---
title: Procedimiento para crear formularios secundarios MDI
ms.date: 03/30/2017
dev_langs:
- CSharp
- CPP
- VB
helpviewer_keywords:
- MDI [Windows Forms], creating forms
- child forms
ms.assetid: 164b69bb-2eca-4339-ada3-0679eb2c6dda
ms.openlocfilehash: f5e8682caf658d159f044528f040b99676355448
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/15/2019
ms.locfileid: "69040107"
---
# <a name="how-to-create-mdi-child-forms"></a>Procedimiento Crear formularios MDI secundarios

Los formularios MDI secundarios son un elemento fundamental de [las aplicaciones de interfaz de múltiples documentos (MDI)](multiple-document-interface-mdi-applications.md), ya que estos formularios son el centro de la interacción con el usuario.

En el procedimiento siguiente, usará Visual Studio para crear un formulario MDI secundario que muestre un <xref:System.Windows.Forms.RichTextBox> control, similar a la mayoría de las aplicaciones de procesamiento de texto. Al sustituir el <xref:System.Windows.Forms> control por otros controles, como el <xref:System.Windows.Forms.DataGridView> control, o una combinación de controles, puede crear ventanas secundarias MDI (y, por extensión, aplicaciones MDI) con diversas posibilidades.

## <a name="create-mdi-child-forms"></a>Crear formularios MDI secundarios

1. Cree un nuevo proyecto de aplicación de Windows Forms en Visual Studio. En la **ventana Propiedades** del formulario, <xref:System.Windows.Forms.Form.IsMdiContainer%2A> establezca su propiedad en `true` y su `WindowsState` propiedad en `Maximized`.

   Esto hace que el formulario se designe como contenedor MDI de las ventanas secundarias.

2. Desde el `Toolbox`, arrastre un control <xref:System.Windows.Forms.MenuStrip> al formulario. Establezca su `Text` propiedad en **archivo**.

3. Haga clic en los puntos suspensivos (...) junto a la propiedad **elementos** y haga clic en **Agregar** para agregar dos elementos de menú de la franja de herramientas secundaria. Establezca la `Text` propiedad de estos elementos en **nuevo** y **ventana**.

4. En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto y, a continuación, seleccione **Agregar** > **Nuevo elemento**.

5. En el cuadro de diálogo **Agregar nuevo elemento** , **Seleccione Windows Form** (en Visual Basic o en C#visual) o **Windows Forms aplicación (.net)** (en C++visual) en el panel **plantillas** . En el cuadro **nombre** , asigne al formulario el nombre **Form2**. Seleccione **abrir** para agregar el formulario al proyecto.

    > [!NOTE]
    > El formulario secundario MDI creado en este paso es un Windows Form estándar. Como tal, tiene una propiedad <xref:System.Windows.Forms.Form.Opacity%2A>, que le permite controlar la transparencia del formulario. Sin embargo, la propiedad <xref:System.Windows.Forms.Form.Opacity%2A> se diseñó para ventanas de nivel superior. No la use con formularios secundarios MDI porque se pueden producir problemas de dibujo.

     Este formulario será la plantilla para los formularios secundarios MDI.

     Se abre el **Diseñador de Windows Forms** , que muestra **Form2**.

6. En el **cuadro de herramientas**, arrastre un control **RichTextBox** al formulario.

7. En la ventana **propiedades** , establezca la `Anchor` propiedad en **superior, izquierda** y la `Dock` propiedad enrellenar.

   Esto hace que el control <xref:System.Windows.Forms.RichTextBox> rellene completamente el área del formulario MDI secundario, incluso cuando se cambia el tamaño del formulario.

8. Haga doble clic en el elemento de menú nuevo <xref:System.Windows.Forms.Control.Click> para crear un controlador de eventos para él.

9. Inserte código similar al siguiente para crear un nuevo formulario MDI secundario cuando el usuario haga clic en el **nuevo** elemento de menú.

   > [!NOTE]
   > En el ejemplo siguiente, el controlador de eventos controla el evento <xref:System.Windows.Forms.Control.Click> para `MenuItem2`. Tenga en cuenta que, en función de los detalles de la arquitectura de la aplicación , es posible que el nuevo `MenuItem2`elemento de menú no sea.

    ```vb
    Protected Sub MDIChildNew_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MenuItem2.Click
       Dim NewMDIChild As New Form2()
       'Set the Parent Form of the Child window.
       NewMDIChild.MdiParent = Me
       'Display the new form.
       NewMDIChild.Show()
    End Sub
    ```

    ```csharp
    protected void MDIChildNew_Click(object sender, System.EventArgs e){
       Form2 newMDIChild = new Form2();
       // Set the Parent Form of the Child window.
       newMDIChild.MdiParent = this;
       // Display the new form.
       newMDIChild.Show();
    }
    ```

    ```cpp
    private:
       void menuItem2_Click(System::Object ^ sender,
          System::EventArgs ^ e)
       {
          Form2^ newMDIChild = gcnew Form2();
          // Set the Parent Form of the Child window.
          newMDIChild->MdiParent = this;
          // Display the new form.
          newMDIChild->Show();
       }
    ```

   En C++, agregue la siguiente `#include` Directiva al principio de Form1. h:

   ```cpp
   #include "Form2.h"
   ```

10. En la lista desplegable de la parte superior de la ventana **propiedades** , seleccione la franja de menús correspondiente a la franja de menú **archivo** y establezca <xref:System.Windows.Forms.MenuStrip.MdiWindowListItem%2A> la propiedad en la <xref:System.Windows.Forms.ToolStripMenuItem>ventana.

    Esto permite que el menú **ventana** mantenga una lista de ventanas secundarias MDI abiertas con una marca de verificación junto a la ventana secundaria activa.

11. Presione **F5** para ejecutar la aplicación. Al seleccionar **nuevo** en el menú **archivo** , puede crear nuevos formularios MDI secundarios, cuyo seguimiento se mantiene en el elemento de menú **ventana** .

    > [!NOTE]
    > Cuando un formulario MDI secundario tiene un componente <xref:System.Windows.Forms.MainMenu> (por lo general, con una estructura de menús con elementos de menú) y se abre dentro de un formulario MDI primario que tiene un componente <xref:System.Windows.Forms.MainMenu> (por lo general, con una estructura de menús con elementos de menú), los elementos de menú se combinan automáticamente si ha establecido la propiedad <xref:System.Windows.Forms.MenuItem.MergeType%2A> (y, opcionalmente, la propiedad <xref:System.Windows.Forms.MenuItem.MergeOrder%2A>). Establezca la propiedad <xref:System.Windows.Forms.MenuItem.MergeType%2A> de ambos componentes <xref:System.Windows.Forms.MainMenu> y todos los elementos de menú del formulario secundario en <xref:System.Windows.Forms.MenuMerge.MergeItems>. Además, establezca la propiedad <xref:System.Windows.Forms.MenuItem.MergeOrder%2A> para que los elementos de ambos menús aparezcan en el orden deseado. Tenga en cuenta también que, cuando se cierra un formulario MDI primario, cada uno de los formularios MDI secundarios genera un evento <xref:System.Windows.Forms.Form.Closing> antes de que se produzca el evento <xref:System.Windows.Forms.Form.Closing> para el formulario MDI primario. Cancelar el evento <xref:System.Windows.Forms.Form.Closing> de un elemento MDI secundario no impedirá que se produzca el evento <xref:System.Windows.Forms.Form.Closing> del elemento MDI primario; sin embargo, el argumento <xref:System.ComponentModel.CancelEventArgs> del evento <xref:System.Windows.Forms.Form.Closing> del elemento MDI primario ahora se establecerá en `true`. Puede forzar el cierre del formularios MDI primario y de todos los formularios MDI secundarios estableciendo el argumento <xref:System.ComponentModel.CancelEventArgs> en `false`.

## <a name="see-also"></a>Vea también

- [Aplicaciones de interfaz de múltiples documentos (MDI)](multiple-document-interface-mdi-applications.md)
- [Procedimientos: Crear formularios MDI primarios](how-to-create-mdi-parent-forms.md)
- [Cómo: Determinar el elemento secundario MDI activo](how-to-determine-the-active-mdi-child.md)
- [Procedimientos: Enviar datos al elemento secundario MDI activo](how-to-send-data-to-the-active-mdi-child.md)
- [Procedimientos: Organizar formularios MDI secundarios](how-to-arrange-mdi-child-forms.md)
