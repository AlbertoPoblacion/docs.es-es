---
title: Procedimiento para crear formularios secundarios MDI
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- MDI [Windows Forms], creating forms
- child forms
ms.assetid: 164b69bb-2eca-4339-ada3-0679eb2c6dda
ms.openlocfilehash: 8965231307da84fd555b181440978adbea7e7244
ms.sourcegitcommit: 7e129d879ddb42a8b4334eee35727afe3d437952
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66052842"
---
# <a name="how-to-create-mdi-child-forms"></a>Procedimiento Crear formularios MDI secundarios

Formularios secundarios MDI son un elemento esencial de [aplicaciones de interfaz de múltiples documentos (MDI)](multiple-document-interface-mdi-applications.md), ya que estos formularios son el centro de la interacción del usuario.

En el siguiente procedimiento, usará Visual Studio para crear un formulario MDI secundario que muestra un <xref:System.Windows.Forms.RichTextBox> control, similar a las aplicaciones más procesamiento de texto. Sustituir el control <xref:System.Windows.Forms> por otros controles, como el control <xref:System.Windows.Forms.DataGridView>, o por una mezcla de controles permite crear ventanas secundarias MDI (y, por extensión, aplicaciones MDI) con diversas posibilidades.

## <a name="create-mdi-child-forms"></a>Crear formularios MDI secundarios

1. Cree un nuevo proyecto de Windows Forms. En **las propiedades de Windows** del formulario, establezca su <xref:System.Windows.Forms.Form.IsMdiContainer%2A> propiedad `true`y su `WindowsState` propiedad `Maximized`.

   Esto hace que el formulario se designe como contenedor MDI de las ventanas secundarias.

2. Desde el `Toolbox`, arrastre un control <xref:System.Windows.Forms.MenuStrip> al formulario. Establezca su `Text` propiedad **archivo**.

3. Haga clic en el botón de puntos suspensivos (...) junto a la **elementos** propiedad y haga clic en **agregar** para agregar dos elementos de menú de franja de herramientas secundarios. Establecer el `Text` propiedad para que estos elementos **New** y **ventana**.

4. En **el Explorador de soluciones**, haga clic en el proyecto, seleccione **agregar**y, a continuación, seleccione **Agregar nuevo elemento**.

5. En el **Agregar nuevo elemento** cuadro de diálogo, seleccione **formulario Windows** (en Visual Basic o Visual C#) o **aplicación de Windows Forms (. NET)** (en Visual C++) desde el **Plantillas** panel. En el **nombre** cuadro, asigne el nombre del formulario **Form2**. Haga clic en el **abierto** para agregar el formulario al proyecto.

    > [!NOTE]
    > El formulario secundario MDI creado en este paso es un Windows Form estándar. Como tal, tiene una propiedad <xref:System.Windows.Forms.Form.Opacity%2A>, que le permite controlar la transparencia del formulario. Sin embargo, la propiedad <xref:System.Windows.Forms.Form.Opacity%2A> se diseñó para ventanas de nivel superior. No la use con formularios secundarios MDI porque se pueden producir problemas de dibujo.

     Este formulario será la plantilla para los formularios secundarios MDI.

     El **Diseñador de Windows Forms** se abre, mostrando **Form2**.

6. Desde el **cuadro de herramientas**, arrastre un **RichTextBox** control al formulario.

7. En el **propiedades** ventana, establezca el `Anchor` propiedad **superior, izquierdo** y el `Dock` propiedad **rellenar**.

   Esto hace que el control <xref:System.Windows.Forms.RichTextBox> rellene completamente el área del formulario MDI secundario, incluso cuando se cambia el tamaño del formulario.

8. Haga doble clic en el **New** elemento de menú para crear un <xref:System.Windows.Forms.Control.Click> controlador de eventos para él.

9. Inserte código similar al siguiente para crear un nuevo formulario MDI secundario cuando el usuario hace clic en el **New** elemento de menú.

   > [!NOTE]
   > En el ejemplo siguiente, el controlador de eventos controla el evento <xref:System.Windows.Forms.Control.Click> para `MenuItem2`. Tenga en cuenta que, según las particularidades de la arquitectura de aplicaciones, su **New** no puede ser el elemento de menú `MenuItem2`.

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

   En C++, agregue la siguiente `#include` la directiva al principio de Form1.h:

   ```cpp
   #include "Form2.h"
   ```

10. En la lista desplegable en la parte superior de la **propiedades** ventana, seleccione la franja de menú que corresponde a la **archivo** banda del menú y establezca el <xref:System.Windows.Forms.MenuStrip.MdiWindowListItem%2A> propiedad a la ventana <xref:System.Windows.Forms.ToolStripMenuItem>.

    Esto habilitará la **ventana** menú para mantener una lista de ventanas MDI secundarias abiertas con una marca de verificación situada junto a la ventana secundaria activa.

11. Presione **F5** para ejecutar la aplicación. Seleccionando **New** desde el **archivo** menú, puede crear nuevos formularios MDI secundarios, que se mantiene un seguimiento en el **ventana** elemento de menú.

    > [!NOTE]
    > Cuando un formulario MDI secundario tiene un componente <xref:System.Windows.Forms.MainMenu> (por lo general, con una estructura de menús con elementos de menú) y se abre dentro de un formulario MDI primario que tiene un componente <xref:System.Windows.Forms.MainMenu> (por lo general, con una estructura de menús con elementos de menú), los elementos de menú se combinan automáticamente si ha establecido la propiedad <xref:System.Windows.Forms.MenuItem.MergeType%2A> (y, opcionalmente, la propiedad <xref:System.Windows.Forms.MenuItem.MergeOrder%2A>). Establezca la propiedad <xref:System.Windows.Forms.MenuItem.MergeType%2A> de ambos componentes <xref:System.Windows.Forms.MainMenu> y todos los elementos de menú del formulario secundario en <xref:System.Windows.Forms.MenuMerge.MergeItems>. Además, establezca la propiedad <xref:System.Windows.Forms.MenuItem.MergeOrder%2A> para que los elementos de ambos menús aparezcan en el orden deseado. Tenga en cuenta también que, cuando se cierra un formulario MDI primario, cada uno de los formularios MDI secundarios genera un evento <xref:System.Windows.Forms.Form.Closing> antes de que se produzca el evento <xref:System.Windows.Forms.Form.Closing> para el formulario MDI primario. Cancelar el evento <xref:System.Windows.Forms.Form.Closing> de un elemento MDI secundario no impedirá que se produzca el evento <xref:System.Windows.Forms.Form.Closing> del elemento MDI primario; sin embargo, el argumento <xref:System.ComponentModel.CancelEventArgs> del evento <xref:System.Windows.Forms.Form.Closing> del elemento MDI primario ahora se establecerá en `true`. Puede forzar el cierre del formularios MDI primario y de todos los formularios MDI secundarios estableciendo el argumento <xref:System.ComponentModel.CancelEventArgs> en `false`.

## <a name="see-also"></a>Vea también

- [Aplicaciones de interfaz de múltiples documentos (MDI)](multiple-document-interface-mdi-applications.md)
- [Cómo: Crear formularios principales MDI](how-to-create-mdi-parent-forms.md)
- [Cómo: Determinar el formulario secundario MDI activo](how-to-determine-the-active-mdi-child.md)
- [Cómo: Enviar datos al formulario secundario MDI activo](how-to-send-data-to-the-active-mdi-child.md)
- [Cómo: Organizar formularios MDI secundarios](how-to-arrange-mdi-child-forms.md)
