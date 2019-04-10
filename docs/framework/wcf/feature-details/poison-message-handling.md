---
title: Control de mensajes dudosos
ms.date: 03/30/2017
ms.assetid: 8d1c5e5a-7928-4a80-95ed-d8da211b8595
ms.openlocfilehash: fe748ac40f03ed22cacb254ab464a6caf3d27a8c
ms.sourcegitcommit: 558d78d2a68acd4c95ef23231c8b4e4c7bac3902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2019
ms.locfileid: "59305031"
---
# <a name="poison-message-handling"></a>Control de mensajes dudosos
Un *mensaje dudoso* es un mensaje que ha superado el número máximo de intentos de entrega a la aplicación. Esta situación se puede presentar cuando una aplicación basada en cola no puede procesar un mensaje debido a los errores. Para satisfacer la confiabilidad que exige, una aplicación en cola recibe los mensajes bajo una transacción. Anular la transacción en la que un mensaje en cola se recibió deja el mensaje en la cola para que el mensaje se vuelva a intentar con una nueva transacción. Si no se corrige el problema que produjo la anulación de la transacción, la aplicación receptora se puede atascar en una recepción de bucle y anulando el mismo mensaje hasta que supere el número máximo de intentos de entrega, y se produzca un mensaje dudoso.  
  
 Un mensaje se puede volver un mensaje dudoso por muchas razones. Las razones más comunes son específicas de la aplicación. Por ejemplo, si una aplicación lee un mensaje de una cola y realiza algún procesamiento de base de datos, es posible que la aplicación no pueda obtener un bloqueo en la base de datos, haciendo que se anule la transacción. Dado que la transacción de base de datos se anula, el mensaje permanece en la cola, lo que hace que la aplicación vuelva a leer el mensaje una segunda vez y realice otro intento de adquirir un bloqueo en la base de datos. Los mensajes también se pueden volver dudosos si contienen la información no válida. Por ejemplo, un pedido de compra puede contener un número del cliente no válido. En estos casos, la aplicación puede anular voluntariamente la transacción y forzar al mensaje a convertirse en un mensaje dudoso.  
  
 En raras ocasiones, se puede producir un error en la distribución a la aplicación. La capa de Windows Communication Foundation (WCF) puede encontrar un problema con el mensaje, como si el mensaje tiene un marco incorrecto, adjuntas credenciales de mensaje no válido para la base de datos o un encabezado de acción no válido. En estos casos, la aplicación nunca recibe el mensaje; sin embargo, el mensaje todavía se puede convertir en un mensaje dudoso y procesar manualmente.  
  
## <a name="handling-poison-messages"></a>Control de mensajes dudosos  
 En WCF, control de mensajes dudosos proporciona un mecanismo para una aplicación receptora trate con mensajes que no se pueden enviar a la aplicación, o que se envían a la aplicación pero que no puedan procesarse debido a específicos de la aplicación motivos. El control de mensajes dudosos se configura mediante las siguientes propiedades en cada uno de los enlaces en cola disponibles:  
  
-   `ReceiveRetryCount`. Un valor entero que indica el número máximo de horas para reintentar la entrega de un mensaje de la cola de la aplicación a la aplicación. El valor predeterminado es 5. Esto es suficiente en casos donde un reintento inmediato corrige el problema, como ocurre con un interbloqueo temporal en una base de datos.  
  
-   `MaxRetryCycles`. Un valor entero que indica el número máximo de ciclos de reintento. Un ciclo de reintento consiste en transferir un mensaje de la cola de la aplicación a una subcola de intento y, después de un retraso configurable, de la subcola de intento de vuelta a la cola de la aplicación para reintentar la entrega. El valor predeterminado es 2. En [!INCLUDE[wv](../../../../includes/wv-md.md)], el mensaje se intenta un máximo de (`ReceiveRetryCount` +1) * (`MaxRetryCycles` + 1) veces. `MaxRetryCycles` se omite en [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] y [!INCLUDE[wxp](../../../../includes/wxp-md.md)].  
  
-   `RetryCycleDelay`. El tiempo de retardo entre los ciclos de reintento. El valor predeterminado es de 30 minutos. `MaxRetryCycles` y `RetryCycleDelay` juntos proporcionan un mecanismo para resolver el problema donde un reintento después de un retraso periódico corrige el problema. Por ejemplo, esto controla un conjunto de filas bloqueado en confirmación de la transacción pendiente de SQL Server.  
  
-   `ReceiveErrorHandling`. Una enumeración que indica la acción a realizar para un mensaje en el que se ha producido un error tras intentar el número máximo de reintentos. Los valores pueden ser Fault, Drop, Reject, y Move. La opción de unidad predeterminada es Fault.  
  
