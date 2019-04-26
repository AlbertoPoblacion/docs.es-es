---
title: Canal local
ms.date: 03/30/2017
ms.assetid: fa1917a4-f701-4e82-a439-14a16282c7cc
ms.openlocfilehash: 1711909ada4756dd2723f62160eef0ad12c03174
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61989838"
---
# <a name="local-channel"></a>Canal local
Canal local es un canal de transporte de Windows Communication Foundation (WCF) que se usa para la comunicación dentro del mismo dominio de aplicación. Esto es útil para los escenarios donde el cliente y el servicio se están ejecutando en el mismo dominio de aplicación y la sobrecarga de la pila del canal WCF típica (la serialización y deserialización de mensajes) se debe evitar.  
  
## <a name="demonstrates"></a>Demostraciones  
 Canal local  
  
## <a name="discussion"></a>Discusión  
 El ejemplo consta de dos archivos de proyecto:  
  
-   **LocalChannel**: La representación de programación del canal local dentro del dominio de aplicación actual. En este proyecto, el componente de envío coloca el mensaje en una cola en memoria y el componente receptor saca el mensaje de la cola para recibirlo.  
  
-   **ClientAndService**: Este proyecto hospeda un servicio en una aplicación de consola y, a continuación, ejecuta un cliente para llamar al servicio desde dentro del mismo dominio de aplicación.  
  
 El diseño del canal local omite la pila del canal y el proceso de serialización para aumentar la velocidad. El canal de transporte local se implementa utilizando una cola para las llamadas del servicio de transporte desde el cliente al servicio y para devolver el valor al cliente. En lugar de serializar los parámetros y los valores devueltos, en el ejemplo se copian los objetos.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Configurar, compilar y ejecutar el ejemplo  
  
1. Compile y ejecute la solución LocalChannel.  
  
2. El host del servicio se inicia y el cliente llama al servicio utilizando el canal local. Una ventana de la consola aparece para mostrar los resultados de la llamada del servicio.  
  
> [!IMPORTANT]
>  Puede que los ejemplos ya estén instalados en su equipo. Compruebe el siguiente directorio (predeterminado) antes de continuar.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Si no existe este directorio, vaya a [Windows Communication Foundation (WCF) y Windows Workflow Foundation (WF) Samples para .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los Windows Communication Foundation (WCF) y [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ejemplos. Este ejemplo se encuentra en el siguiente directorio.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Channels\LocalChannel`
