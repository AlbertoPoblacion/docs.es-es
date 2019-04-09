---
title: ServiceDescription y referencias WSDL
ms.date: 03/30/2017
ms.assetid: eedc025d-abd9-46b1-bf3b-61d2d5c95fd6
ms.openlocfilehash: 6690bea3d3df0f39a5581c3a6c14723c0f30f40c
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59182889"
---
# <a name="servicedescription-and-wsdl-reference"></a>ServiceDescription y referencias WSDL
Este tema describe cómo Windows Communication Foundation (WCF) asigna los documentos de lenguaje de descripción de servicios Web (WSDL) a y desde <xref:System.ServiceModel.Description.ServiceDescription> instancias.  
  
## <a name="how-servicedescription-maps-to-wsdl-11"></a>Asignaciones de ServiceDescription a WSDL 1.1  
 Puede usar WCF para exportar documentos WSDL desde un <xref:System.ServiceModel.Description.ServiceDescription> instancia para el servicio. Los documentos WSDL se generan automáticamente para su servicio al publicar los puntos de conexión de metadatos.  
  
 Además, puede importar instancias <xref:System.ServiceModel.Description.ServiceEndpoint>, instancias <xref:System.ServiceModel.Description.ContractDescription>, e instancias <xref:System.ServiceModel.Channels.Binding> desde documentos WSDL mediante el tipo `WsdlImporter`.  
  
 Los documentos WSDL, exportados por WCF, importación las definiciones de esquema XML utilizadas desde documentos de esquema XML externos. Se exporta un documento de esquema XML independiente para cada espacio de nombres de destino utilizado por los tipos de datos en el servicio. Igualmente, se exporta un documento WSDL independiente para cada espacio de nombres de destino utilizado por los contratos de servicios.  
  
### <a name="servicedescription"></a>ServiceDescription  
 Se asigna una instancia <xref:System.ServiceModel.Description.ServiceDescription> a un elemento `wsdl:service`. Una instancia <xref:System.ServiceModel.Description.ServiceDescription> contiene una colección de instancias <xref:System.ServiceModel.Description.ServiceEndpoint> en la que cada una se asigna a elementos `wsdl:port` individuales.  
  
|Propiedades|Asignación WSDL|  
|----------------|------------------|  
|`Name`|El `wsdl:service` /@name valor para el servicio.|  
|`Namespace`|El espacio de nombres de destino para la definición `wsdl:service` del servicio.|  
|`Endpoints`|Las definiciones `wsdl:port` del servicio.|  
  
### <a name="serviceendpoint"></a>ServiceEndpoint  
 Se asigna una instancia <xref:System.ServiceModel.Description.ServiceEndpoint> a un elemento `wsdl:port`. Una instancia <xref:System.ServiceModel.Description.ServiceEndpoint> contiene una dirección, un enlace y un contrato.  
  
 Los comportamientos del punto de conexión que implementan la interfaz <xref:System.ServiceModel.Description.IWsdlExportExtension> pueden modificar el elemento `wsdl:port` del punto de conexión al que están adjuntos.  
  
|Propiedades|Asignación WSDL|  
|----------------|------------------|  
|`Name`|El `wsdl:port` /@name valor para el punto de conexión y la `wsdl:binding` /@name valor para el enlace de punto de conexión.|  
|`Address`|La dirección para la definición `wsdl:port` del punto de conexión.<br /><br /> El transporte del extremo determina el formato de la dirección. Por ejemplo, para los transportes admitidos por WCF podría ser una dirección SOAP o una referencia del extremo.|  
|`Binding`|La definición `wsdl:binding` del extremo.<br /><br /> A diferencia de `wsdl:binding` definiciones, enlaces de WCF no están asociadas con un contrato.|  
|`Contract`|La definición `wsdl:portType` del extremo.|  
|`Behaviors`|Los comportamientos del punto de conexión que implementan la interfaz <xref:System.ServiceModel.Description.IWsdlExportExtension> pueden modificar `wsdl:port` del punto de conexión.|  
  