-   Fault. Esta opción envía un error al agente de escucha que provocó el error en `ServiceHost`. El mensaje debe ser eliminado de la cola de la aplicación por algún mecanismo externo antes de que la aplicación pueda continuar procesando los mensajes de la cola.  
  
-   Drop. Esta opción quita el mensaje dudoso y el mensaje nunca llega a la aplicación. Si la propiedad `TimeToLive` del mensaje ha expirado en este punto, el mensaje puede aparecer en la cola de mensajes no enviados del remitente. Si no, el mensaje no aparece en ningún sitio. Esta opción indica que el usuario no ha especificado qué hacer si se pierde el mensaje.  
  
-   Reject. Esta opción solo está disponible en [!INCLUDE[wv](../../../../includes/wv-md.md)]. Indica a Message Queuing (MSMQ) que devuelva una confirmación de que no se pudo realizar la acción al administrador de la cola emisora para indicar que la aplicación no puede recibir el mensaje. El mensaje se coloca en la cola de mensajes no enviados del administrador de la cola emisora.  
  
-   Move. Esta opción solo está disponible en [!INCLUDE[wv](../../../../includes/wv-md.md)]. Mueve el mensaje dudoso a una cola de mensajes dudosos para ser procesado posteriormente por una aplicación de control de mensajes dudosos. La cola de mensajes dudosos es una subcola de la cola de la aplicación. Una aplicación de mensajes dudosos puede ser un servicio WCF que lee los mensajes fuera de la cola de mensajes dudosos. La cola de mensajes dudosos es una subcola de la cola de aplicación y se puede direccionar como net.msmq://\<*nombre-equipo*>/*applicationQueue*; poison, donde  *nombre de la máquina* es el nombre del equipo en el que reside la cola y el *applicationQueue* es el nombre de la cola específica de la aplicación.  
  
 A continuación, se muestra el número máximo de intentos de entrega realizados para un mensaje:  
  
-   ((ReceiveRetryCount+1) * (MaxRetryCycles + 1)) en [!INCLUDE[wv](../../../../includes/wv-md.md)].  
  
-   (ReceiveRetryCount + 1) en [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] y [!INCLUDE[wxp](../../../../includes/wxp-md.md)].  
  
