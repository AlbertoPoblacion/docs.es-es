---
title: 'Tutorial: Depurar controles personalizados de formularios Windows Forms en tiempo de diseño'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- debugging [Visual Studio], walkthroughs
- custom controls [Windows Forms], walkthroughs
- visual editors
- debugging [Visual Studio], Windows Forms
- custom controls [Windows Forms], debugging
- designers
- controls [Windows Forms], debugging
- walkthroughs [Windows Forms], debugging
- design-time debugging
ms.assetid: 1fd83ccd-3798-42fc-85a3-6cba99467387
ms.openlocfilehash: a8f228d334785cd880b06dbeda8f96550471599a
ms.sourcegitcommit: 0d0a6e96737dfe24d3257b7c94f25d9500f383ea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2019
ms.locfileid: "65211547"
---
# <a name="walkthrough-debugging-custom-windows-forms-controls-at-design-time"></a>Tutorial: Depurar controles personalizados de formularios Windows Forms en tiempo de diseño

Cuando se crea un control personalizado, a menudo encontrará lo necesario para depurar su comportamiento en tiempo de diseño. Esto es especialmente cierto si va a crear un diseñador personalizado para el control personalizado. Para obtener más información, consulte [Tutorial: Crear un Windows Forms Control que aprovecha las características de tiempo de diseño de Visual Studio](creating-a-wf-control-design-time-features.md).

Puede depurar sus controles personalizados mediante Visual Studio, simplemente como lo haría cualquier otras clases de .NET Framework. La diferencia es que desea depurar una instancia independiente de Visual Studio que se está ejecutando código del control personalizado

Las tareas ilustradas en este tutorial incluyen:

- Crear un proyecto de Windows Forms para hospedar el control personalizado

- Crear un proyecto de biblioteca de controles

- Agregar una propiedad al control personalizado

- Agregar el control personalizado al formulario de host

- Configurar el proyecto para la depuración de tiempo de diseño

- Depurar el control personalizado en tiempo de diseño

Cuando haya terminado, tendrá una comprensión de las tareas necesarias para depurar el comportamiento en tiempo de diseño de un control personalizado.

## <a name="create-the-project"></a>Crear el proyecto

El primer paso es crear el proyecto de aplicación. Este proyecto se utilizará para compilar la aplicación que hospeda el control personalizado.

