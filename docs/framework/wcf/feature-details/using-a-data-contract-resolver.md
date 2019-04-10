---
title: Utilizar una resolución del contrato de datos
ms.date: 03/30/2017
ms.assetid: 2e68a16c-36f0-4df4-b763-32021bff2b89
ms.openlocfilehash: b1c545d84db68f4b13925dd9088cc9d81050b5e7
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59222450"
---
# <a name="using-a-data-contract-resolver"></a>Utilizar una resolución del contrato de datos
Una resolución del contrato de datos le permite configurar los tipos conocidos dinámicamente. Se necesitan tipos conocidos al serializar o deserializar un tipo no esperado por un contrato de datos. Para obtener más información sobre los tipos conocidos, consulte [Data Contract Known Types](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md). Los tipos conocidos se suelen especificar de modo estático. Esto significa que tendría que conocer todos los tipos posibles que puede recibir una operación mientras la implementa. Hay escenarios en los que no esto no se cumple y es importante saber especificar los tipos conocidos de forma dinámica.  
  
## <a name="creating-a-data-contract-resolver"></a>Crear una resolución del contrato de datos  
 La creación de una resolución del contrato de datos supone la implementación de dos métodos, <xref:System.Runtime.Serialization.DataContractResolver.TryResolveType%2A> y <xref:System.Runtime.Serialization.DataContractResolver.ResolveName%2A>. Estos dos métodos implementan devoluciones de llamada que se utilizan durante la serialización y la deserialización respectivamente. El método <xref:System.Runtime.Serialization.DataContractResolver.TryResolveType%2A> se invoca durante la serialización y toma un tipo de contrato de datos para asignarlo a un espacio de nombres y a un nombre `xsi:type`. El método <xref:System.Runtime.Serialization.DataContractResolver.ResolveName%2A> se invoca durante la deserialización y toma un espacio de nombres y un nombre `xsi:type` y lo resuelve como un tipo de contrato de datos. Ambos métodos tienen un parámetro `knownTypeResolver` que se puede emplear para usar la resolución de tipo conocido predeterminada en la implementación.  
  
 En el siguiente ejemplo, se muestra cómo implementar una clase <xref:System.Runtime.Serialization.DataContractResolver> para realizar asignaciones desde y hacia un tipo de contrato de datos denominado `Customer` derivado de una `Person` del tipo de contrato de datos.  
  
```csharp  
public class MyCustomerResolver : DataContractResolver  
{  
    public override bool TryResolveType(Type dataContractType, Type declaredType, DataContractResolver knownTypeResolver, out XmlDictionaryString typeName, out XmlDictionaryString typeNamespace)  
    {  
        if (dataContractType == typeof(Customer))  
        {  
            XmlDictionary dictionary = new XmlDictionary();  
            typeName = dictionary.Add("SomeCustomer");  
            typeNamespace = dictionary.Add("http://tempuri.com");  
            return true;  
        }  
        else  
        {  
            return knownTypeResolver.TryResolveType(dataContractType, declaredType, null, out typeName, out typeNamespace);  
        }  
    }  
  
    public override Type ResolveName(string typeName, string typeNamespace, DataContractResolver knownTypeResolver)  
    {  
        if (typeName == "SomeCustomer" && typeNamespace == "http://tempuri.com")  
        {  
            return typeof(Customer);  
        }  
        else  
        {  
            return knownTypeResolver.ResolveName(typeName, typeNamespace, null);  
        }  
    }  
}  
```  
  
 Cuando haya definido una <xref:System.Runtime.Serialization.DataContractResolver>, puede utilizarla pasándola al constructor <xref:System.Runtime.Serialization.DataContractSerializer>, tal y como se muestra en el siguiente ejemplo.  
  
```  
XmlObjectSerializer serializer = new DataContractSerializer(typeof(Customer), null, Int32.MaxValue, false, false, null, new MyCustomerResolver());  
```  
  
 Puede especificar la clase <xref:System.Runtime.Serialization.DataContractResolver> en una llamada a los métodos <xref:System.Runtime.Serialization.DataContractSerializer.ReadObject%2A?displayProperty=nameWithType> o <xref:System.Runtime.Serialization.DataContractSerializer.WriteObject%2A?displayProperty=nameWithType>, tal y como se muestra en el siguiente ejemplo.  
  
```  
MemoryStream ms = new MemoryStream();  
DataContractSerializer serializer = new DataContractSerializer(typeof(Customer));  
XmlDictionaryWriter writer = XmlDictionaryWriter.CreateDictionaryWriter(XmlWriter.Create(ms));  
serializer.WriteObject(writer, new Customer(), new MyCustomerResolver());  
writer.Flush();  
ms.Position = 0;  
Console.WriteLine(((Customer)serializer.ReadObject(XmlDictionaryReader.CreateDictionaryReader(XmlReader.Create(ms)), false, new MyCustomerResolver()));  
```  
  
 También puede establecerla en <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>, tal y como se muestra en el siguiente ejemplo.  
  
```  
ServiceHost host = new ServiceHost(typeof(MyService));  
  
ContractDescription cd = host.Description.Endpoints[0].Contract;  
OperationDescription myOperationDescription = cd.Operations.Find("Echo");  
  
DataContractSerializerOperationBehavior serializerBehavior = myOperationDescription.Behaviors.Find<DataContractSerializerOperationBehavior>();  
if (serializerBehavior == null)  
{  
    serializerBehavior = new DataContractSerializerOperationBehavior(myOperationDescription);  
    myOperationDescription.Behaviors.Add(serializerBehavior);  
}  
  
SerializerBehavior.DataContractResolver = new MyCustomerResolver();  
```  
  
 Puede especificar mediante declaración una resolución de contrato de datos implementando un atributo que pueda aplicarse a un servicio.  Para obtener más información, consulte el [KnownAssemblyAttribute](../../../../docs/framework/wcf/samples/knownassemblyattribute.md) ejemplo. Este ejemplo implementa un atributo denominado "KnownAssembly" que agrega una resolución del contrato de datos personalizados para el comportamiento del servicio.  
  
## <a name="see-also"></a>Vea también

- [Tipos conocidos de contratos de datos](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)
- [Ejemplo de DataContractSerializer](../../../../docs/framework/wcf/samples/datacontractserializer-sample.md)
- [KnownAssemblyAttribute](../../../../docs/framework/wcf/samples/knownassemblyattribute.md)
