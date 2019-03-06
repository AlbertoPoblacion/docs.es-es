---
title: 'Tutorial: Incrustar los tipos de los ensamblados administrados en Visual Studio (Visual Basic)'
ms.date: 07/20/2015
ms.assetid: 56ed12ba-adff-4e9c-a668-7fcba80c4795
ms.openlocfilehash: 836d035aab06f18c13e3675fbd72c5ab9879a3d2
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2019
ms.locfileid: "57359472"
---
# <a name="walkthrough-embedding-types-from-managed-assemblies-in-visual-studio-visual-basic"></a>Tutorial: Incrustar los tipos de los ensamblados administrados en Visual Studio (Visual Basic)

Si inserta información de tipos de un ensamblado administrado con nombre seguro, puede acoplar tipos holgadamente en una aplicación para lograr independencia de versiones. Es decir, el programa puede escribirse de modo que use tipos de varias versiones de una biblioteca administrada sin tener que volver a compilarse para cada versión.

La inserción de tipos se usa a menudo con interoperabilidad COM, como, por ejemplo, una aplicación que use objetos de automatización de Microsoft Office. La inserción de información de tipos permite que la misma versión de un programa funcione con distintas versiones de Microsoft Office en equipos diferentes. Pero la inserción de tipos también se puede usar con una solución totalmente administrada.

La información de tipos puede insertarse de un ensamblado que tenga las siguientes características:

- El ensamblado expone al menos una interfaz pública.

- Las interfaces insertadas se anotan con un atributo `ComImport` y un atributo `Guid` (y un GUID único).

- El ensamblado se anota con los atributos `ImportedFromTypeLib` o `PrimaryInteropAssembly` y un atributo `Guid` de nivel de ensamblado. (De forma predeterminada, las plantillas de proyecto de Visual Basic incluyen un nivel de ensamblado `Guid` atributo.)

Después de especificar las interfaces públicas que se pueden insertar, puede crear clases en tiempo de ejecución que implementen esas interfaces. Un programa cliente puede luego incrustar la información de tipo de dichas interfaces en tiempo de diseño haciendo referencia al ensamblado que contiene la configuración y las interfaces públicas de la propiedad `Embed Interop Types` de la referencia a `True`. Esto equivale a usar el compilador de línea de comandos y hacer referencia al ensamblado mediante la opción `/link` del compilador. El programa cliente puede luego cargar instancias de los objetos en tiempo de ejecución escritos como esas interfaces. Si crea otra versión del ensamblado en tiempo de ejecución con nombre seguro, el programa cliente no tiene que volver a compilarse con el ensamblado en tiempo de ejecución actualizado. En su lugar, el programa cliente sigue usando cualquier versión del ensamblado en tiempo de ejecución que encuentre disponible y usa la información de tipo insertada para las interfaces públicas.

Dado que la función principal de la inserción de tipos es admitir la inserción de información de tipos de ensamblados de interoperabilidad COM, cuando se inserta información de tipos en una solución totalmente administrada se aplican las siguientes limitaciones:

- Solo se insertan los atributos específicos de interoperabilidad COM; se omiten otros atributos.

- Si un tipo usa parámetros genéricos y el tipo del parámetro genérico es un tipo insertado, ese tipo no se puede usar más allá de un límite de ensamblado. Entre los ejemplos de cruce de un límite de ensamblado se incluyen llamar a un método desde otro ensamblado o derivar un tipo de un tipo definido en otro ensamblado.

- Las constantes no se insertan.

- La clase <xref:System.Collections.Generic.Dictionary%602?displayProperty=nameWithType> no admite un tipo insertado como clave. Puede implementar su propio tipo de diccionario que admita un tipo insertado como clave.

 En este tutorial, se realizarán las siguientes tareas:

- Crear un ensamblado con nombre seguro que tenga una interfaz pública e incluya información de tipo que se puede insertar.

- Crear un ensamblado en tiempo de ejecución con nombre seguro que implemente esa interfaz pública.

- Crear un programa cliente que inserte la información de tipo de la interfaz pública y cree una instancia de la clase del ensamblado en tiempo de ejecución.

- Modificar y recompilar el ensamblado en tiempo de ejecución.

