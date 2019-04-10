---
title: Codificación MTOM
ms.date: 03/30/2017
ms.assetid: 820e316f-4ee1-4eb5-ae38-b6a536e8a14f
ms.openlocfilehash: abca7810e9d414808ddc195b95de05922edb6238
ms.sourcegitcommit: 558d78d2a68acd4c95ef23231c8b4e4c7bac3902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2019
ms.locfileid: "59323140"
---
# <a name="mtom-encoding"></a>Codificación MTOM
Este ejemplo muestra el uso de la codificación de mensajes del Mecanismo de optimización de transmisión del mensaje (MTOM) con WSHttpBinding. MTOM es un mecanismo para transmitir los datos adjuntos binarios grandes con mensajes SOAP como bytes sin formato, permitiendo los mensajes menores.  
  
> [!IMPORTANT]
>  Puede que los ejemplos ya estén instalados en su equipo. Compruebe el siguiente directorio (predeterminado) antes de continuar.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Si no existe este directorio, vaya a [Windows Communication Foundation (WCF) y Windows Workflow Foundation (WF) Samples para .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los Windows Communication Foundation (WCF) y [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ejemplos. Este ejemplo se encuentra en el siguiente directorio.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\WS\MTOM`  
  
 De forma predeterminada, WSHttpBinding envía y recibe los mensajes como texto normal XML. Para habilitar la recepción y el envío de los mensajes MTOM, establezca el atributo `messageEncoding` en la configuración (como en el código de ejemplo siguiente) del enlace o directamente en el enlace utilizando la propiedad `MessageEncoding`. El servicio o cliente puede enviar y recibir ahora los mensajes MTOM.  
  
```xml  
<wsHttpBinding>  
  <binding name="WSHttpBinding_IUpload" messageEncoding="Mtom" />  
</wsHttpBinding>  
```  
  
 El codificador MTOM puede optimizar matrices de bytes y secuencias. En este ejemplo, la operación utiliza un parámetro `Stream` y, por consiguiente, puede optimizarse.  

```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
  public interface IUpload  
  {  
      [OperationContract]  
      int Upload(Stream data);  
  }  
```
  
 El contrato elegido porque este ejemplo transmite los datos binarios al servicio y recibe el número de bytes cargado como el valor devuelto. Cuando se instala el servicio y se ejecuta el cliente, imprime el número 1000, que indica que se recibieron 1000 bytes por completo. El resto de las listas de salida optimizó y no optimizó los tamaños del mensaje para varias cargas útiles.  
  
```  
Output:  
1000  
  
Text encoding with a 100 byte payload: 433  
MTOM encoding with a 100 byte payload: 912  
  
Text encoding with a 1000 byte payload: 1633  
MTOM encoding with a 1000 byte payload: 2080  
  
Text encoding with a 10000 byte payload: 13633  
MTOM encoding with a 10000 byte payload: 11080  
  
Text encoding with a 100000 byte payload: 133633  
MTOM encoding with a 100000 byte payload: 101080  
  
Text encoding with a 1000000 byte payload: 1333633  
MTOM encoding with a 1000000 byte payload: 1001080  
  
Press <ENTER> to terminate client.  
```  
  
 El propósito para utilizar MTOM es optimizar la transmisión de grandes cargas útiles binarias. Al enviar un mensaje SOAP mediante MTOM, se tiene una sobrecarga notable para las cargas útiles binarias pequeñas, pero implica un gran ahorro cuando la cifra se eleva a unos miles de bytes. La razón es que el texto normal XML codifica datos binarios mediante Base64, lo cual requiere cuatro caracteres para cada tres bytes, y aumenta el tamaño de los datos en un tercio. MTOM puede transmitir los datos binarios como bytes sin formato, guardando el tiempo de codificación/descodificando y lo que resulta son los mensajes menores. El umbral de unos miles de bytes es pequeño cuando se compara con los documentos comerciales y las fotos digitales de hoy en día.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>Configurar, compilar y ejecutar el ejemplo  
  
1. Instale [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 4.0 mediante el siguiente comando.  
  
    ```  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
    ```  
  
2. Asegúrese de que ha realizado la [procedimiento de instalación de un solo uso para los ejemplos de Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
3. Para compilar el código C# o Visual Basic .NET Edition de la solución, siga las instrucciones de [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
4. Para ejecutar el ejemplo en una configuración de equipos única o cruzada, siga las instrucciones de [ejecutando los ejemplos de Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
