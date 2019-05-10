---
title: Construcción funcional (LINQ to XML) (Visual Basic)
ms.date: 07/20/2015
ms.assetid: feac4273-39ab-43ae-bab7-4059c807a785
ms.openlocfilehash: a942d4a0fa4c33cf4699c5825ea05403bdfce48f
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2019
ms.locfileid: "64618322"
---
# <a name="functional-construction-linq-to-xml-visual-basic"></a>Construcción funcional (LINQ to XML) (Visual Basic)
[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] proporciona una manera eficaz de crear elementos XML denominada *construcción funcional*. La construcción funcional es la capacidad de crear un árbol XML en una sola instrucción.  
  
 Hay varias características fundamentales de la interfaz de programación de [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] que permiten la construcción funcional:  
  
- El constructor <xref:System.Xml.Linq.XElement> toma varios tipos de argumentos para el contenido. Por ejemplo, puede pasar otro objeto <xref:System.Xml.Linq.XElement>, que se convierte en un elemento secundario. Puede pasar un objeto <xref:System.Xml.Linq.XAttribute>, que se convierte en un atributo del elemento. O bien, puede pasar cualquier otro tipo de objeto, que se convierte en una cadena y en el contenido de texto del elemento.  
  
- El constructor <xref:System.Xml.Linq.XElement> toma una matriz de `params` del tipo <xref:System.Object>, de forma que puede pasar cualquier número de objetos al constructor. Esto permite crear un elemento que tiene un contenido complejo.  
  
- Si un objeto implementa <xref:System.Collections.Generic.IEnumerable%601>, se enumera la colección del objeto y se agregan todos los elementos de la colección. Si la colección contiene objetos <xref:System.Xml.Linq.XElement> o <xref:System.Xml.Linq.XAttribute>, cada elemento de la colección se agrega por separado. Esto es importante porque le permite pasar los resultados de una consulta de [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] al constructor.  
  
 A continuación se muestra un ejemplo:  
  
 Estas características le permiten escribir código mediante literales XML para crear un árbol XML y también para escribir código que usa los resultados de [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] consultas cuando se crea un árbol XML:  
  
```vb  
Dim srcTree As XElement = _  
    <Root>  
        <Element>1</Element>  
        <Element>2</Element>  
        <Element>3</Element>  
        <Element>4</Element>  
        <Element>5</Element>  
    </Root>  
Dim xmlTree As XElement = _  
    <Root>  
        <Child>1</Child>  
        <Child>2</Child>  
        <%= From el In srcTree.Elements() _  
            Where CInt(el) > 2 _  
            Select el %>  
    </Root>  
Console.WriteLine(xmlTree)  
```  
  
 Este ejemplo produce el siguiente resultado:  
  
```xml  
<Root>  
  <Child>1</Child>  
  <Child>2</Child>  
  <Element>3</Element>  
  <Element>4</Element>  
  <Element>5</Element>  
</Root>  
```  
  
## <a name="see-also"></a>Vea también

- [Crear árboles XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/creating-xml-trees.md)
