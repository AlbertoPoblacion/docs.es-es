---
title: 'Procedimiento Utilizar el espacio de nombres My: Guía de programación de C#'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, My namespace access
ms.assetid: e7152414-0ea5-4c8e-bf02-c8d5bbe45ff4
ms.openlocfilehash: 9621f6a01ef4e30bf34b97df3d2c3033e9b62a23
ms.sourcegitcommit: 558d78d2a68acd4c95ef23231c8b4e4c7bac3902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2019
ms.locfileid: "59316029"
---
# <a name="how-to-use-the-my-namespace-c-programming-guide"></a>Procedimiento Utilizar el espacio de nombres My (Guía de programación de C#)
El espacio de nombres <xref:Microsoft.VisualBasic.MyServices> (`My` en Visual Basic) proporciona acceso fácil e intuitivo a una serie de clases de .NET Framework, lo que le permite escribir código que interactúe con el equipo, la aplicación, la configuración, los recursos, etc. Aunque se diseñó originalmente para usarse con Visual Basic, el espacio de nombres `MyServices` puede usarse en aplicaciones de C#.  
  
 Para obtener más información sobre el uso del espacio de nombres `MyServices` de Visual Basic, consulte [Development with My](../../../visual-basic/developing-apps/development-with-my/index.md) (Desarrollo con My).  
  
## <a name="adding-a-reference"></a>Agregar una referencia  
 Para poder usar las clases `MyServices` en la solución, debe agregar una referencia a la biblioteca de Visual Basic.  
  
#### <a name="to-add-a-reference-to-the-visual-basic-library"></a>Para agregar una referencia a la biblioteca de Visual Basic  
  
1. En el **Explorador de soluciones**, haga clic con el botón derecho en el nodo **Referencias** y seleccione **Agregar referencia**.  
  
2. Cuando aparezca el cuadro de diálogo **Referencias**, desplácese hacia abajo en la lista y seleccione Microsoft.VisualBasic.dll.  
  
     También es posible que quiera incluir la siguiente línea en la sección `using` al principio del programa.  
  
     [!code-csharp[csProgGuideNamespaces#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces3.cs#18)]  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo, se llama a distintos métodos estáticos contenidos en el espacio de nombres `MyServices`. Para que pueda compilar este código, debe agregarse al proyecto una referencia a Microsoft.VisualBasic.DLL.  
  
 [!code-csharp[csProgGuideNamespaces#19](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces3.cs#19)]  
  
 No se puede llamar a todas las clases en el espacio de nombres `MyServices` desde una aplicación de C#: por ejemplo, la clase <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy> no es compatible. En este caso concreto, los métodos estáticos que forman parte de <xref:Microsoft.VisualBasic.FileIO.FileSystem>, que también se incluyen en el archivo VisualBasic.dll, pueden usarse en su lugar. Por ejemplo, aquí se muestra cómo usar uno de estos métodos para duplicar un directorio:  
  
 [!code-csharp[csProgGuideNamespaces#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces3.cs#20)]  
  
## <a name="see-also"></a>Vea también

- [Guía de programación de C#](../../../csharp/programming-guide/index.md)
- [Espacios de nombres](../../../csharp/programming-guide/namespaces/index.md)
- [Uso de espacios de nombres](../../../csharp/programming-guide/namespaces/using-namespaces.md)
