---
title: 'Tutorial: Crear contenido Direct3D9 para hospedarlo en WPF'
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- WPF [WPF], creating Direct3D9 content
- Direct3D9 [WPF interoperability], creating Direct3D9 content
ms.assetid: 286e98bc-1eaa-4b5e-923d-3490a9cca5fc
ms.openlocfilehash: 160395b84ef7ca447d162ceff34752113a1d59a9
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59300273"
---
# <a name="walkthrough-creating-direct3d9-content-for-hosting-in-wpf"></a>Tutorial: Crear contenido Direct3D9 para hospedarlo en WPF
Este tutorial muestra cómo crear contenido Direct3D9 que es adecuado para el hospedaje en una aplicación de Windows Presentation Foundation (WPF). Para obtener más información sobre hospedar contenido Direct3D9 en aplicaciones de WPF, vea [interoperabilidad entre Direct3D9 y WPF](wpf-and-direct3d9-interoperation.md).

 En este tutorial, realizará las tareas siguientes:

-   Cree un proyecto de Direct3D9.

-   Configurar el proyecto de Direct3D9 para hospedarlo en una aplicación de WPF.

 Cuando haya terminado, tendrá un archivo DLL que contiene contenido Direct3D9 para su uso en una aplicación WPF.

## <a name="prerequisites"></a>Requisitos previos
 Necesita los componentes siguientes para completar este tutorial:

-   Visual Studio 2010.

-   DirectX SDK 9 o posterior.

## <a name="creating-the-direct3d9-project"></a>Crear el proyecto de Direct3D9
 El primer paso es crear y configurar el proyecto de Direct3D9.

#### <a name="to-create-the-direct3d9-project"></a>Para crear el proyecto de Direct3D9

1. Cree un nuevo proyecto de Win32 en C++ denominado `D3DContent`.

     El Asistente para aplicaciones de Win32 se abre y muestra la pantalla de bienvenida.

2. Haga clic en **Siguiente**.

     Aparecerá la pantalla de configuración de la aplicación.

3. En el **tipo de aplicación:** sección, seleccione el **DLL** opción.

4. Haga clic en **Finalizar**.

     Se genera el proyecto D3DContent.

5. En el Explorador de soluciones, haga clic en el proyecto D3DContent y seleccione **propiedades**.

     El **páginas de propiedades de D3DContent** abre el cuadro de diálogo.

6. Seleccione el **C o C++** nodo.

7. En el **directorios de inclusión adicionales** , especifique la ubicación de DirectX incluir carpeta. La ubicación predeterminada de esta carpeta es %ProgramFiles%\Microsoft DirectX SDK (*versión*) \Include.

8. Haga doble clic en el **vinculador** nodo para expandirlo.

9. En el **directorios de bibliotecas adicionales** , especifique la ubicación de la carpeta de bibliotecas de DirectX. La ubicación predeterminada de esta carpeta es %ProgramFiles%\Microsoft DirectX SDK (*versión*) \Lib\x86.

10. Seleccione el **entrada** nodo.

11. En el **dependencias adicionales** campo, agregue el `d3d9.lib` y `d3dx9.lib` archivos.

12. En el Explorador de soluciones, agregue un nuevo archivo de definición de módulo (.def) denominado `D3DContent.def` al proyecto.

## <a name="creating-the-direct3d9-content"></a>Crear contenido Direct3D9
 Para obtener el mejor rendimiento, el contenido Direct3D9 debe utilizar valores determinados. El código siguiente muestra cómo crear una superficie de Direct3D9 con las mejores características de rendimiento. Para obtener más información, consulte [consideraciones de rendimiento para la interoperabilidad de WPF y Direct3D9](performance-considerations-for-direct3d9-and-wpf-interoperability.md).

#### <a name="to-create-the-direct3d9-content"></a>Para crear contenido de la Direct3D9

1. Mediante el Explorador de soluciones, agregue tres clases de C++ al proyecto denominado lo siguiente.

     `CRenderer` (con destructor virtual)

     `CRendererManager`

     `CTriangleRenderer`

2. Abra Renderer.h en el Editor de código y reemplace el código generado automáticamente por el código siguiente.

     [!code-cpp[System.Windows.Interop.D3DImage#RendererH](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.h#rendererh)]

3. Abra Renderer.cpp en el Editor de código y reemplace el código generado automáticamente por el código siguiente.

     [!code-cpp[System.Windows.Interop.D3DImage#RendererCPP](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.cpp#renderercpp)]

4. Abra RendererManager.h en el Editor de código y reemplace el código generado automáticamente por el código siguiente.

     [!code-cpp[System.Windows.Interop.D3DImage#RendererManagerH](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.h#renderermanagerh)]

5. Abra RendererManager.cpp en el Editor de código y reemplace el código generado automáticamente por el código siguiente.

     [!code-cpp[System.Windows.Interop.D3DImage#RendererManagerCPP](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanagercpp)]

6. Abra TriangleRenderer.h en el Editor de código y reemplace el código generado automáticamente por el código siguiente.

     [!code-cpp[System.Windows.Interop.D3DImage#TriangleRendererH](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/trianglerenderer.h#trianglerendererh)]

7. Abra TriangleRenderer.cpp en el Editor de código y reemplace el código generado automáticamente por el código siguiente.

     [!code-cpp[System.Windows.Interop.D3DImage#TriangleRendererCPP](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/trianglerenderer.cpp#trianglerenderercpp)]

8. Abra stdafx.h en el Editor de código y reemplace el código generado automáticamente por el código siguiente.

     [!code-cpp[System.Windows.Interop.D3DImage#StdafxH](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/stdafx.h#stdafxh)]

9. Abra el Editor de código de dllmain.cpp y reemplace el código generado automáticamente por el código siguiente.

     [!code-cpp[System.Windows.Interop.D3DImage#DllMain](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/dllmain.cpp#dllmain)]

10. Abra D3DContent.def en el editor de código.

11. Reemplace el código generado automáticamente por el código siguiente.

    ```
    LIBRARY "D3DContent"

    EXPORTS

    SetSize
    SetAlpha
    SetNumDesiredSamples
    SetAdapter

    GetBackBufferNoRef
    Render
    Destroy
    ```

12. Compile el proyecto.

## <a name="next-steps"></a>Pasos siguientes

-   Hospedar contenido Direct3D9 en una aplicación WPF. Para obtener más información, vea [Tutorial: Hospedar contenido Direct3D9 en WPF](walkthrough-hosting-direct3d9-content-in-wpf.md).

## <a name="see-also"></a>Vea también

- <xref:System.Windows.Interop.D3DImage>
- [Consideraciones de rendimiento para la interoperabilidad entre Direct3D9 y WPF](performance-considerations-for-direct3d9-and-wpf-interoperability.md)
- [Tutorial: Hospedar contenido Direct3D9 en WPF](walkthrough-hosting-direct3d9-content-in-wpf.md)
