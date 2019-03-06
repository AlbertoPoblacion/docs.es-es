---
title: Propiedad de eje descendiente XML Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.XmlPropertyDescendantsAxis
helpviewer_keywords:
- Visual Basic code, accessing XML
- XML descendant axis property [Visual Basic]
- descendant axis property [Visual Basic]
- XML axis [Visual Basic], descendant
- XML [Visual Basic], accessing
ms.assetid: a178f85b-5d54-438f-8479-40b62af6fe76
ms.openlocfilehash: bc1dff6dc3b580079087f370212b7d3acd30e4fb
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2019
ms.locfileid: "57353028"
---
# <a name="xml-descendant-axis-property-visual-basic"></a>Propiedad de eje descendiente XML Visual Basic)

Proporciona acceso a los descendientes de los siguientes valores: una <xref:System.Xml.Linq.XElement> objeto, un <xref:System.Xml.Linq.XDocument> (objeto), una colección de <xref:System.Xml.Linq.XElement> objetos o una colección de <xref:System.Xml.Linq.XDocument> objetos.

## <a name="syntax"></a>Sintaxis

```
object...<descendant>
```

## <a name="parts"></a>Elementos

`object` Obligatorio. Un objeto <xref:System.Xml.Linq.XElement>, un objeto <xref:System.Xml.Linq.XDocument>, una colección de objetos <xref:System.Xml.Linq.XElement> o una colección de objetos <xref:System.Xml.Linq.XDocument>.

`...<` Obligatorio. Denota el inicio de una propiedad de eje descendiente.

`descendant` Obligatorio. Nombre de los nodos descendientes para tener acceso a la forma [`prefix:]name`.

|Parte|Descripción|
|----------|-----------------|
|`prefix`|Opcional. Prefijo de espacio de nombres XML para el nodo descendiente. Debe ser un espacio de nombres XML global que se define utilizando un `Imports` instrucción.|
|`name`|Obligatorio. Nombre local del nodo descendiente. Consulte [nombres de atributos y elementos XML declarados](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md).|

`>` Obligatorio. Denota el final de una propiedad de eje descendiente.

## <a name="return-value"></a>Valor devuelto

Una colección de objetos <xref:System.Xml.Linq.XElement>.

## <a name="remarks"></a>Comentarios

Puede usar una propiedad de eje descendiente XML para tener acceso a los nodos descendientes por nombre desde un <xref:System.Xml.Linq.XElement> o <xref:System.Xml.Linq.XDocument> objeto, o de una colección de <xref:System.Xml.Linq.XElement> o <xref:System.Xml.Linq.XDocument> objetos. Use el código XML `Value` propiedad para tener acceso al valor del primer nodo descendiente de la colección devuelta. Para obtener más información, consulte [propiedad Value de XML](../../../visual-basic/language-reference/xml-axis/xml-value-property.md).

El compilador de Visual Basic convierte las propiedades de eje descendiente en llamadas a la <xref:System.Xml.Linq.XContainer.Descendants%2A> método.

## <a name="xml-namespaces"></a>Espacios de nombres XML

El nombre de una propiedad de eje descendiente puede usar solo espacios de nombres XML declarados globalmente con la `Imports` instrucción. No puede utilizar espacios de nombres XML declarados localmente dentro de literales de elemento XML. Para obtener más información, consulte [instrucción Imports (XML Namespace)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md).

## <a name="example"></a>Ejemplo

El ejemplo siguiente muestra cómo tener acceso al valor del primer nodo descendiente denominado `name` y los valores de todos los nodos descendientes denominados `phone` desde el `contacts` objeto.

[!code-vb[VbXMLSamples#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples11.vb#25)]

Este código muestra el siguiente texto:

`Name: Patrick Hines`

`Home Phone = 206-555-0144`

## <a name="example"></a>Ejemplo

En el ejemplo siguiente se declara `ns` como un prefijo de espacio de nombres XML. A continuación, usa el prefijo del espacio de nombres para crear un literal XML y obtener acceso al valor del primer nodo secundario con el nombre completo `ns:name`.

[!code-vb[VbXMLSamples#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples12.vb#26)]

Este código muestra el siguiente texto:

`Name: Patrick Hines`

## <a name="see-also"></a>Vea también

- <xref:System.Xml.Linq.XElement>
- [Propiedades del eje XML](../../../visual-basic/language-reference/xml-axis/index.md)
- [Literales XML](../../../visual-basic/language-reference/xml-literals/index.md)
- [Crear XML en Visual Basic](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
- [Nombres de atributos y elementos XML declarados](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)