- Ejecute el programa cliente para ver que se usa la nueva versión del ensamblado en tiempo de ejecución sin tener que recompilar el programa cliente.

[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]

## <a name="creating-an-interface"></a>Creación de una interfaz

#### <a name="to-create-the-type-equivalence-interface-project"></a>Para crear el proyecto de interfaz de equivalencia de tipos

1. En el menú **Archivo** de Visual Studio, apunte a **Nuevo** y haga clic en **Proyecto**.

2. En el panel **Tipos de proyecto** del cuadro de diálogo **Nuevo proyecto**, asegúrese de que esté seleccionado **Windows**. Seleccione **Biblioteca de clases** en el panel **Plantillas**. En el cuadro **Nombre**, escriba `TypeEquivalenceInterface` y haga clic en **Aceptar**. Se crea el proyecto.

3. En **el Explorador de soluciones**, haga clic en el archivo Class1.vb y haga clic en **cambiar el nombre**. Cambie el nombre del archivo a `ISampleInterface.vb` y pulse ENTRAR. Al cambiar el nombre del archivo también se cambiará el nombre de la clase a `ISampleInterface`. Esta clase representará la interfaz pública de la clase.

4. Haga clic con el botón derecho en el proyecto TypeEquivalenceInterface y haga clic en **Propiedades**. Haga clic en la pestaña **Compilar**. Establezca la ruta de acceso de salida en una ubicación válida en el equipo de desarrollo, como `C:\TypeEquivalenceSample`. Esta ubicación también se usará en un paso posterior en este tutorial.

5. Mientras sigue editando las propiedades del proyecto, haga clic en la pestaña **Firma**. Seleccione la opción **Firmar el ensamblado**. En la lista **Elija un archivo de clave de nombre seguro**, haga clic en **<Nuevo...>**. En el cuadro **Nombre del archivo de clave**, escriba `key.snk`. Desactive la casilla **Proteger mi archivo de clave mediante contraseña**. Haga clic en **Aceptar**.

6. Abra el archivo ISampleInterface.vb. Agregue el código siguiente al archivo de clase ISampleInterface para crear la interfaz ISampleInterface.

    ```vb
    Imports System.Runtime.InteropServices

    <ComImport()>
    <Guid("8DA56996-A151-4136-B474-32784559F6DF")>
    Public Interface ISampleInterface
        Sub GetUserInput()
        ReadOnly Property UserInput As String
    End Interface
    ```

7. En el menú **Herramientas**, haga clic en **Crear GUID**. En el cuadro de diálogo **Crear GUID**, haga clic en **Formato de Registro** y luego en **Copiar**. Haga clic en **Salir**.

8. En el atributo `Guid`, elimine el GUID de ejemplo y pegue el GUID que ha copiado del cuadro de diálogo **Crear GUID**. Quite las llaves ({}) del GUID copiado.

9. En el menú **Proyecto**, haga clic en **Mostrar todos los archivos**.

10. En **el Explorador de soluciones**, expanda el **mi proyecto** carpeta. Haga doble clic en el AssemblyInfo.vb. Agregue el atributo siguiente al archivo.

    ```vb
    <Assembly: ImportedFromTypeLib("")>
    ```

    Guarde el archivo.

11. Guarde el proyecto.

12. Haga clic con el botón derecho en el proyecto TypeEquivalenceInterface y haga clic en **Compilar**. El archivo .dll de biblioteca de clases se compila y se guarda en la ruta de acceso de salida de la compilación especificada (por ejemplo, C:\TypeEquivalenceSample).

## <a name="creating-a-runtime-class"></a>Creación de una clase en tiempo de ejecución

#### <a name="to-create-the-type-equivalence-runtime-project"></a>Para crear el proyecto en tiempo de ejecución de equivalencia de tipos

1. En el menú **Archivo** de Visual Studio, apunte a **Nuevo** y haga clic en **Proyecto**.

2. En el panel **Tipos de proyecto** del cuadro de diálogo **Nuevo proyecto**, asegúrese de que esté seleccionado **Windows**. Seleccione **Biblioteca de clases** en el panel **Plantillas**. En el cuadro **Nombre**, escriba `TypeEquivalenceRuntime` y haga clic en **Aceptar**. Se crea el proyecto.

