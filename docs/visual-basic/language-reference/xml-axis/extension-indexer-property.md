---
title: Propiedad de indizador de extensión (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.XmlPropertyExtensionIndexer
helpviewer_keywords:
- Visual Basic code, accessing XML
- XML extension indexer [Visual Basic]
- extension indexer [Visual Basic]
- XML [Visual Basic], accessing
ms.assetid: a16a4b13-54be-432c-82b3-a87091464ada
ms.openlocfilehash: a02c482db81d9d76752cfe66a292dc57c48b2acb
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61698907"
---
# <a name="extension-indexer-property-visual-basic"></a>Propiedad de indizador de extensión (Visual Basic)
Proporciona acceso a los elementos individuales de una recopilación.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
object(index)  
```  
  
## <a name="parts"></a>Elementos  
  
|Término|Definición|  
|---|---|  
|`object`|Obligatorio. Una colección consultable. Es decir, una colección que implementa <xref:System.Collections.Generic.IEnumerable%601> o <xref:System.Linq.IQueryable%601>.|  
|(|Obligatorio. Denota el inicio de la propiedad de indizador.|  
|`index`|Obligatorio. Expresión entera que especifica la posición de base cero de un elemento de la colección.|  
|)|Obligatorio. Denota el final de la propiedad de indizador.|  
  
## <a name="return-value"></a>Valor devuelto  
 El objeto de la ubicación especificada en la colección, o `Nothing` si el índice está fuera del intervalo.  
  
## <a name="remarks"></a>Comentarios  
 Puede usar la propiedad de indizador de extensión para tener acceso a elementos individuales de una colección. Esta propiedad de indizador se usa normalmente en la salida de las propiedades de eje XML. El elemento secundario XML y propiedades de eje descendiente XML devuelven colecciones de <xref:System.Xml.Linq.XElement> objetos o un valor de atributo.  
  
 El compilador de Visual Basic convierte las propiedades del indizador de extensión para las llamadas a la `ElementAtOrDefault` método. A diferencia de un indizador de matriz, el `ElementAtOrDefault` devuelve del método `Nothing` si el índice está fuera del intervalo. Este comportamiento es útil cuando no se puede determinar fácilmente el número de elementos de una colección.  
  
 Esta propiedad de indizador es como una propiedad de extensión para las colecciones que implementan <xref:System.Collections.Generic.IEnumerable%601> o <xref:System.Linq.IQueryable%601>: se usa solo si la colección no tiene un indizador o una propiedad predeterminada.  
  
 Para obtener acceso al valor del primer elemento en una colección de <xref:System.Xml.Linq.XElement> o <xref:System.Xml.Linq.XAttribute> objetos, puede utilizar el código XML `Value` propiedad. Para obtener más información, consulte [propiedad Value de XML](../../../visual-basic/language-reference/xml-axis/xml-value-property.md).  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra cómo usar el indizador de extensión para tener acceso el segundo nodo secundario en una colección de <xref:System.Xml.Linq.XElement> objetos. Se tiene acceso a la colección mediante el uso de la propiedad de eje secundario, que obtiene todos los elementos secundarios denominados `phone` en el `contact` objeto.  
  
 [!code-vb[VbXMLSamples#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples11.vb#24)]  
  
 Este código muestra el siguiente texto:  
  
 `Second phone number: 425-555-0145`  
  
## <a name="see-also"></a>Vea también

- <xref:System.Xml.Linq.XElement>
- [Propiedades del eje XML](../../../visual-basic/language-reference/xml-axis/index.md)
- [Literales XML](../../../visual-basic/language-reference/xml-literals/index.md)
- [Crear XML en Visual Basic](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
- [Propiedad de valor XML](../../../visual-basic/language-reference/xml-axis/xml-value-property.md)
