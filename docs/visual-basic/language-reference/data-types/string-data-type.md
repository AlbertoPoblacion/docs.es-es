---
title: String (Tipo de datos, Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.String
helpviewer_keywords:
- strings [Visual Basic], character
- strings [Visual Basic], fixed-length
- string keyword [Visual Basic]
- fixed-length strings [Visual Basic], string data type
- literals [Visual Basic], string
- text [Visual Basic], String data type
- $ identifier type character
- String data type
- fixed-length strings
- string literals [Visual Basic]
- data types [Visual Basic], assigning
- String literals [Visual Basic]
- identifier type characters [Visual Basic], $
ms.assetid: 15ac03f5-cabd-42cc-a754-1df3893c25d9
ms.openlocfilehash: 3e87dc6527b4351467b1155439ee8266157c16ff
ms.sourcegitcommit: bce0586f0cccaae6d6cbd625d5a7b824d1d3de4b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58842296"
---
# <a name="string-data-type-visual-basic"></a>String (Tipo de datos, Visual Basic)
Contiene secuencias de puntos de código (2 bytes) de 16 bits sin signo de ese intervalo de valor comprendido entre 0 y 65535. Cada *punto de código*, o código de carácter representa un único carácter Unicode. Puede contener una cadena de 0 a dos mil millones (2 ^ 31) caracteres Unicode.  
  
## <a name="remarks"></a>Comentarios  
 Use la `String` tipo de datos que contenga varios caracteres sin la sobrecarga de administración de la matriz de `Char()`, una matriz de `Char` elementos.  
  
 El valor predeterminado de `String` es `Nothing` (una referencia nula). Tenga en cuenta que esto no es igual que la cadena vacía (valor `""`).  
  
## <a name="unicode-characters"></a>Caracteres Unicode  
 Los primeros puntos de 128 código (0 – 127) de Unicode corresponden a las letras y símbolos en un teclado US estándar. Estos primeros puntos de 128 código son los mismos que los define el juego de caracteres ASCII. El segundo 128 puntos de código (128-255) representan caracteres especiales, como letras del alfabeto latino, acentos, símbolos de moneda y fracciones. Unicode utiliza los puntos de código restantes (256-65535) para una amplia variedad de símbolos. Esto incluye caracteres de texto de todo el mundo, los signos diacríticos y símbolos técnicos y matemáticos.  
  
 Puede usar métodos como <xref:System.Char.IsDigit%2A> y <xref:System.Char.IsPunctuation%2A> en un carácter individual en un `String` variable para determinar su clasificación Unicode.  
  
## <a name="format-requirements"></a>Requisitos de formato  
 Debe incluir un `String` literal entre comillas (`" "`). Si se debe incluir una comilla como uno de los caracteres de la cadena, utilice dos comillas contiguas (`""`). Esto se ilustra en el siguiente ejemplo:  
  
```  
Dim j As String = "Joe said ""Hello"" to me."  
Dim h As String = "Hello"  
' The following messages all display the same thing:  
' "Joe said "Hello" to me."  
MsgBox(j)  
MsgBox("Joe said " & """" & h & """" & " to me.")  
MsgBox("Joe said """ & h & """ to me.")  
```  
  
 Tenga en cuenta que las comillas contiguas que representan una comilla en la cadena son independientes de las comillas que comienzan y terminan la `String` literal.  
  
## <a name="string-manipulations"></a>Manipulaciones de cadenas  
 Una vez que asigne una cadena a un `String` variable, esa cadena es *inmutable*, lo que significa que no puede cambiar su longitud ni su contenido. Cuando se modifica una cadena de cualquier manera, Visual Basic crea una nueva cadena y abandona la anterior. El `String` variable apunta a la nueva cadena.  
  
 Puede manipular el contenido de un `String` variable mediante una variedad de funciones de cadena. El siguiente ejemplo ilustra el <xref:Microsoft.VisualBasic.Strings.Left%2A> (función)  
  
```  
Dim S As String = "Database"  
' The following statement sets S to a new string containing "Data".  
S = Microsoft.VisualBasic.Left(S, 4)  
```  
  
 Una cadena creada por otro componente podría estar rellena con espacios iniciales o finales. Si recibe este tipo de cadena, puede usar el <xref:Microsoft.VisualBasic.Strings.Trim%2A>, <xref:Microsoft.VisualBasic.Strings.LTrim%2A>, y <xref:Microsoft.VisualBasic.Strings.RTrim%2A> funciones para quitar estos espacios.  
  
 Para obtener más información acerca de las manipulaciones de cadenas, vea [cadenas](../../../visual-basic/programming-guide/language-features/strings/index.md).  
  
## <a name="programming-tips"></a>Sugerencias de programación  
  
-   **Números negativos.** Recuerde que los caracteres mantienen por `String` están firmados y no puede representar los valores negativos. En cualquier caso, no debe utilizar `String` para contener valores numéricos.  
  
-   **Consideraciones de interoperabilidad.** Si interactúa con componentes no escritos para .NET Framework, por ejemplo objetos de automatización o COM, recuerde que los caracteres de cadena tienen un ancho de datos diferentes (8 bits) en otros entornos. Si se pasa un argumento de cadena de caracteres de 8 bits a esos componentes, declárelo como `Byte()`, una matriz de `Byte` elementos, en lugar de `String` en el nuevo código de Visual Basic.  
  
-   **Caracteres de tipo.** Anexar el carácter de tipo identificador `$` a cualquier identificador lo fuerza a la `String` tipo de datos. `String` no tiene ningún carácter de tipo literal. Sin embargo, el compilador trata los literales incluidos entre comillas (`" "`) como `String`.  
  
-   **Tipo de marco de trabajo.** El tipo correspondiente en .NET Framework es la <xref:System.String?displayProperty=nameWithType> clase.  
  
## <a name="see-also"></a>Vea también

- <xref:System.String?displayProperty=nameWithType>
- [Tipos de datos](../../../visual-basic/language-reference/data-types/index.md)
- [Char (tipo de datos)](../../../visual-basic/language-reference/data-types/char-data-type.md)
- [Funciones de conversión de tipos](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [Resumen de conversión](../../../visual-basic/language-reference/keywords/conversion-summary.md)
- [Cómo: Llamar a una función de Windows que adopta tipos sin signo](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)
- [Uso eficiente de tipos de datos](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