3. En **el Explorador de soluciones**, haga clic en el archivo Class1.vb y haga clic en **cambiar el nombre**. Cambie el nombre del archivo a `SampleClass.vb` y pulse ENTRAR. Al cambiar el nombre del archivo también se cambiará el nombre de la clase a `SampleClass`. Esta clase implementará la interfaz `ISampleInterface`.

4. Haga clic con el botón derecho en el proyecto TypeEquivalenceRuntime y haga clic en **Propiedades**. Haga clic en la pestaña **Compilar**. Establezca la ruta de acceso de salida en la misma ubicación que se usa en el proyecto TypeEquivalenceInterface, por ejemplo, `C:\TypeEquivalenceSample`.

5. Mientras sigue editando las propiedades del proyecto, haga clic en la pestaña **Firma**. Seleccione la opción **Firmar el ensamblado**. En la lista **Elija un archivo de clave de nombre seguro**, haga clic en **<Nuevo...>**. En el cuadro **Nombre del archivo de clave**, escriba `key.snk`. Desactive la casilla **Proteger mi archivo de clave mediante contraseña**. Haga clic en **Aceptar**.

6. Haga clic con el botón derecho en el proyecto TypeEquivalenceRuntime y haga clic en **Agregar referencia**. Haga clic en la pestaña **Examinar** y vaya a la carpeta de la ruta de acceso de salida. Seleccione el archivo TypeEquivalenceInterface.dll y haga clic en **Aceptar**.

7. En el menú **Proyecto**, haga clic en **Mostrar todos los archivos**.

8. En el **Explorador de soluciones**, expanda la carpeta **Referencias**. Seleccione la referencia TypeEquivalenceInterface. En la ventana Propiedades de la referencia TypeEquivalenceInterface, establezca la propiedad **Versión específica** en **False**.

9. Agregue el código siguiente al archivo de clase SampleClass para crear la clase SampleClass.

    ```vb
    Imports TypeEquivalenceInterface

    Public Class SampleClass
        Implements ISampleInterface

        Private p_UserInput As String
        Public ReadOnly Property UserInput() As String Implements ISampleInterface.UserInput
            Get
                Return p_UserInput
            End Get
        End Property

        Public Sub GetUserInput() Implements ISampleInterface.GetUserInput
            Console.WriteLine("Please enter a value:")
            p_UserInput = Console.ReadLine()
        End Sub
    End Class
    ```

10. Guarde el proyecto.

11. Haga clic con el botón derecho en el proyecto TypeEquivalenceRuntime y haga clic en **Compilar**. El archivo .dll de biblioteca de clases se compila y se guarda en la ruta de acceso de salida de la compilación especificada (por ejemplo, C:\TypeEquivalenceSample).

## <a name="creating-a-client-project"></a>Creación de un proyecto de cliente

#### <a name="to-create-the-type-equivalence-client-project"></a>Para crear el proyecto de cliente de equivalencia de tipos

1. En el menú **Archivo** de Visual Studio, apunte a **Nuevo** y haga clic en **Proyecto**.

2. En el panel **Tipos de proyecto** del cuadro de diálogo **Nuevo proyecto**, asegúrese de que esté seleccionado **Windows**. Seleccione **Aplicación de consola** en el panel **Plantillas**. En el cuadro **Nombre**, escriba `TypeEquivalenceClient` y haga clic en **Aceptar**. Se crea el proyecto.

3. Haga clic con el botón derecho en el proyecto TypeEquivalenceClient y haga clic en **Propiedades**. Haga clic en la pestaña **Compilar**. Establezca la ruta de acceso de salida en la misma ubicación que se usa en el proyecto TypeEquivalenceInterface, por ejemplo, `C:\TypeEquivalenceSample`.

4. Haga clic con el botón derecho en el proyecto TypeEquivalenceClient y haga clic en **Agregar referencia**. Haga clic en la pestaña **Examinar** y vaya a la carpeta de la ruta de acceso de salida. Seleccione el archivo TypeEquivalenceInterface.dll file (no el TypeEquivalenceRuntime.dll) y haga clic en **Aceptar**.

5. En el menú **Proyecto**, haga clic en **Mostrar todos los archivos**.

