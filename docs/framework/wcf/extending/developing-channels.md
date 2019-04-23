---
title: Desarrollo de canales
ms.date: 03/30/2017
ms.assetid: 0513af9f-a0c2-457b-9a50-5b6bfee48513
ms.openlocfilehash: 44fb0da52c60b900c41b7b497861c12ed72d8ffc
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59334548"
---
# <a name="developing-channels"></a>Desarrollo de canales
Para desarrollar un canal de transporte o protocolo que se puede usar con Windows Communication Foundation (WCF), capa de aplicación requiere varios pasos. En este tema se describen esos pasos y se le dirige a temas con información específica. Para entender el modelo del canal y los distintos tipos que se mencionan en este tema, consulte [información general del modelo de canal](../../../../docs/framework/wcf/extending/channel-model-overview.md). Para obtener un ejemplo de canal de transporte completo, vea [transporte: UDP](../../../../docs/framework/wcf/samples/transport-udp.md).  
  
## <a name="the-channel-development-task-list"></a>La lista de tareas de desarrollo de canal  
 Los pasos para crear un canal definido por el usuario son como sigue. Todos los canales deben:  
  
1. Decidir qué patrones de intercambio de mensajes de canal (<xref:System.ServiceModel.Channels.IOutputChannel>, <xref:System.ServiceModel.Channels.IInputChannel>, <xref:System.ServiceModel.Channels.IDuplexChannel>, <xref:System.ServiceModel.Channels.IRequestChannel> o <xref:System.ServiceModel.Channels.IReplyChannel>) <xref:System.ServiceModel.Channels.IChannelFactory> y <xref:System.ServiceModel.Channels.IChannelListener> admitirán, así como si serán compatibles las variaciones con sesión de estas interfaces. Para obtener más información, consulte [elegir un patrón de intercambio de mensajes](../../../../docs/framework/wcf/extending/choosing-a-message-exchange-pattern.md).  
  
2. Cree un generador de canales y un agente de escucha (<xref:System.ServiceModel.Channels.IChannelFactory> y <xref:System.ServiceModel.Channels.IChannelListener>) que admitan su patrón de intercambio de mensajes. Para obtener más información sobre cómo desarrollar los generadores, vea [cliente: Generadores de canales y canales](../../../../docs/framework/wcf/extending/client-channel-factories-and-channels.md). Para obtener más información sobre el desarrollo de los agentes de escucha, vea [servicio: Canales y escuchas de canales](../../../../docs/framework/wcf/extending/service-channel-listeners-and-channels.md).  
  
3. Asegurarse de que cualquier excepción específica de la red se normaliza a <xref:System.TimeoutException?displayProperty=nameWithType> o a la clase derivada adecuada de <xref:System.ServiceModel.CommunicationException>. Para obtener más información, consulte [control de excepciones y errores](../../../../docs/framework/wcf/extending/handling-exceptions-and-faults.md).  
  
4. Para habilitar el uso del nivel de aplicación, agregue un <xref:System.ServiceModel.Channels.BindingElement> que añade el canal personalizado a una pila del canal. Para obtener más información, consulte [creación de un BindingElement](../../../../docs/framework/wcf/extending/creating-a-bindingelement.md).  
  
 Son necesarios pasos adicionales para permitir una compatibilidad más completa en el nivel de la aplicación:  
  
1. Agregue una sección de extensión de elemento de enlace para exponer el nuevo elemento de enlace al sistema de configuración. Para obtener más información, consulte [configuración y compatibilidad con metadatos](../../../../docs/framework/wcf/extending/configuration-and-metadata-support.md).  
  
2. Agregue las extensiones de metadatos para comunicar las funciones a otros puntos de conexión. Para obtener más información, consulte [configuración y compatibilidad con metadatos](../../../../docs/framework/wcf/extending/configuration-and-metadata-support.md).  
  
3. Agregue un enlace que configura previamente una pila de elementos de enlace según un perfil bien determinado. Para obtener más información, consulte [crear enlaces](../../../../docs/framework/wcf/extending/creating-user-defined-bindings.md).  
  
4. Agregue una sección de enlace y un elemento de configuración de enlace para exponer el enlace al sistema de configuración. Para obtener más información, consulte [configuración y compatibilidad con metadatos](../../../../docs/framework/wcf/extending/configuration-and-metadata-support.md).  
  
## <a name="see-also"></a>Vea también

- [Extensión de enlaces](../../../../docs/framework/wcf/extending/extending-bindings.md)
