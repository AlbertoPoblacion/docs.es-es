---
title: MsmqBindingElementBase
ms.date: 03/30/2017
ms.assetid: 210d41ab-a2a4-4d7a-afd2-0916c08a4015
ms.openlocfilehash: 1df4b32feda246a536183a42ac11b113bc4bb259
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61963441"
---
# <a name="msmqbindingelementbase"></a>MsmqBindingElementBase
MsmqBindingElementBase  
  
## <a name="syntax"></a>Sintaxis  
  
```csharp  
class MsmqBindingElementBase : TransportBindingElement  
{  
  string CustomDeadLetterQueue;  
  string DeadLetterQueue;  
  boolean Durable;  
  boolean ExactlyOnce;  
  sint32 MaxRetryCycles;  
  string ReceiveErrorHandling;  
  sint32 ReceiveRetryCount;  
  datetime RetryCycleDelay;  
  datetime TimeToLive;  
  boolean UseMsmqTracing;  
  boolean UseSourceJournal;  
};  
```  
  
## <a name="methods"></a>Métodos  
 La clase TraceListenerArgument no define ningún método.  
  
## <a name="properties"></a>Propiedades  
 La clase MsmqBindingElementBase tiene las siguientes propiedades:  
  
### <a name="customdeadletterqueue"></a>CustomDeadLetterQueue  
 Tipo de datos: cadena  
  
 Tipo de acceso: De sólo lectura  
  
 Un URI que contiene la ubicación de la cola de mensajes no enviados de cada aplicación, donde se colocan los mensajes que han expirado o cuya transferencia o envío han fallado.  
  
### <a name="deadletterqueue"></a>DeadLetterQueue  
 Tipo de datos: cadena  
  
 Tipo de acceso: De sólo lectura  
  
 Un valor de enumeración que indica el tipo de cola de mensajes no enviados que se ha de usar.  
  
### <a name="durable"></a>Durable  
 Tipo de datos: booleano  
  
 Tipo de acceso: De sólo lectura  
  
 Un valor que indica si los mensajes procesados por este enlace son duraderos o volátiles.  
  
### <a name="exactlyonce"></a>ExactlyOnce  
 Tipo de datos: booleano  
  
 Tipo de acceso: De sólo lectura  
  
 Un valor booleano que indica si los mensajes procesados por este enlace se reciben solo una vez.  
  
### <a name="maxretrycycles"></a>MaxRetryCycles  
 Tipo de datos: sint32  
  
 Tipo de acceso: De sólo lectura  
  
 El número máximo de ciclos de reintento de entrega de mensajes a la aplicación receptora.  
  
### <a name="receiveerrorhandling"></a>ReceiveErrorHandling  
 Tipo de datos: cadena  
  
 Tipo de acceso: De sólo lectura  
  
 Los valores para el control de mensajes dudosos.  
  
### <a name="receiveretrycount"></a>ReceiveRetryCount  
 Tipo de datos: sint32  
  
 Tipo de acceso: De sólo lectura  
  
 El número máximo de intentos de reintento inmediato en un mensaje que se lee desde la cola de la aplicación.  
  
### <a name="retrycycledelay"></a>RetryCycleDelay  
 Tipo de datos: datetime  
  
 Tipo de acceso: De sólo lectura  
  
 Un valor que indica el tiempo de retardo entre los ciclos de reintento al intentar entregar un mensaje que no se pudo entregar inmediatamente.  
  
### <a name="timetolive"></a>TimeToLive  
 Tipo de datos: datetime  
  
 Tipo de acceso: De sólo lectura  
  
 El intervalo de tiempo que indica cuánto tiempo pueden estar en la cola los mensajes procesados por este enlace antes de expirar.  
  
### <a name="usemsmqtracing"></a>UseMsmqTracing  
 Tipo de datos: booleano  
  
 Tipo de acceso: De sólo lectura  
  
 Un valor booleano que indica si los mensajes procesados por este enlace se deberían seguir paso a paso.  
  
### <a name="usesourcejournal"></a>UseSourceJournal  
 Tipo de datos: booleano  
  
 Tipo de acceso: De sólo lectura  
  
 Un valor booleano que indica si las copias de mensajes procesados por este enlace deberían almacenarse en la cola de diario de origen.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Se declara en Servicemodel.mof.|  
|---------|-----------------------------------|  
|Espacio de nombres|Se define en root\ServiceModel|  
  
## <a name="see-also"></a>Vea también

- <xref:System.ServiceModel.NetMsmqBinding>
- <xref:System.ServiceModel.MsmqBindingBase>