### <a name="bindings"></a>Enlaces  
 La instancia de enlace para una instancia `ServiceEndpoint` se asigna a una definición `wsdl:binding`. A diferencia de `wsdl:binding` definiciones, que deben asociarse con un valor concreto `wsdl:portType` definición, los enlaces de WCF son independientes de cualquier contrato.  
  
 Un enlace se compone de una colección de elementos de enlace. Cada elemento describe algún aspecto de cómo el extremo se comunica con los clientes. Además, un enlace tiene una <xref:System.ServiceModel.Channels.MessageVersion> que indica la <xref:System.ServiceModel.EnvelopeVersion> y la <xref:System.ServiceModel.Channels.AddressingVersion> del extremo.  
  
|Propiedades|Asignación WSDL|  
|----------------|------------------|  
|`Name`|Se utiliza en el nombre predeterminado de un extremo, que es el nombre del enlace al que se anexa el nombre del contrato separado por un guión bajo.|  
|`Namespace`|`targetNamespace` para la definición `wsdl:binding`.<br /><br /> En importación, si una directiva está adjunta al puerto WSDL, el espacio de nombres del enlace importado se asigna a `targetNamespace` para la definición `wsdl:port`.|  
|`BindingElementCollection`, tal como lo devuelve el `CreateBindingElements`(método))|Varias extensiones específicas del dominio para la definición `wsdl:binding`, normalmente, las aserciones de directiva.|  
|`MessageVersion`|`EnvelopeVersion` y `AddressingVersion` para el extremo.<br /><br /> Cuando se especifica `MessageVersion.None`, el enlace de WSDL no contiene un enlace SOAP y el puerto WSDL no incluye contenido de WS-Addressing. Este valor se utiliza normalmente para puntos de conexión “XML sin formato” (POX).|  
  
#### <a name="bindingelements"></a>BindingElements  
 Los elementos de enlace de un enlace de extremo se asignan a distintas extensiones WSDL en `wsdl:binding`, por ejemplo, las aserciones de directiva.  
  
 <xref:System.ServiceModel.Channels.TransportBindingElement> del enlace determina la dirección URI del transporte de un enlace SOAP.  
  
#### <a name="addressingversion"></a>AddressingVersion  
 `AddressingVersion` en un enlace se asigna a la versión de direccionamiento usada en `wsd:port`. WCF es compatible con SOAP 1.1 y SOAP 1.2 direcciones y WS-Addressing 2004/08 y referencias de extremo de WS-Addressing 1.0.  
  
#### <a name="envelopeversion"></a>EnvelopeVersion  
 `EnvelopeVersion` en un enlace se asigna a la versión de SOAP usada en `wsdl:binding`. WCF admite enlaces SOAP 1.1 y SOAP 1.2.  
  
### <a name="contracts"></a>Contratos  
 La instancia <xref:System.ServiceModel.Description.ContractDescription> para una instancia `ServiceEndpoint` se asigna a `wsdl:portType`. Una instancia `ContractDescription` describe todas las operaciones de un contrato determinado.  
  
|Propiedades|Asignación WSDL|  
|----------------|------------------|  
|`Name`|El `wsdl:portType` /@name valor para el contrato.|  
|`Namespace`|El espacio de nombres de destino para la definición `wsdl:portType`.|  
|`SessionMode`|El `wsdl:portType` /@msc:usingSession valor para el contrato. Este atributo es una extensión WCF para WSDL 1.1.|  
|`Operations`|Las definiciones `wsdl:operation` para el contrato.|  
  
### <a name="operations"></a>Operaciones  
 Un <xref:System.ServiceModel.Description.OperationDescription> instancia se asigna a un `wsdl:portType` / `wsdl:operation`. `OperationDescription` contiene una colección de instancias `MessageDescription` que describen los mensajes para la operación.  
  
 Dos comportamientos de la operación participan considerablemente en la asignación de `OperationDescription` a un documento WSDL: `DataContractSerializerOperationBehavior` y `XmlSerializerOperationBehavior`.  
  