En Visual Studio, cree un proyecto de aplicación de Windows denominado "DebuggingExample" (**archivo** > **New** > **proyecto**  >  **Visual C#**  o **Visual Basic** > **escritorio clásico de** > **deaplicacióndeformulariosdeWindows**).

## <a name="create-the-control-library-project"></a>Crear el proyecto de biblioteca de controles

1. Agregar un **biblioteca de controles de Windows** proyecto a la solución.

2. Agregue un nuevo **UserControl** al proyecto DebugControlLibrary. Para obtener más detalles, vea [Cómo: Agregar nuevos elementos de proyecto](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/w0572c5b(v=vs.100)). Asigne el nuevo archivo de origen en un nombre de base de "DebugControl".

3. Mediante el **el Explorador de soluciones**, elimine el control predeterminado del proyecto eliminando el archivo de código con el nombre de base "`UserControl1`". Para obtener más detalles, vea [Cómo: Quitar, eliminar y excluir elementos](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/0ebzhwsk(v=vs.100)).

4. Compile la solución.

## <a name="checkpoint"></a>Punto de control

En este momento, podrá ver el control personalizado en el **cuadro de herramientas**.

Para comprobar el progreso, busque la nueva ficha denominada **DebugControlLibrary componentes** y haga clic para seleccionarlo. Cuando se abre, verá el control aparece como **DebugControl** con el icono predeterminado junto a él.

## <a name="add-a-property-to-your-custom-control"></a>Agregar una propiedad al control personalizado

Para demostrar que se está ejecutando código del control personalizado en tiempo de diseño, agregará una propiedad y establecer un punto de interrupción en el código que implementa la propiedad.

1. Abra **DebugControl** en el **Editor de código**. Agregue el código siguiente a la definición de clase:

    ```vb
    Private demoStringValue As String = Nothing
    <BrowsableAttribute(true)>
    Public Property DemoString() As String

        Get
            Return Me.demoStringValue
        End Get

        Set(ByVal value As String)
            Me.demoStringValue = value
        End Set

    End Property
    ```

    ```csharp
    private string demoStringValue = null;
    [Browsable(true)]
    public string DemoString
    {
        get
        {
            return this.demoStringValue;
        }
        set
        {
            demoStringValue = value;
        }
    }
    ```

2. Compile la solución.

## <a name="add-your-custom-control-to-the-host-form"></a>Agregar el control personalizado al formulario de host

Para depurar el comportamiento en tiempo de diseño del control personalizado, colocará una instancia de la clase de control personalizado en un formulario de host.

1. En el proyecto "DebuggingExample", abra Form1 en el **Diseñador de Windows Forms**.

2. En el **cuadro de herramientas**, abra el **DebugControlLibrary componentes** pestaña y arrastre un **DebugControl** instancia hasta el formulario.

3. Buscar el `DemoString` propiedad personalizada en el **propiedades** ventana. Tenga en cuenta que puede cambiar su valor como lo haría con cualquier otra propiedad. Tenga en cuenta también que, cuando el `DemoString` propiedad está seleccionada, la cadena de descripción de la propiedad aparece en la parte inferior de la **propiedades** ventana.

## <a name="set-up-the-project-for-design-time-debugging"></a>Configurar el proyecto para la depuración de tiempo de diseño

Para depurar el comportamiento en tiempo de diseño del control personalizado, que desea depurar una instancia independiente de Visual Studio que se está ejecutando código del control personalizado.

1. Haga doble clic en el **DebugControlLibrary** del proyecto en el **el Explorador de soluciones** y seleccione **propiedades**.

2. En el **DebugControlLibrary** hoja de propiedades, seleccione la **depurar** ficha.

     En el **acción de inicio** sección, seleccione **iniciar programa externo**. Puede depurar una instancia independiente de Visual Studio, haga clic en el botón de puntos suspensivos (![de pantalla de VisualStudioEllipsesButton](../media/vbellipsesbutton.png "vbEllipsesButton")) botón para buscar el IDE de Visual Studio. El nombre del archivo ejecutable es **devenv.exe**, y si ha instalado en la ubicación predeterminada, su ruta de acceso es %programfiles%\Microsoft Visual Studio 9.0\Common7\IDE\devenv.exe.

3. Haga clic en **Aceptar** para cerrar el cuadro de diálogo.

4. Haga clic en el **DebugControlLibrary** del proyecto y seleccione **establecer como proyecto de inicio** para habilitar esta configuración de depuración.

## <a name="debug-your-custom-control-at-design-time"></a>Depurar el control personalizado en tiempo de diseño

Ahora está listo para depurar el control personalizado mientras se ejecuta en modo de diseño. Al iniciar la sesión de depuración, se creará una nueva instancia de Visual Studio y se usará para cargar la solución "DebuggingExample". Cuando se abre Form1 en el **Diseñador de formularios**, una instancia del control personalizado se crea y se volverá a ejecutarse.

1. Abra el **DebugControl** archivo de código fuente en el **Editor de código** y coloque un punto de interrupción en el `Set` descriptor de acceso de la `DemoString` propiedad.

2. Presione F5 para iniciar la sesión de depuración. Tenga en cuenta que se crea una nueva instancia de Visual Studio. Puede distinguir entre las instancias de dos maneras:

    - La instancia de depuración con la palabra **ejecutando** en su barra de título

    - La instancia de depuración tiene el **iniciar** situado en su **depurar** deshabilitado de la barra de herramientas

     El punto de interrupción se establece en la instancia de depuración.

3. En la nueva instancia de Visual Studio, abra la solución "DebuggingExample". Puede encontrar fácilmente la solución seleccionando **proyectos recientes** desde el **archivo** menú. El archivo de solución "DebuggingExample.sln" se mostrará como los archivos usados recientemente.

4. Abra Form1 en el **Diseñador de formularios** y seleccione el **DebugControl** control.

5. Cambie el valor de la propiedad `DemoString` . Tenga en cuenta que cuando se confirma el cambio, la instancia de depuración de Visual Studio adquiere el foco y la ejecución se detiene en el punto de interrupción. Puede paso a paso a través del descriptor de acceso de propiedad al igual que su cualquier otro código.

6. Cuando haya terminado con la sesión de depuración, puede salir descartando la instancia hospedada de Visual Studio o haciendo clic en el **Detener depuración** botón en la instancia de depuración.

## <a name="next-steps"></a>Pasos siguientes

Ahora que puede depurar controles personalizados en tiempo de diseño, hay muchas posibilidades para expandir la interacción del control con el IDE de Visual Studio.

- Puede usar el <xref:System.ComponentModel.Component.DesignMode%2A> propiedad de la <xref:System.ComponentModel.Component> clase para escribir código que solo se ejecutará en tiempo de diseño. Para obtener información detallada, vea <xref:System.ComponentModel.Component.DesignMode%2A>.

- Hay varios atributos puede aplicar a las propiedades del control para manipular la interacción del control personalizado con el diseñador. Puede encontrar estos atributos en el <xref:System.ComponentModel?displayProperty=nameWithType> espacio de nombres.

- Puede escribir un diseñador personalizado para el control personalizado. Esto le ofrece control completo sobre la experiencia de diseño mediante la infraestructura del diseñador extensible expuesta por Visual Studio. Para obtener más información, consulte [Tutorial: Crear un Windows Forms Control que aprovecha las características de tiempo de diseño de Visual Studio](creating-a-wf-control-design-time-features.md).

## <a name="see-also"></a>Vea también

- [Tutorial: Crear un Control de Windows Forms que aproveche las características de tiempo de diseño de Visual Studio](creating-a-wf-control-design-time-features.md)
- [Cómo: Acceso a servicios en tiempo de diseño](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/ms171822(v=vs.120))
- [Cómo: Compatibilidad de tiempo de diseño de acceso en Windows Forms](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/ms171827(v=vs.120))
