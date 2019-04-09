---
title: Limitaciones de inferencia
ms.date: 03/30/2017
ms.assetid: 78517994-5d57-44f8-9d20-38812977de09
ms.openlocfilehash: 308d2ffdd9e2cb16626861e25613657f341a4ccb
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59076249"
---
# <a name="inference-limitations"></a>Limitaciones de inferencia
El proceso de inferencia de un esquema de <xref:System.Data.DataSet> a partir de XML puede dar como resultado esquemas diferentes, dependiendo de los elementos XML contenidos en cada documento. Por ejemplo, considere los siguientes documentos XML.  
  
 Document1:  
  
```xml  
<DocumentElement>  
  <Element1>Text1</Element1>  
  <Element1>Text2</Element1>  
</DocumentElement>  
```  
  
 Document2:  
  
```xml  
<DocumentElement>  
  <Element1>Text1</Element1>  
</DocumentElement>  
```  
  
 "Document1", el proceso de inferencia produce un **DataSet** denominado "DocumentElement" y una tabla denominada "Element1", ya que "Element1" es un elemento repetitivo.  
  
 **DataSet:** DocumentElement  
  
 **Tabla:** Element1  
  
|Element1_Text|  
|--------------------|  
|Text1|  
|Text2|  
  
 Sin embargo, para "Document2", el proceso de inferencia produce un **DataSet** denominado "NewDataSet" y una tabla denominada "DocumentElement". "Element1" se deduce como una columna porque no tiene atributos ni elementos secundarios.  
  
 **DataSet:** NewDataSet  
  
 **Tabla:** DocumentElement  
  
|Element1|  
|--------------|  
|Text1|  
  
 Podría parecer que estos dos documentos XML producirían el mismo esquema, pero el proceso de inferencia genera resultados muy diferentes basándose en los elementos contenidos en cada documento.  
  
 Para evitar las discrepancias que pueden producirse al generar el esquema de un documento XML, se recomienda especificar explícitamente un esquema mediante el lenguaje de definición de esquemas XML (XSD) o datos XML reducidos (XDR) al cargar un **DataSet** desde XML. Para obtener más información acerca de cómo especificar explícitamente un **DataSet** esquema con el esquema XML, vea [derivar estructura relacional de DataSet de esquemas XML (XSD)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md).  
  
## <a name="see-also"></a>Vea también

- [Inferir una estructura relacional de un conjunto de datos a partir de XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)
- [Cargar un conjunto de datos desde XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)
- [Cargar información del esquema de un conjunto de datos desde XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)
- [Usar XML en un conjunto de datos](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)
- [Objetos DataSet, DataTable y DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)
- [Proveedores administrados de ADO.NET y centro de desarrolladores de DataSet](https://go.microsoft.com/fwlink/?LinkId=217917)
