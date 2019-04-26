---
title: 103 - ActivityStateRecord
ms.date: 03/30/2017
ms.assetid: 57636a9a-561e-44aa-aef9-1f1894aaa6dd
ms.openlocfilehash: 38cec570cffebf6af6d35df481cbec8c7dca8cd1
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61924389"
---
# <a name="103---activitystaterecord"></a>103 - ActivityStateRecord
## <a name="properties"></a>Propiedades  
  
|||  
|-|-|  
|Id.|103|  
|Palabras clave|EndToEndMonitoring, Troubleshooting, HealthMonitoring, WFTracking|  
|Nivel|Información|  
|Canal|Microsoft-Windows-Application Server-Applications/Analytic|  
  
## <a name="description"></a>Descripción  
 El participante de seguimiento de ETW emite este evento cuando una actividad en una instancia de flujo de trabajo emite ActivityStateRecord.  
  
## <a name="message"></a>Mensaje  
 TrackRecord = ActivityStateRecord, InstanceID = %1, RecordNumber=%2, EventTime=%3, State = %4, Name=%5, ActivityId=%6, ActivityInstanceId=%7, ActivityTypeName=%8, Arguments=%9, Variables=%10, Annotations=%11, ProfileName = %12  
  
## <a name="details"></a>Detalles  
  
|Nombre del elemento de datos|Tipo del elemento de datos|Descripción|  
|--------------------|--------------------|-----------------|  
|InstanceId|xs:GUID|El id. de instancia del flujo de trabajo.|  
|RecordNumber|xs:long|El número de secuencia del registro emitido.|  
|EventTime|xs:dateTime|La hora en UTC cuando se emitió el evento.|  
|Estado|xs:string|El estado de la actividad.|  
|Name|xs:string|El nombre para mostrar de la actividad que emitió el evento.|  
|ActivityId|xs:string|El id. de actividad de la actividad que se emite.|  
|ActivityInstance|xs:string|El id. de instancia de la actividad de la actividad que se emite.|  
|ActivityTypeName|xs:string|El nombre del tipo de la actividad que se emite.|  
|Argumentos|xs:string|Los argumentos a los que se realizó el seguimiento con este evento.  Los valores se almacenan en un elemento xml con el formato \<elementos >\< nombre del elemento = "argumentName" Type = "> argumentValue\</artículo >\</Items >.  Si no se realizara el seguimiento de ningún argumento, la cadena contendría \<elementos / >. El tamaño del evento ETW está limitado por el tamaño de búfer de ETW o la carga útil máxima para un evento ETW. Si el tamaño del evento supera los límites de ETW, el evento se trunca quitando las anotaciones y reemplazando el valor de anotación con \<elementos >... \</Items >.  Los tipos siguientes están almacenados como valores posibles ya que los devuelve ToString(); string,char,bool,int,short,long,uint,ushort,ulong,System.Single,float,double,System.Guid,System.DateTimeOffset,System.DateTime.  Todos los demás tipos se serializan con System.Runtime.Serialization.NetDataContractSerializer.|  
|Variables|xs:string|Las variables a las que se realizó el seguimiento con este evento.  Los valores se almacenan en un elemento xml con el formato \<elementos >\< nombre del elemento = "variableName" Type = "> variableValue\</artículo >\</Items >.  Si no se realizara el seguimiento de ninguna variable, la cadena contendría \<elementos / >. El tamaño del evento ETW está limitado por el tamaño de búfer de ETW o la carga útil máxima para un evento ETW. Si el tamaño del evento supera los límites de ETW, el evento se trunca quitando las anotaciones y reemplazando el valor de las variables con \<elementos >... \</Items >.  Los tipos siguientes están almacenados como valores posibles ya que los devuelve ToString(); string,char,bool,int,short,long,uint,ushort,ulong,System.Single,float,double,System.Guid,System.DateTimeOffset,System.DateTime.  Todos los demás tipos se serializan con System.Runtime.Serialization.NetDataContractSerializer.|  
|Anotaciones|xs:string|Las anotaciones que se agregaron a este evento.  Los valores se almacenan en un elemento xml con el formato \<elementos >\< nombre del elemento = "annotationName" Type = "> annotationValue\</artículo >\</Items >.  Si se especifica ninguna anotación, la cadena contendría \<elementos / >. El tamaño del evento ETW está limitado por el tamaño de búfer de ETW o la carga útil máxima para un evento ETW. Si el tamaño del evento supera los límites de ETW, el evento se trunca quitando las anotaciones y reemplazando el valor de anotación con \<elementos >... \</Items >.|  
|ProfileName|xs:string|El nombre o el perfil de seguimiento que dio como resultado que se emitiera este evento.|  
|HostReference|xs:string|En el caso de los servicios hospedados en web, este campo identifica de manera única el servicio en la jerarquía web.  Su formato se define como ' ruta de acceso Virtual de sitio Web de nombre de la aplicación&#124;ruta de acceso Virtual del servicio&#124;NombreServicio ' ejemplo: ' Default Web Site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService'|  
|AppDomain|xs:string|La cadena devuelta por AppDomain.CurrentDomain.FriendlyName.|
