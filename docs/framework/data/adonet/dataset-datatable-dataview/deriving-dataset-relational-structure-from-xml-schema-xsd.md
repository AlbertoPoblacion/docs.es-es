---
title: Derivar una estructura relacional de un conjunto de datos a partir de un esquema XML (XSD)
ms.date: 03/30/2017
ms.assetid: 8f6cd04d-6197-4bc4-9096-8c51c7e4acae
ms.openlocfilehash: 549579fca0179994191987097c12b6085ee91756
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59119696"
---
# <a name="deriving-dataset-relational-structure-from-xml-schema-xsd"></a>Derivar una estructura relacional de un conjunto de datos a partir de un esquema XML (XSD)
Esta sección ofrece información general sobre cómo se crea el esquema relacional de un `DataSet` a partir del documento de esquema del lenguaje de definición de esquema XML (XSD). En general, para cada `complexType` elemento secundario de un elemento de esquema, se genera una tabla en la `DataSet`. La estructura de la tabla está determinada por la definición del tipo complejo. Las tablas se crean en el `DataSet` para elementos de nivel superior en el esquema. Sin embargo, solo se crea una tabla para un nivel superior `complexType` elemento cuando el `complexType` elemento está anidado dentro de otra `complexType` elemento, en el que caso anidado `complexType` elemento se asigna a un `DataTable` dentro de la `DataSet`.  
  
 Para obtener más información sobre el XSD, vea el World Wide Web Consortium (W3C) [XML Schema Part 0: Recomendación base](https://www.w3.org/TR/xmlschema-0/), el [esquema XML parte 1: Recomendación de estructuras](https://www.w3.org/TR/xmlschema-1/)y el [esquema XML parte 2: Recomendación sobre tipos de datos](https://www.w3.org/TR/xmlschema-2/).  
  
 En el ejemplo siguiente se muestra un esquema XML donde `customers` es el elemento secundario de la `MyDataSet` elemento, que es un **DataSet** elemento.  
  
```xml  
<xs:schema id="SomeID"   
            xmlns=""   
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
   <xs:element name="MyDataSet" msdata:IsDataSet="true">  
     <xs:complexType>  
       <xs:choice maxOccurs="unbounded">  
         <xs:element name="customers" >   
           <xs:complexType >  
             <xs:sequence>  
               <xs:element name="CustomerID" type="xs:integer"   
                            minOccurs="0" />  
               <xs:element name="CompanyName" type="xs:string"   
                            minOccurs="0" />  
               <xs:element name="Phone" type="xs:string" />  
             </xs:sequence>  
           </xs:complexType>  
          </xs:element>  
       </xs:choice>  
     </xs:complexType>  
   </xs:element>  
 </xs:schema>  
```  
  
 En el ejemplo anterior, `customers` es un elemento de tipo complejo. Por tanto, se analiza la definición del tipo complejo y el proceso de asignación crea la tabla siguiente.  
  
```  
Customers (CustomerID , CompanyName, Phone)  
```  
  
 El tipo de datos de cada columna de la tabla se deriva del tipo de esquema XML del correspondiente elemento o atributo especificado.  
  
> [!NOTE]
>  Si el elemento `customers` es de un tipo de datos de esquema XML simple como **entero**, se generará ninguna tabla. Solo se crean tablas para elementos de nivel superior que sean de tipos complejos.  
  
 En el siguiente esquema XML, el **esquema** elemento tiene dos elementos secundarios, `InStateCustomers` y `OutOfStateCustomers`.  
  
```xml  
<xs:schema id="SomeID"   
            xmlns=""   
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
   <xs:element name="InStateCustomers" type="customerType" />  
   <xs:element name="OutOfStateCustomers" type="customerType" />  
    <xs:complexType name="customerType" >  
  
     </xs:complexType>  
  
   <xs:element name="MyDataSet" msdata:IsDataSet="true">  
     <xs:complexType>  
       <xs:choice maxOccurs="unbounded">  
         <xs:element ref="customers" />  
       </xs:choice>  
     </xs:complexType>  
   </xs:element>  
 </xs:schema>  
```  
  
 Los dos elementos secundarios `InStateCustomers` y `OutOfStateCustomers` son elementos de tipo complejo (`customerType`). Por lo tanto, el proceso de asignación genera las dos siguientes tablas idénticas en el `DataSet`.  
  
```  
InStateCustomers (CustomerID , CompanyName, Phone)  
OutOfStateCustomers (CustomerID , CompanyName, Phone)  
```  
  
## <a name="in-this-section"></a>En esta sección  
 [Asignar restricciones de un esquema XML (XSD) a restricciones de conjuntos de datos](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 Describe los elementos de esquema XML utilizados para crear restricciones de clave únicas y externas en un `DataSet`.  
  
 [Generar relaciones de objetos DataSet en un esquema XML (XSD)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/generating-dataset-relations-from-xml-schema-xsd.md)  
 Describe los elementos de esquema XML utilizados para crear relaciones entre columnas de tabla en un `DataSet`.  
  
 [Restricciones y relaciones del esquema XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/xml-schema-constraints-and-relationships.md)  
 Describe cómo se crean implícitamente relaciones cuando se usan elementos de esquema XML para crear restricciones en un `DataSet`.  
  
## <a name="related-sections"></a>Secciones relacionadas  
 [Usar XML en un conjunto de datos](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)  
 Describe cómo cargar y conservar la estructura relacional y los datos en un `DataSet` como datos XML.  
  
## <a name="see-also"></a>Vea también

- [Proveedores administrados de ADO.NET y centro de desarrolladores de DataSet](https://go.microsoft.com/fwlink/?LinkId=217917)