> [!NOTE]
>  No se realiza ningún reintento para un mensaje que se entrega correctamente.  
  
 Para realizar un seguimiento del número de veces que se intenta leer un mensaje, [!INCLUDE[wv](../../../../includes/wv-md.md)] mantiene una propiedad de mensaje duradero que cuenta el número de anulaciones y una propiedad de recuento de movimiento que cuenta el número de veces que el mensaje se mueve entre la cola de la aplicación y las subcolas. El canal WCF utiliza para calcular el número de reintentos de recepción y el recuento de ciclos de reintento. En [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] y [!INCLUDE[wxp](../../../../includes/wxp-md.md)], el recuento de anulación se mantiene en memoria por el canal WCF y se restablece si se produce un error en la aplicación. Además, el canal WCF puede contener que recuentos de la anulación para hasta 256 mensajes en la memoria en cualquier momento. Si se lee el mensaje número 257, se restablece el recuento de la anulación del mensaje más antiguo.  
  
 Las propiedades de recuento de la anulación y recuento de movimiento están disponibles para la operación del servicio a través del contexto de la operación. En el ejemplo de código siguiente se muestra cómo obtener acceso.  
  
 [!code-csharp[S_UE_MSMQ_Poison#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ue_msmq_poison/cs/service.cs#1)]  
  
 WCF proporciona dos enlaces en cola estándares:  
  
-   <xref:System.ServiceModel.NetMsmqBinding>. Un [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] enlace adecuado para realizar la comunicación basada en cola con otros extremos WCF.  
  
-   <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>. Un enlace conveniente para comunicar con aplicaciones Message Queuing existentes.  
  
> [!NOTE]
>  Puede modificar las propiedades de estos enlaces basándose en los requisitos de su servicio WCF. Todo el mecanismo de control de mensajes dudosos es local a la aplicación receptora. El proceso es invisible para la aplicación emisora a menos que la aplicación receptora se detenga finalmente y devuelva una confirmación de que no se pudo realizar la acción al remitente. En ese caso, el mensaje se mueve a la cola de mensajes no enviados del remitente.  
  
## <a name="best-practice-handling-msmqpoisonmessageexception"></a>Procedimiento recomendado: Controlar MsmqPoisonMessageException  
 Cuando el servicio determina que un mensaje es dudoso, el transporte en cola arroja <xref:System.ServiceModel.MsmqPoisonMessageException> que contiene `LookupId` del mensaje dudoso.  
  
 Una aplicación receptora puede implementar la interfaz <xref:System.ServiceModel.Dispatcher.IErrorHandler> para controlar cualquier error que la aplicación requiera. Para obtener más información, consulte [extender Control sobre el control de errores e informes](../../../../docs/framework/wcf/samples/extending-control-over-error-handling-and-reporting.md).  
  
 La aplicación puede requerir algún tipo de control automatizado de mensajes dudosos que los aparte a una cola específica de manera que el servicio pueda tener acceso al resto de los mensajes de la cola. El único escenario para utilizar el mecanismo del controlador de errores para realizar escuchas para las excepciones de mensajes dudosos es cuando <xref:System.ServiceModel.Configuration.MsmqBindingElementBase.ReceiveErrorHandling%2A> está establecido en <xref:System.ServiceModel.ReceiveErrorHandling.Fault>. El ejemplo de mensaje dudoso para Message Queuing 3.0 demuestra este comportamiento. A continuación se dibujan los pasos a realizar para controlar los mensajes dudosos, incluyendo los procedimientos recomendados:  
  
1. Asegúrese de que la configuración de mensajes dudosos refleja los requisitos de la aplicación. Al trabajar con los valores, asegúrese de que entienda las diferencias entre las funciones de Message Queuing en [!INCLUDE[wv](../../../../includes/wv-md.md)], [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]y [!INCLUDE[wxp](../../../../includes/wxp-md.md)].  
  
2. Si se requiere, implemente `IErrorHandler` para controlar los errores de los mensajes dudosos. Dado que al establecer `ReceiveErrorHandling` en `Fault` se requiere un mecanismo manual para quitar el mensaje dudoso de la cola o corregir un problema derivado externo, lo normal es implementar `IErrorHandler` cuando `ReceiveErrorHandling` se establece en `Fault`, como se muestra en el código siguiente.  
  
     [!code-csharp[S_UE_MSMQ_Poison#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ue_msmq_poison/cs/poisonerrorhandler.cs#2)]  
  
3. Cree un `PoisonBehaviorAttribute` que pueda usar el comportamiento del servicio. El comportamiento instala `IErrorHandler` en el distribuidor. Vea el ejemplo de código siguiente.  
  
     [!code-csharp[S_UE_MSMQ_Poison#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ue_msmq_poison/cs/poisonbehaviorattribute.cs#3)]  
  
4. Asegúrese de que su servicio se anote con el atributo de comportamiento de mensajes venenosos.  

 Además, si `ReceiveErrorHandling` se establece en `Fault`, `ServiceHost` genera un error al encontrar el mensaje dudoso. Puede enlazarlo con el evento que ha generado el error y cerrar el servicio, tomar medidas correctivas y reiniciarlo. Por ejemplo, puede tomar nota del `LookupId` de la <xref:System.ServiceModel.MsmqPoisonMessageException> propagada a `IErrorHandler` y, cuando el host de servicio genere el error, puede utilizar la API `System.Messaging` para recibir el mensaje de la cola, utilizando el `LookupId` para quitarlo de la cola y almacenarlo en algún almacén externo u otra cola. Puede reiniciar a continuación `ServiceHost` para reanudar el procesamiento normal. El [control de mensajes dudosos en MSMQ 4.0](../../../../docs/framework/wcf/samples/poison-message-handling-in-msmq-4-0.md) demuestra este comportamiento.  
  
## <a name="transaction-time-out-and-poison-messages"></a>Tiempo de espera de la transacción y mensajes dudosos  
 Una clase de errores se puede producir entre el canal de transporte en cola y el código de usuario. Estos errores pueden ser detectados por niveles intermedios, como el nivel de seguridad de mensajes o el servicio que distribuye la lógica. Por ejemplo, cuando se detecta la ausencia de un certificado X.509 en el nivel de seguridad SOAP y la ausencia de una acción son casos en los que el mensaje no se distribuye a la aplicación. Cuando esto sucede, el modelo de servicio quita el mensaje. Puesto que el mensaje se lee en una transacción y no se puede proporcionar un resultado para la misma, la transacción agota el tiempo de espera, se anula y el mensaje se pone de nuevo en la cola. En otras palabras, para una cierta clase de errores, la transacción no anula inmediatamente sino que espera hasta que se agote el tiempo de espera. Puede modificar el tiempo de espera de la transacción para un servicio utilizando <xref:System.ServiceModel.ServiceBehaviorAttribute>.  
  
 Para cambiar el tiempo de espera de la transacción para todos los equipos, modifique el archivo machine.config y establezca el tiempo de espera adecuado de la transacción. Es importante tener en cuenta que, dependiendo del tiempo de espera establecido en la transacción, la transacción finalmente se anula y regresa a la cola, incrementándose su número de anulación. Finalmente, el mensaje se convierte en dudoso y se elimina de la forma que especifique la configuración del usuario.  
  
## <a name="sessions-and-poison-messages"></a>Sesiones y mensajes dudosos  
 Una sesión sufre los mismos procedimientos de reintento y control de mensajes dudosos como un mensaje único. Las propiedades enumeradas anteriormente para los mensajes dudosos se aplican a toda la sesión. Esto significa que se reintenta la sesión completa y se envía a una cola de mensajes dudosos final o a la cola de mensajes no enviados del remitente si se rechaza el mensaje.  
  
## <a name="batching-and-poison-messages"></a>Procesamiento por lotes y mensajes dudosos  
 Si un mensaje se vuelve un mensaje dudoso y es parte de un lote, se deshace el lote completo y el canal vuelve a leer un mensaje cada vez. Para obtener más información sobre el procesamiento por lotes, vea [mensajes por lotes en una transacción](../../../../docs/framework/wcf/feature-details/batching-messages-in-a-transaction.md)  
  
## <a name="poison-message-handling-for-messages-in-a-poison-queue"></a>Control de mensajes dudosos para mensajes en una cola de mensajes dudosos  
 El control de mensajes dudosos no finaliza cuando un mensaje se coloca en la cola de mensajes dudosos. Los mensajes de la cola de mensajes dudosos también se deben leer y controlar. Puede utilizar un subconjunto de los valores de control de mensajes dudosos al leer mensajes de la subcola final de mensajes dudosos. La configuración aplicable es `ReceiveRetryCount` y `ReceiveErrorHandling`. Puede establecer `ReceiveErrorHandling` en Drop, Reject o Fault. `MaxRetryCycles` se omite y se produce una excepción si `ReceiveErrorHandling` se establece en Move.  
  
## <a name="windows-vista-windows-server-2003-and-windows-xp-differences"></a>Diferencias entre Windows Vista, Windows Server 2003, y Windows XP  
 Como se ha apuntado anteriormente, no todos los valores de control de mensajes dudosos son aplicables a [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] y [!INCLUDE[wxp](../../../../includes/wxp-md.md)]. Las siguientes diferencias clave entre Message Queuing (MSMQ) en [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)], [!INCLUDE[wxp](../../../../includes/wxp-md.md)] y [!INCLUDE[wv](../../../../includes/wv-md.md)] son pertinentes para el control de mensajes dudosos:  
  
-   Message Queuing en [!INCLUDE[wv](../../../../includes/wv-md.md)] admite subcolas, mientras que [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] y [!INCLUDE[wxp](../../../../includes/wxp-md.md)] no admiten subcolas. Las subcolas se utilizan en el control de mensajes dudosos. Las colas de reintento y la cola dudosa son subcolas en la cola de la aplicación que se crea dependiendo de los valores de control del mensaje dudoso. `MaxRetryCycles` dicta cuántas subcolas de reintento se crean. Por lo tanto, cuando se ejecutan en [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] o [!INCLUDE[wxp](../../../../includes/wxp-md.md)], `MaxRetryCycles` se omiten y no se permite `ReceiveErrorHandling.Move`.  
  
-   Message Queuing en [!INCLUDE[wv](../../../../includes/wv-md.md)] admite una confirmación de que no se pudo realizar la acción, mientras que [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] y [!INCLUDE[wxp](../../../../includes/wxp-md.md)] no. Una confirmación de que no se pudo realizar la acción del administrador de la cola receptora hace que el administrador de la cola emisora coloque el mensaje rechazado en la cola de mensajes no enviados. Como tal, `ReceiveErrorHandling.Reject` no se permite con [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] y [!INCLUDE[wxp](../../../../includes/wxp-md.md)].  
  
-   Message Queuing en [!INCLUDE[wv](../../../../includes/wv-md.md)] admite una propiedad de mensaje que mantiene un recuento del número de veces que se intenta la entrega del mensaje. Esta propiedad de recuento de anulación no está disponible en [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] y [!INCLUDE[wxp](../../../../includes/wxp-md.md)]. WCF mantiene el recuento de anulación en memoria, por lo que es posible que esta propiedad no puede contener un valor preciso cuando el mismo mensaje es leído por más de un servicio WCF en una granja de servidores.  
  
## <a name="see-also"></a>Vea también

- [Información general de colas](../../../../docs/framework/wcf/feature-details/queues-overview.md)
- [Diferencias en las características de cola en Windows Vista, Windows Server 2003 y Windows XP](../../../../docs/framework/wcf/feature-details/diff-in-queue-in-vista-server-2003-windows-xp.md)
- [Especificación y administración de errores en contratos y servicios](../../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)
