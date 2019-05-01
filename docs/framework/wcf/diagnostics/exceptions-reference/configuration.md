---
title: Configuración
ms.date: 03/30/2017
ms.assetid: 86a6e12f-73b5-450e-8725-f4ca5fe0702c
ms.openlocfilehash: 3ef91a1f851f87ebf35669748f8beb1c6a880ae8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61998821"
---
# <a name="configuration"></a>Configuración
En este tema se enumera todas las excepciones generadas por la configuración de Windows Communication Foundation (WCF).  
  
## <a name="exception-list"></a>Lista de excepciones  
  
|Código de recurso|Cadena de recurso|  
|-------------------|---------------------|  
|ConfigBindingCannotBeConfigured|No se puede configurar el enlace en el punto de conexión de servicio.|  
|ConfigElementKeyNull|La clave de elemento de configuración concreta no puede ser NULL.|  
|ConfigExtensionTypeNotRegisteredInCollection|El tipo de extensión concreto no está registrado en la colección de extensión concreta.|  
|ConfigIndexOutOfRange|El valor para el atributo concreto está fuera del intervalo.|  
|ConfigInvalidBindingConfigurationName|La configuración concreta no tiene un enlace con el nombre específico.|  
|ConfigInvalidBindingName|La configuración concreta no tiene un enlace con el nombre específico. Éste es un valor no válido para el enlace.|  
|ConfigInvalidCommonEndpointBehaviorType|No pueda agregar la extensión de comportamiento concreta al comportamiento del extremo común porque no implementa el tipo específico.|  
|ConfigInvalidCommonServiceBehaviorType|No pueda agregar la extensión de comportamiento concreta al comportamiento del servicio común porque no implementa el tipo específico.|  
|ConfigInvalidEndpointBehaviorType|No pueda agregar la extensión de comportamiento concreta al comportamiento del punto de conexión concreto porque el tipo de comportamiento subyacente no implementa la interfaz IServiceBehavior.|  
|ConfigInvalidExtensionType|El tipo específico debe derivar de la extensión concreta para que se utilice en la colección.|  
|ConfigInvalidServiceBehaviorType|No pueda agregar la extensión de comportamiento al comportamiento de servicio con el nombre específico porque el tipo de comportamiento subyacente no implementa la interfaz IServiceBehavior.|  
|ConfigMessageEncodingAlreadyInBinding|No puede agregar el elemento de codificación de mensajes concreto. Otro elemento de codificación de mensajes ya existe en el enlace concreto. Solo puede haber un elemento de codificación de mensajes para cada enlace.|  
|ConfigNoExtensionCollectionAssociatedWithType|No puede encontrar la colección de extensiones asociada a la extensión del tipo específico.|  
|ConfigSectionNotFound|No se puede crear la sección de configuración concreta. Al archivo Machine.config le falta información. Compruebe que esta sección de configuración esté correctamente registrada y que ha escrito correctamente el nombre de sección. Para las secciones Windows Communication Foundation, ejecute ServiceModelReg.exe -i para corregir este error.|  
|ConfigTransportAlreadyInBinding|No puede agregar el elemento de transporte concreto. Otro elemento de transporte ya existe en el enlace concreto. Solo puede haber un elemento de codificación de mensajes para cada enlace.|