6. En el **Explorador de soluciones**, expanda la carpeta **Referencias**. Seleccione la referencia TypeEquivalenceInterface. En la ventana Propiedades de la referencia TypeEquivalenceInterface, establezca la propiedad **Incrustar tipos de interoperabilidad** en **True**.

7. Agregue el código siguiente al archivo Module1.vb para crear el programa cliente.

    ```vb
    Imports TypeEquivalenceInterface
    Imports System.Reflection

    Module Module1

        Sub Main()
            Dim sampleAssembly = Assembly.Load("TypeEquivalenceRuntime")
            Dim sampleClass As ISampleInterface = CType( _
                sampleAssembly.CreateInstance("TypeEquivalenceRuntime.SampleClass"), ISampleInterface)
            sampleClass.GetUserInput()
            Console.WriteLine(sampleClass.UserInput)
            Console.WriteLine(sampleAssembly.GetName().Version)
            Console.ReadLine()
        End Sub

    End Module
    ```

8. Pulse CTRL+F5 para compilar y ejecutar el programa.

## <a name="modifying-the-interface"></a>Modificación de la interfaz

#### <a name="to-modify-the-interface"></a>Para modificar la interfaz

1. En el menú **Archivo** de Visual Studio, apunte a **Abrir** y haga clic en **Proyecto o solución**.

2. En el cuadro de diálogo **Abrir proyecto**, haga clic con el botón derecho en el proyecto TypeEquivalenceInterface y haga clic en **Propiedades**. Haga clic en la pestaña **Aplicación** . Haga clic en el botón **Información de ensamblado**. Cambie los valores de **Versión de ensamblado** y **Versión de archivo** a `2.0.0.0`.

3. Abra el archivo ISampleInterface.vb. Agregue la línea de código siguiente a la interfaz ISampleInterface.

    ```vb
    Function GetDate() As Date
    ```

    Guarde el archivo.

4. Guarde el proyecto.

5. Haga clic con el botón derecho en el proyecto TypeEquivalenceInterface y haga clic en **Compilar**. Una nueva versión del archivo .dll de biblioteca de clases se compila y se guarda en la ruta de acceso de salida de la compilación especificada (por ejemplo, C:\TypeEquivalenceSample).

## <a name="modifying-the-runtime-class"></a>Modificación de la clase en tiempo de ejecución

#### <a name="to-modify-the-runtime-class"></a>Para modificar la clase en tiempo de ejecución

1. En el menú **Archivo** de Visual Studio, apunte a **Abrir** y haga clic en **Proyecto o solución**.

2. En el cuadro de diálogo **Abrir proyecto**, haga clic con el botón derecho en el proyecto TypeEquivalenceRuntime y haga clic en **Propiedades**. Haga clic en la pestaña **Aplicación** . Haga clic en el botón **Información de ensamblado**. Cambie los valores de **Versión de ensamblado** y **Versión de archivo** a `2.0.0.0`.

3. Abra el archivo SampleClass.vb. Agregue las líneas de código siguientes a la clase SampleClass.

```vb
Public Function GetDate() As DateTime Implements ISampleInterface.GetDate
    Return Now
End Function
```

    Save the file.

4. Guarde el proyecto.

5. Haga clic con el botón derecho en el proyecto TypeEquivalenceRuntime y haga clic en **Compilar**. Una versión actualizada del archivo .dll de biblioteca de clases se compila y se guarda en la ruta de acceso de salida de la compilación especificada anteriormente (por ejemplo, C:\TypeEquivalenceSample).

6. En el Explorador de archivos, abra la carpeta de la ruta de acceso de salida (por ejemplo, C:\TypeEquivalenceSample). Haga doble clic en el archivo TypeEquivalenceClient.exe para ejecutar el programa. El programa reflejará la nueva versión del ensamblado TypeEquivalenceRuntime sin tener que volver a compilarse de nuevo.

## <a name="see-also"></a>Vea también

- [/link (Visual Basic)](../../../../visual-basic/reference/command-line-compiler/link.md)
- [Conceptos de programación](../../../../visual-basic/programming-guide/concepts/index.md)
- [Programar con ensamblados](../../../../framework/app-domains/programming-with-assemblies.md)
- [Ensamblados de .NET](../../../../standard/assembly/index.md)