|Propiedades|Asignación WSDL|  
|----------------|------------------|  
|`Name`|El `wsdl:portType` / `wsdl:operation` /@name valor para la operación.|  
|`ProtectionLevel`|Aserciones de protección de la directiva de seguridad adjuntas a los mensajes `wsdl:binding/wsdl:operation` de esta operación.|  
|`IsInitiating`|El `wsdl:portType` / `wsdl:operation` /@msc:isInitiating valor para la operación. Este atributo es una extensión WCF para WSDL 1.1.|  
|`IsTerminating`|El `wsdl:portType` / `wsdl:operation` /@msc:isTerminating valor para la operación. Este atributo es una extensión WCF para WSDL 1.1.|  
|`Messages`|El `wsdl:portType` / `wsdl:operation` / `wsdl:input` y `wsdl:portType` / `wsdl:operation` / `wsdl:output` mensajes para la operación.|  
|`Faults`|El `wsdl:portType` / `wsdl:operation` / `wsdl:fault` definiciones para la operación.|  
|`Behaviors`|`DataContractSerializerOperationBehavior` y `XmlSerializerOperationBehavior` están relacionados con el enlace y los mensajes de la operación.|  
  
#### <a name="the-datacontractserializeroperationbehavior"></a>DataContractSerializerOperationBehavior  
 `DataContractSerializerOperationBehavior` de una operación es una implementación `IWsdlExportExtension` que exporta los mensajes y el enlace WSDL de esa operación. Los tipos del esquema XML se exportan mediante `XsdDataContractExporter`. `DataContractSerializerOperationBehavior` también determina el uso y el estilo, así como el exportador e importador del esquema que se utilizarán para esa operación.  
  
|Propiedades|Asignación WSDL|  
|----------------|------------------|  
|`DataContractFormatAttribute`|El `Style` propiedad para este atributo se asigna a la `wsdl:binding` / `wsdl:operation` / `soap:operation` /@style valor para la operación.<br /><br /> `DataContractSerializerOperationBehavior` solo admite el uso literal de los tipos del esquema en WSDL.|  
  
#### <a name="the-xmlserializeroperationbehavior"></a>XmlSerializerOperationBehavior  
 `XmlSerializerOperationBehavior` de una operación es una implementación `IWsdlExportExtension` que exporta los mensajes y el enlace WSDL de esa operación. Los tipos del esquema XML se exportan mediante `XmlSchemaExporter`. `XmlSerializerOperationBehavior` también determina el uso y el estilo, así como el exportador e importador del esquema que se utilizarán para esa operación.  
  
|Propiedades|Asignación WSDL|  
|----------------|------------------|  
|`XmlSerializerFormatAttribute`|El `Style` propiedad para este atributo se asigna a la `wsdl:binding` / `wsdl:operation` / `soap:operation` /@style valor para la operación.<br /><br /> El `Use` propiedad para este atributo se asigna a la `wsdl:binding` / `wsdl:operation` / `soap:operation`/ */@use valores para todos los mensajes en la operación.|  
  
### <a name="messages"></a>Mensajes  
 Un `MessageDescription` instancia se asigna a un `wsdl:message` que hace referencia un `wsdl:portType` / `wsdl:operation` / `wsdl:input` o un `wsdl:portType` / `wsdl:operation` / `wsdl:output`mensaje en una operación. `MessageDescription` posee un cuerpo y encabezados.  
  
|Propiedades|Asignación WSDL|  
|----------------|------------------|  
|`Action`|La acción de SOAP o de WS-Addressing para el mensaje.<br /><br /> Tenga en cuenta que las operaciones que utilizan la cadena de acción "*" no se representan en WSDL.|  
|`Direction`|`MessageDirection.Input` se asigna a `wsdl:input`.<br /><br /> `MessageDirection.Output` se asigna a `wsdl:output`.|  
|`ProtectionLevel`|Aserciones de protección de la directiva de seguridad adjuntas a las definiciones `wsdl:message` de este mensaje.|  
|`Body`|El cuerpo del mensaje.|  
|`Headers`|Los encabezados del mensaje.|  
|`ContractDescription.Name`, `OperationContract.Name`|Al exportar, se usa para derivar el `wsdl:message` /@name valor.|  
  
