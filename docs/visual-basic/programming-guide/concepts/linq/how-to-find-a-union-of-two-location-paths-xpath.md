---
title: Procedimiento Buscar una Unión de dos rutas de acceso de ubicación (XPath-LINQ to XML) (Visual Basic)
ms.date: 07/20/2015
ms.assetid: c82c09b4-cb0a-47ec-8cc3-a124144c2788
ms.openlocfilehash: 6905e6a7bd0cba37006b1fc3077ad72de36bcf56
ms.sourcegitcommit: d7c298f6c2e3aab0c7498bfafc0a0a94ea1fe23e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/10/2019
ms.locfileid: "72249949"
---
# <a name="how-to-find-a-union-of-two-location-paths-xpath-linq-to-xml-visual-basic"></a>Procedimiento Buscar una Unión de dos rutas de acceso de ubicación (XPath-LINQ to XML) (Visual Basic)
XPath permite buscar la unión de los resultados de dos rutas de ubicación XPath.  
  
 La expresión XPath es:  
  
 `//Category|//Price`  
  
 Puede conseguir los mismos resultados usando el operador de consulta estándar <xref:System.Linq.Enumerable.Concat%2A>.  
  
## <a name="example"></a>Ejemplo  
 Este ejemplo busca todos los elementos `Category` y todos los elementos `Price` y los concatena en una única recopilación. Tenga en cuenta que la consulta [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] llama a <xref:System.Xml.Linq.Extensions.InDocumentOrder%2A> para ordenar los resultados. Los resultados de la evaluación de la expresión XPath también están en el orden del documento.  
  
 Este ejemplo utiliza el siguiente documento XML: [Archivo XML de ejemplo: Datos numéricos (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-numerical-data-linq-to-xml.md).  
  
```vb  
Dim data As XDocument = XDocument.Load("Data.xml")  
  
' LINQ to XML query  
Dim list1 As IEnumerable(Of XElement) = _  
    data...<Category>.Concat(data...<Price>).InDocumentOrder()  
  
' XPath expression  
Dim list2 As IEnumerable(Of XElement) = _  
    data.XPathSelectElements("//Category|//Price")  
  
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
  
```console
Results are identical  
<Category>A</Category>  
<Price>24.50</Price>  
<Category>B</Category>  
<Price>89.99</Price>  
<Category>A</Category>  
<Price>4.95</Price>  
<Category>A</Category>  
<Price>66.00</Price>  
<Category>B</Category>  
<Price>.99</Price>  
<Category>A</Category>  
<Price>29.00</Price>  
<Category>B</Category>  
<Price>6.99</Price>  
```  
  
## <a name="see-also"></a>Vea también

- [LINQ to XML para los usuarios de XPath (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)
