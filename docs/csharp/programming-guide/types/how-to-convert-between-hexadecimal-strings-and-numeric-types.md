---
title: 'Procedimiento Convertir cadenas hexadecimales en tipos numéricos: Guía de programación de C#'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- hexadecimal strings [C#], converting to numeric type
- conversions [C#], hexidecimal strings
- strings [C#], converting hexadecimal strings
- hexadecimal strings [C#]
ms.assetid: 7115c49f-7d1d-40c3-8bd9-aae0cc1d46b6
ms.openlocfilehash: 99d30d6c2b50569312ff2d732a34020ab29ce81c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2019
ms.locfileid: "64595069"
---
# <a name="how-to-convert-between-hexadecimal-strings-and-numeric-types-c-programming-guide"></a>Procedimiento Convertir cadenas hexadecimales en tipos numéricos (Guía de programación de C#)
En estos ejemplos se muestra cómo realizar las tareas siguientes:  
  
- Obtener el valor hexadecimal de cada uno de los caracteres de un elemento [string](../../../csharp/language-reference/keywords/string.md).  
  
- Obtener el elemento [char](../../../csharp/language-reference/keywords/char.md) que corresponde a cada valor de una cadena hexadecimal.  
  
- Convertir un elemento `string` hexadecimal en un elemento [int](../../../csharp/language-reference/keywords/int.md).  
  
- Convertir un elemento `string` hexadecimal en un elemento [float](../../../csharp/language-reference/keywords/float.md).  
  
- Convertir una matriz de [bytes](../../../csharp/language-reference/keywords/byte.md) en un elemento `string` hexadecimal.  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo se genera el valor hexadecimal de cada uno de los caracteres de `string`. Primero, analiza `string` como una matriz de caracteres. Después, llama a <xref:System.Convert.ToInt32%28System.Char%29> en cada carácter para obtener su valor numérico. Finalmente, aplica formato al número como su representación hexadecimal en un elemento `string`.  
  
 [!code-csharp[csProgGuideTypes#30](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#30)]  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo se analiza un elemento `string` de valores hexadecimales y genera el carácter correspondiente a cada valor hexadecimal. Primero, llama al método [Split(Char\[\])](xref:System.String.Split(System.Char[])) para obtener cada valor hexadecimal como un elemento `string` individual en una matriz. Después, llama a <xref:System.Convert.ToInt32%28System.String%2CSystem.Int32%29> para convertir el valor hexadecimal a un valor decimal representado como [int](../../../csharp/language-reference/keywords/int.md). Muestra dos maneras distintas de obtener el carácter correspondiente a ese código de carácter. En la primera técnica se usa <xref:System.Char.ConvertFromUtf32%28System.Int32%29>, que devuelve el carácter correspondiente al argumento de tipo entero como `string`. En la segunda técnica, `int` se convierte de manera explícita en un elemento [char](../../../csharp/language-reference/keywords/char.md).  
  
 [!code-csharp[csProgGuideTypes#31](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#31)]  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo se muestra otra manera de convertir un `string` hexadecimal en un entero mediante la llamada al método <xref:System.Int32.Parse%28System.String%2CSystem.Globalization.NumberStyles%29>.  
  
 [!code-csharp[csProgGuideTypes#32](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#32)]  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se muestra cómo convertir un `string` hexadecimal en un elemento [float](../../../csharp/language-reference/keywords/float.md) con la clase <xref:System.BitConverter?displayProperty=nameWithType> y el método <xref:System.UInt32.Parse%2A?displayProperty=nameWithType>.  
  
 [!code-csharp[csProgGuideTypes#39](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#39)]  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo convertir una matriz [byte](../../../csharp/language-reference/keywords/byte.md) en una cadena hexadecimal mediante la clase <xref:System.BitConverter?displayProperty=nameWithType>.  
  
 [!code-csharp[csProgGuideTypes#38](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#38)]  
  
## <a name="see-also"></a>Vea también

- [Standard Numeric Format Strings](../../../standard/base-types/standard-numeric-format-strings.md)
- [Tipos](../../../csharp/programming-guide/types/index.md)
- [Cómo: Determinar si una cadena representa un valor numérico](../../../csharp/programming-guide/strings/how-to-determine-whether-a-string-represents-a-numeric-value.md)
