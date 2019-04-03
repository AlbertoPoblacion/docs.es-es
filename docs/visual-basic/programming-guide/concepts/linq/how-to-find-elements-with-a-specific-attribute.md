---
title: Filtrar Buscar elementos con un atributo específico (XPath-LINQ to XML) (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 4bb38d2c-bc7c-4196-8909-aaf41fb86b28
ms.openlocfilehash: 17c5e9abf607df7311ff2552b7e9c54cbf30fd59
ms.sourcegitcommit: bce0586f0cccaae6d6cbd625d5a7b824d1d3de4b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58825344"
---
# <a name="how-to-find-elements-with-a-specific-attribute-xpath-linq-to-xml-visual-basic"></a>Filtrar Buscar elementos con un atributo específico (XPath-LINQ to XML) (Visual Basic)
En ocasiones, deseará buscar todos los elementos que tengan un atributo en particular. Pero no le preocupa cuáles es el contenido del atributo. En vez de ello, desea realizar la selección en función de si existe o no el atributo.  
  
 La expresión XPath es:  
  
 `./*[@Select]`  
  
## <a name="example"></a>Ejemplo  
 El siguiente código selecciona únicamente los elementos que tengan el atributo `Select`.  
  
```vb  
Dim doc As XElement = _   
    <Root>  
        <Child1>1</Child1>  
        <Child2 Select='true'>2</Child2>  
        <Child3>3</Child3>  
        <Child4 Select='true'>4</Child4>  
        <Child5>5</Child5>  
    </Root>  
  
' LINQ to XML query  
Dim list1 As IEnumerable(Of XElement) = _  
    From el In doc.Elements() _  
    Where el.@Select <> Nothing _  
    Select el  
  
' XPath expression  
Dim list2 As IEnumerable(Of XElement) = DirectCast(doc.XPathEvaluate _  
    ("./*[@Select]"), IEnumerable).Cast(Of XElement)()  
  
If list1.Count() = list2.Count() And _  
    list1.Intersect(list2).Count() = list1.Count() Then  
    Console.WriteLine("Results are identical")  
Else  
    Console.WriteLine("Results differ")  
End If  
  
For Each el As XElement In list1  
    Console.WriteLine(el)  
Next  
```  
  
 Este ejemplo produce el siguiente resultado:  
  
```  
Results are identical  
<Child2 Select="true">2</Child2>  
<Child4 Select="true">4</Child4>  
```  
  
## <a name="see-also"></a>Vea también

- [LINQ to XML para usuarios de XPath (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)
