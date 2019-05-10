---
title: 'Tutorial: Demostración de la herencia visual'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- form inheritance [Windows Forms], walkthroughs
- visual inheritance
- inheritance [Windows Forms], walkthroughs
- walkthroughs [Windows Forms], visual inheritance
- Windows Forms, inheritance
ms.assetid: 01966086-3142-450e-8210-3fd4cb33f591
ms.openlocfilehash: a5e2a8b0bf982ff112d7930e331456fa69485dfc
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2019
ms.locfileid: "64665910"
---
# <a name="walkthrough-demonstrating-visual-inheritance"></a>Tutorial: Demostración de la herencia visual
La herencia visual le permite ver los controles del formulario base y agregar controles nuevos. En este tutorial, creará un formulario base y lo compilará para convertirlo en una biblioteca de clases. Importará la biblioteca de clases en otro proyecto y creará un nuevo formulario que herede del formulario base. Durante este tutorial aprenderá a:  
  
- Crear un proyecto de biblioteca de clases que contiene un formulario base.  
  
- Agregar un botón con propiedades que las clases derivadas del formulario base pueden modificar.  
  
- Agregar un botón que los herederos del formulario base no pueden modificar.  
  
- Crear un proyecto que contiene un formulario que hereda de `BaseForm`.  
  
 Por último, en este tutorial se mostrará la diferencia entre los controles privados y los protegidos de un formulario heredado.  
  
> [!NOTE]
>  Los cuadros de diálogo y comandos de menú que se ven pueden diferir de los descritos en la Ayuda, en función de los valores de configuración o de edición activos. Para cambiar la configuración, elija la opción **Importar y exportar configuraciones** del menú **Herramientas** . Para más información, vea [Personalizar el IDE de Visual Studio](/visualstudio/ide/personalizing-the-visual-studio-ide).  
  
> [!CAUTION]
>  No todos los controles admiten la herencia visual a partir de un formulario base. Los siguientes controles no admiten el escenario que se describe en este tutorial:  
>   
>  <xref:System.Windows.Forms.WebBrowser>  
>   
>  <xref:System.Windows.Forms.ToolStrip>  
>   
>  <xref:System.Windows.Forms.ToolStripPanel>  
>   
>  <xref:System.Windows.Forms.TableLayoutPanel>  
>   
>  <xref:System.Windows.Forms.FlowLayoutPanel>  
>   
>  <xref:System.Windows.Forms.DataGridView>  
>   
>  Estos controles del formulario heredado siempre son de solo lectura, independientemente de los modificadores que utilice (`private`, `protected` o `public`).  
  
## <a name="scenario-steps"></a>Pasos del escenario  
 El primer paso es crear el formulario base.  
  
#### <a name="to-create-a-class-library-project-containing-a-base-form"></a>Para crear un proyecto de biblioteca de clases que contenga un formulario base  
  
1. Desde el **archivo** menú, elija **New**y, a continuación, **proyecto** para abrir el **nuevo proyecto** cuadro de diálogo.  
  
2. Cree una aplicación de Windows Forms denominada `BaseFormLibrary`.  
  
3. Para crear una biblioteca de clases en lugar de una aplicación de Windows Forms estándar, en **el Explorador de soluciones**, haga clic en el **BaseFormLibrary** nodo de proyecto y, a continuación, seleccione **propiedades**.  
  
4. En las propiedades del proyecto, cambie el **tipo de salida** desde **aplicación Windows** a **biblioteca de clases**.  
  
5. Desde el **archivo** menú, elija **guardar todo** para guardar el proyecto y archivos en la ubicación predeterminada.  
  
 Los dos procedimientos siguientes agregan botones al formulario base. Para ilustrar la herencia visual, proporcionará a los botones distintos niveles de acceso estableciendo sus propiedades `Modifiers`.  
  
#### <a name="to-add-a-button-that-inheritors-of-the-base-form-can-modify"></a>Para agregar un botón que los herederos del formulario base puedan modificar  
  
1. Abra **Form1** en el diseñador.  
  
2. En el **todos los formularios de Windows** pestaña de la **cuadro de herramientas**, haga doble clic en **botón** para agregar un botón al formulario. Use el mouse para colocar y cambiar de tamaño el botón.  
  
3. En la ventana Propiedades, establezca las propiedades siguientes del botón:  
  
    - Establecer el **texto** propiedad **Say Hello**.  
  
    - Establecer el **(nombre)** propiedad **btnProtected**.  
  
    - Establecer el **modificadores** propiedad **Protected**. Esto hace posible para los formularios que heredan de **Form1** para modificar las propiedades de **btnProtected**.  
  
4. Haga doble clic en el **Say Hello** para agregar un controlador de eventos para el **haga clic en** eventos.  
  
5. Agregue la línea de código siguiente al controlador del evento:  
  
    ```vb  
    MessageBox.Show("Hello, World!")  
    ```  
  
    ```csharp  
    MessageBox.Show("Hello, World!");  
    ```  
  
#### <a name="to-add-a-button-that-cannot-be-modified-by-inheritors-of-the-base-form"></a>Para agregar un botón que los herederos del formulario base no puedan modificar  
  