#### <a name="message-body"></a>Cuerpo del mensaje  
 Un `MessageBodyDescription` instancia se asigna a la `wsdl:message` / `wsdl:part` definiciones para el cuerpo de un mensaje. El cuerpo del mensaje puede ser de estilo ajustado o sencillo.  
  
|Propiedades|Asignación WSDL|  
|----------------|------------------|  
|`WrapperName`|Si el estilo no es RPC, el `WrapperName` asigna al nombre del elemento al que hace referencia el `wsdl:message` / `wsdl:part` con @name establecido en "parámetros".|  
|`WrapperNamespace`|Si el estilo no es RPC, el `WrapperNamespace` se asigna al espacio de nombres de elemento para el `wsdl:message` / `wsdl:part` con @name establecido en "parámetros".|  
|`Parts`|Las partes del mensaje de este cuerpo del mensaje.|  
|`ReturnValue`|El elemento secundario del elemento contenedor, si un elemento contenedor existe (Documente con estilo ajustado o estilo RPC), de lo contrario, la primera `wsdl:message` / `wsdl:part` en el mensaje.|  
  
#### <a name="message-parts"></a>Partes del mensaje  
 Un `MessagePartDescription` instancia se asigna a un `wsdl:message` / `wsdl:part` y el tipo de esquema XML o el elemento al que apunta la parte del mensaje.  
  
|Propiedades|Asignación WSDL|  
|----------------|------------------|  
|`Name`|El `wsd:message` / `wsdl:part` /@name valor para la parte del mensaje y el nombre del elemento al que señala la parte del mensaje.|  
|`Namespace`|Espacio de nombres del elemento al que señala la parte del mensaje.|  
|`Index`|El índice de la `wsdl:message` / `wsdl:part` para el mensaje.|  
|`ProtectionLevel`|Aserciones de protección de la directiva de seguridad adjuntas a la definición `wsdl:message` de esta parte del mensaje. La directiva se parametriza para señalar la parte del mensaje específica.|  
|`MessageType`|El tipo de esquema XML del elemento al que señala la parte del mensaje.|  
  
#### <a name="message-headers"></a>Encabezados de mensajes  
 Una instancia `MessageHeaderDescription` es una parte de un mensaje que también se asigna a un enlace `soap:header` de la parte del mensaje.  
  
### <a name="faults"></a>Errores  
 Un `FaultDescription` instancia se asigna a un `wsdl:portType` / `wsdl:operation` / `wsdl:fault` definición y sus asociados `wsdl:message` definición. Se agrega `wsdl:message` al mismo espacio de nombres de destino que su tipo de puerto WSDL asociado. `wsdl:message` tiene una única parte del mensaje denominada "detalle" que señala al elemento de esquema XML que corresponde al valor de propiedad `DefaultType` para la instancia `FaultDescription`.  
  
|Propiedades|Asignación WSDL|  
|----------------|------------------|  
|`Name`|El `wsdl:portType` / `wsdl:operation` / `wsdl:fault` /@name valor para el error.|  
|`Namespace`|El espacio de nombres del elemento de esquema XML al que señala la parte del mensaje de información acerca del error.|  
|`Action`|La acción de SOAP o de WS-Addressing para el error.|  
|`ProtectionLevel`|Aserciones de protección de la directiva de seguridad adjuntas a la definición `wsdl:message` de este error.|  
|`DetailType`|El tipo de esquema XML del elemento al que señala la parte del mensaje de información.|  
|`Name, ContractDescription.Name, OperationDescription.Name,`|Utilizado para derivar el `wsdl:message` /@name valor para el mensaje de error.|  
  
## <a name="see-also"></a>Vea también

- <xref:System.ServiceModel.Description>
