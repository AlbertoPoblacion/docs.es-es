---
title: Value (Propiedad XML) (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.XmlPropertyExtensionValue
helpviewer_keywords:
- Value property [Visual Basic]
- Visual Basic code, accessing XML
- XML axis [Visual Basic], Value
- XML Value property [Visual Basic]
ms.assetid: 7ddd057a-a195-4e9b-ad8b-2ee0e615a20f
ms.openlocfilehash: 1c7aa1cc32bc1c5ef637f7a606db7e695f1dfaee
ms.sourcegitcommit: bce0586f0cccaae6d6cbd625d5a7b824d1d3de4b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58821956"
---
# <a name="xml-value-property-visual-basic"></a>Value (Propiedad XML) (Visual Basic)
Proporciona acceso al valor del primer elemento de una colección de <xref:System.Xml.Linq.XElement> objetos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
object.Value  
```  
  
## <a name="parts"></a>Elementos  
  
|Término|de esquema JSON|  
|---|---|  
|`object`|Obligatorio. Una colección de objetos <xref:System.Xml.Linq.XElement>.|  
  
## <a name="return-value"></a>Valor devuelto  
 Un `String` que contiene el valor del primer elemento de la colección, o `Nothing` si la colección está vacía.  
  
## <a name="remarks"></a>Comentarios  
 El <xref:System.Xml.Linq.XElement.Value%2A> propiedad facilita el acceso al valor del primer elemento en una colección de <xref:System.Xml.Linq.XElement> objetos. Esta propiedad comprueba primero si la colección contiene al menos un objeto. Si la colección está vacía, esta propiedad devuelve `Nothing`. En caso contrario, esta propiedad devuelve el valor de la <xref:System.Xml.Linq.XElement.Value%2A> propiedad del primer elemento de la colección.  
  
> [!NOTE]
>  Al acceder al valor de un atributo XML con el '\@' el valor del atributo de identificador, se devuelve como un `String` y no es necesario especificar explícitamente el <xref:System.Xml.Linq.XAttribute.Value%2A> propiedad.  
  
 Para obtener acceso a otros elementos de una colección, puede usar la propiedad de indizador de extensión XML. Para obtener más información, consulte [propiedad de indizador de extensión](../../../visual-basic/language-reference/xml-axis/extension-indexer-property.md).  
  
## <a name="inheritance"></a>Herencia  
 La mayoría de los usuarios no tendrán que implementar <xref:System.Collections.Generic.IEnumerable%601>y por lo tanto, puede omitir esta sección.  
  
 El <xref:System.Xml.Linq.XElement.Value%2A> es una propiedad de extensión para tipos que implementan `IEnumerable(Of XElement)`. El enlace de esta propiedad de extensión es como el enlace de métodos de extensión: si un tipo implementa una de las interfaces y define una propiedad que tiene el nombre "Value", esa propiedad tiene prioridad sobre la propiedad de extensión. En otras palabras, esto <xref:System.Xml.Linq.XElement.Value%2A> propiedad se puede invalidar mediante la definición de una nueva propiedad en una clase que implementa `IEnumerable(Of XElement)`.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra cómo usar el <xref:System.Xml.Linq.XElement.Value%2A> propiedad para tener acceso al primer nodo en una colección de <xref:System.Xml.Linq.XElement> objetos. El ejemplo utiliza la propiedad de eje secundario para obtener la colección de todos los nodos secundarios denominados `phone` que están en el `contact` objeto.  
  
 [!code-vb[VbXMLSamples#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples7.vb#15)]  
  
 Este código muestra el siguiente texto:  
  
 `Phone number: 206-555-0144`  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra cómo obtener el valor de un atributo XML de una colección de <xref:System.Xml.Linq.XAttribute> objetos. El ejemplo utiliza la propiedad de eje de atributo para mostrar el valor de la `type` atributo para todos los `phone` elementos.  
  
 [!code-vb[VbXMLSamples#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples7.vb#16)]  
  
 Este código muestra el siguiente texto:  
  
 `home`  
  
 `work`  
  
## <a name="see-also"></a>Vea también

- <xref:System.Xml.Linq.XElement>
- <xref:System.Collections.Generic.IEnumerable%601>
- [Propiedades del eje XML](../../../visual-basic/language-reference/xml-axis/index.md)
- [Literales XML](../../../visual-basic/language-reference/xml-literals/index.md)
- [Crear XML en Visual Basic](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
- [Métodos de extensión](../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)
- [Propiedad de indexador de extensión](../../../visual-basic/language-reference/xml-axis/extension-indexer-property.md)
- [Propiedad del eje secundario XML](../../../visual-basic/language-reference/xml-axis/xml-child-axis-property.md)
- [Propiedad del eje de atributo XML](../../../visual-basic/language-reference/xml-axis/xml-attribute-axis-property.md)
