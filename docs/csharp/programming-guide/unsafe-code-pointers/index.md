---
title: 'Código no seguro y punteros: Guía de programación de C#'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- security [C#], type safety
- C# language, unsafe code
- type safety [C#]
- unsafe keyword [C#]
- unsafe code [C#]
- C# language, pointers
- pointers [C#], about pointers
ms.assetid: b0fcca10-a92d-4f2a-835b-b0ccae6739ee
ms.openlocfilehash: 9f4e74e1e8fa71d1492a10162191822c1edfb635
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2019
ms.locfileid: "64608040"
---
# <a name="unsafe-code-and-pointers-c-programming-guide"></a>Código no seguro y punteros (Guía de programación de C#)
Para mantener la seguridad de tipos, C# no admite la aritmética de puntero de forma predeterminada. En cambio, mediante el uso de la palabra clave [unsafe](../../../csharp/language-reference/keywords/unsafe.md), puede definir un contexto no seguro en el que se pueden usar punteros. Para obtener más información sobre los punteros, vea [Tipos de puntero](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md).  
  
> [!NOTE]
>  En Common Language Runtime (CLR), el código no seguro se conoce como código no comprobable. El código no seguro en C# no es necesariamente peligroso; solo es código cuya seguridad no puede comprobar CLR. Por lo tanto, CLR solo ejecutará código no seguro si se encuentra en un ensamblado de plena confianza. Si usa código no seguro, es su responsabilidad asegurarse de que el código no presenta riesgos de seguridad o errores de puntero.  
  
## <a name="unsafe-code-overview"></a>Información general sobre el código no seguro  
 El código no seguro tiene las propiedades siguientes:  
  
- Los métodos, tipos y bloques de código se pueden definir como no seguros.  
  
- En algunos casos, el código no seguro puede aumentar el rendimiento de la aplicación al eliminar las comprobaciones de límites de matriz.  
  
- El código no seguro es necesario al llamar a funciones nativas que requieren punteros.  
  
- El código no seguro presenta riesgos para la seguridad y la estabilidad.  
  
- Para que C# compile código no seguro, la aplicación debe compilarse con [/unsafe](../../../csharp/language-reference/compiler-options/unsafe-compiler-option.md).  
  
## <a name="related-sections"></a>Secciones relacionadas  
 Para obtener más información, consulte:  
  
- [Tipos de puntero](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)  
  
- [Búferes de tamaño fijo](../../../csharp/programming-guide/unsafe-code-pointers/fixed-size-buffers.md)  
  
- [Cómo: Utilizar punteros para copiar una matriz de bytes](../../../csharp/programming-guide/unsafe-code-pointers/how-to-use-pointers-to-copy-an-array-of-bytes.md)  
  
- [unsafe](../../../csharp/language-reference/keywords/unsafe.md)  
  
## <a name="c-language-specification"></a>Especificación del lenguaje C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vea también

- [Guía de programación de C#](../../../csharp/programming-guide/index.md)
