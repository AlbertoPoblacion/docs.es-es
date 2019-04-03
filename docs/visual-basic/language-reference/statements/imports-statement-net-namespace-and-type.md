---
title: Instrucción Imports - Namespace .NET y el tipo (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Imports
- imports
helpviewer_keywords:
- declared element names [Visual Basic], qualification
- imports [Visual Basic]
- Imports statement [Visual Basic]
- aliases [Visual Basic], Imports statement
- container elements [Visual Basic]
- namespaces [Visual Basic], importing
- Imports statement [Visual Basic], syntax
- import aliases [Visual Basic]
- aliases [Visual Basic], import
- declared elements [Visual Basic], container elements
ms.assetid: 7062f8aa-d890-4232-9eed-92836e13fb6e
ms.openlocfilehash: 4574bab62ca6d095ab66c17bf186da5f3d79bfb7
ms.sourcegitcommit: bce0586f0cccaae6d6cbd625d5a7b824d1d3de4b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58826527"
---
# <a name="imports-statement-net-namespace-and-type"></a>Instrucción Imports (Tipo y espacio de nombres de .NET)
Permite escribe los nombres que se haga referencia sin la calificación de espacio de nombres.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
Imports [ aliasname = ] namespace  
-or-  
Imports [ aliasname = ] namespace.element  
```  
  
## <a name="parts"></a>Elementos  
  
|Término|de esquema JSON|  
|---|---|  
|`aliasname`|Opcional. Un *alias de importación* o el nombre por el que puede hacer referencia a código `namespace` en lugar de la cadena de calificación completa. Vea [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).|  
|`namespace`|Obligatorio. El nombre completo del espacio de nombres que se va a importar. Puede ser una cadena de espacios de nombres anidada a cualquier nivel.|  
|`element`|Opcional. El nombre de un elemento de programación declarado en el espacio de nombres. Puede ser cualquier elemento de contenedor.|  
  
## <a name="remarks"></a>Comentarios  
 El `Imports` instrucción permite que los tipos que se encuentran en un espacio de nombres especificado que se haga referencia directamente.  
  
 Puede proporcionar un único espacio de nombres o una cadena de espacios de nombres anidados. Cada espacio de nombres anidado se separa del espacio de nombres de nivel superior siguiente por un punto (`.`), tal y como se muestra en el ejemplo siguiente.  
  
 `Imports System.Collections.Generic`  
  
 Cada archivo de código fuente puede contener cualquier número de `Imports` instrucciones. Éstas deben seguir las declaraciones de opción, como el `Option Strict` instrucción y se debe preceder a cualquier declaración de elemento de programación como `Module` o `Class` instrucciones.  
  
 Puede usar `Imports` sólo en el nivel de archivo. Esto significa que el contexto de declaración de importación debe ser un archivo de origen y no puede ser un espacio de nombres, clase, estructura, módulo, interfaz, procedimiento o bloque.  
  
 Tenga en cuenta que el `Imports` instrucción no hace que estén disponibles para su proyecto elementos de otros proyectos y ensamblados. Importar no realizará la definición de una referencia. Solo quita la necesidad de calificar nombres que ya están disponibles en el proyecto. Para obtener más información, vea "Importar elementos contenedores" en [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md).  
  
> [!NOTE]
>  Puede definir implícita `Imports` instrucciones mediante el uso de la [página referencias, Diseñador de proyectos (Visual Basic)](/visualstudio/ide/reference/references-page-project-designer-visual-basic). Para obtener más información, vea [Cómo: Agregar o quitar espacios de nombres importados (Visual Basic)](/visualstudio/ide/how-to-add-or-remove-imported-namespaces-visual-basic).  
  
## <a name="import-aliases"></a>Alias de importación  
 Un *alias de importación* define el alias para un espacio de nombres o tipo. Alias de importación son útiles cuando necesite utilizar los elementos con el mismo nombre que se declaran en uno o varios espacios de nombres. Para obtener más información y un ejemplo, vea "Calificar un nombre de elemento" en [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md).  
  
 No se deben declarar un miembro en el nivel de módulo con el mismo nombre que `aliasname`. Si lo hace, el compilador de Visual Basic usa `aliasname` solo para el miembro declarado y ya no lo reconoce como un alias de importación.  
  
 Aunque la sintaxis que se utiliza para declarar un alias de importación que se usa para la importación de un prefijo de espacio de nombres XML, los resultados son diferentes. Un alias de importación puede usarse como una expresión en el código, mientras que se puede utilizar un prefijo de espacio de nombres XML sólo en literales XML o propiedades de eje XML como el prefijo para un nombre de atributo o elemento calificado.  
  
### <a name="element-names"></a>Nombres de elementos  
 Si proporciona `element`, debe representar un *elemento contenedor*, es decir, un elemento de programación que puede contener otros elementos. Elementos contenedores incluyen clases, estructuras, módulos, interfaces y enumeraciones.  
  
 El ámbito de los elementos disponible mediante un `Imports` instrucción depende de si se especifica `element`. Si solo especifica `namespace`, todo de forma exclusiva con el nombre de los miembros de ese espacio de nombres y los miembros de elementos contenedores dentro de ese espacio de nombres, están disponibles sin calificación. Si se especifican ambas `namespace` y `element`, solo los miembros de ese elemento están disponibles sin calificación.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve todas las carpetas en el directorio C:\ utilizando la <xref:System.IO.DirectoryInfo> clase.  
  
 El código no tiene ningún `Imports` instrucciones en la parte superior del archivo. Por lo tanto, el `DirectoryInfo`, <xref:System.Text.StringBuilder>, y <xref:Microsoft.VisualBasic.ControlChars.CrLf> las referencias son totalmente completos con los espacios de nombres.  
  
 [!code-vb[VbVbalrStatements#152](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class12.vb#152)]  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se incluye `Imports` instrucciones para los espacios de nombres que se hace referencia. Por lo tanto, no es necesario que los tipos se completa con los espacios de nombres.  
  
 [!code-vb[VbVbalrStatements#153](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class12.vb#153)]  
  
 [!code-vb[VbVbalrStatements#154](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class12.vb#154)]  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se incluye `Imports` las instrucciones que crean alias para los espacios de nombres que se hace referencia. Los tipos están calificados con el alias.  
  
 [!code-vb[VbVbalrStatements#155](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class12.vb#155)]  
  
 [!code-vb[VbVbalrStatements#156](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class12.vb#156)]  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se incluye `Imports` las instrucciones que crean alias para los tipos que se hace referencia. Los alias se usan para especificar los tipos.  
  
 [!code-vb[VbVbalrStatements#157](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class12.vb#157)]  
  
 [!code-vb[VbVbalrStatements#158](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class12.vb#158)]  
  
## <a name="see-also"></a>Vea también

- [Namespace (instrucción)](../../../visual-basic/language-reference/statements/namespace-statement.md)
- [Espacios de nombres en Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md)
- [Referencias y la instrucción Imports](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)
- [Imports (instrucción), espacio de nombres XML](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)
- [Referencias a elementos declarados](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