1. Cambiar a vista de diseño, haga clic en el **Form1.vb [Diseño], Form1.cs [Diseño] o Form1.jsl [Diseño]** ficha encima del editor de código o presionando F7.  
  
2. Agregue un segundo botón y establezca sus propiedades como sigue:  
  
    - Establecer el **texto** propiedad **Say Goodbye**.  
  
    - Establecer el **(nombre)** propiedad **btnPrivate**.  
  
    - Establecer el **modificadores** propiedad **privada**. Esto hace imposible que los formularios que heredan de **Form1** para modificar las propiedades de **btnPrivate**.  
  
3. Haga doble clic en el **Say Goodbye** para agregar un controlador de eventos para el **haga clic en** eventos. Coloque la siguiente línea de código en el procedimiento de evento:  
  
    ```vb  
    MessageBox.Show("Goodbye!")  
    ```  
  
    ```csharp  
    MessageBox.Show("Goodbye!");  
    ```  
  
4. Desde el **compilar** menú, elija **compilar biblioteca BaseForm** para compilar la biblioteca de clases.  
  
     Una vez compilada la biblioteca, puede crear un nuevo proyecto que herede del formulario que acaba de crear.  
  
#### <a name="to-create-a-project-containing-a-form-that-inherits-from-the-base-form"></a>Para crear un proyecto que contenga un formulario que herede del formulario base  
  
1. Desde el **archivo** menú, elija **agregar** y, a continuación, **nuevo proyecto** para abrir el **Agregar nuevo proyecto** cuadro de diálogo.  
  
2. Cree una aplicación de Windows Forms denominada `InheritanceTest`.  
  
#### <a name="to-add-an-inherited-form"></a>Para agregar un formulario heredado  
  
1. En **el Explorador de soluciones**, haga clic en el **InheritanceTest** proyecto, seleccione **agregar**y, a continuación, seleccione **nuevo elemento**.  
  
2. En el **Agregar nuevo elemento** cuadro de diálogo, seleccione el **Windows Forms** categoría (si tiene una lista de categorías) y, a continuación, seleccione el **formulario heredado** plantilla.  
  
3. Deje el nombre predeterminado de `Form2` y, a continuación, haga clic en **agregar**.  
  
4. En el **selector de herencia** cuadro de diálogo, seleccione **Form1** desde el **BaseFormLibrary** proyecto como el formulario para heredar de y haga clic en **Aceptar** .  
  
     Esto crea un formulario en el **InheritanceTest** proyecto que se deriva de la forma en **BaseFormLibrary**.  
  
5. Abra el formulario heredado (**Form2**) en el diseñador haciendo doble clic en él, si aún no está abierto.  
  
     En el diseñador, los botones heredados tienen un símbolo)![Captura de pantalla del símbolo de herencia de Visual Basic.](./media/walkthrough-demonstrating-visual-inheritance/visual-basic-inheritance-glyph.gif)) en la esquina superior para indicar que son heredados.  
  
6. Seleccione el **Say Hello** botón y observe los controladores de tamaño. Como este botón está protegido, los herederos pueden moverlo, cambiarlo de tamaño, cambiar su descripción y realizar otras modificaciones.  
  
7. Seleccione privado **Say Goodbye** botón y tenga en cuenta que no tiene controladores de tamaño. Además, en el **propiedades** ventana, las propiedades de este botón aparecen en gris para indicar que no se pueden modificar.  
  
8. Si está utilizando Visual C#:  
  
    1. En **el Explorador de soluciones**, haga clic en **Form1** en el **InheritanceTest** proyecto y, a continuación, elija **eliminar**. En el cuadro de mensaje que aparece, haga clic en **Aceptar** para confirmar la eliminación.  
  
    2. Abra el archivo Program.cs y cambie la línea `Application.Run(new Form1());` por `Application.Run(new Form2());`.  
  
9. En **el Explorador de soluciones**, haga clic en el **InheritanceTest** del proyecto y seleccione **establecer como proyecto de inicio**.  
  
10. En **el Explorador de soluciones**, haga clic en el **InheritanceTest** del proyecto y seleccione **propiedades**.  
  
11. En el **InheritanceTest** páginas de propiedades, establezca la **objeto Startup** sea el formulario heredado (**Form2**).  
  
12. Presione F5 para ejecutar la aplicación y observe el comportamiento del formulario heredado.  
  
## <a name="next-steps"></a>Pasos siguientes  
 La herencia de los controles de usuario funciona más o menos de la misma manera. Abra un proyecto nuevo de biblioteca de clases y agregue un control de usuario. Coloque en él controles constituyentes y compile el proyecto. Abra otro proyecto nuevo de biblioteca de clases y agregue una referencia a la biblioteca de clases compilada. Además, pruebe a agregar un control heredado (a través de la **agregar nuevos elementos** cuadro de diálogo) al proyecto y el uso de la **selector de herencia**. Agregue un control de usuario y cambie la `Inherits` (`:` en Visual C#) instrucción. Para obtener más información, vea [Cómo: Heredar formularios Windows](how-to-inherit-windows-forms.md).  
  
## <a name="see-also"></a>Vea también

- [Cómo: Heredar Windows Forms](how-to-inherit-windows-forms.md)
- [Herencia visual de Windows Forms](windows-forms-visual-inheritance.md)
- [Windows Forms](../index.md)
