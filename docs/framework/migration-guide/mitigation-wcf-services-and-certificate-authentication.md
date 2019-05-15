---
title: 'Mitigación: Servicios WCF y autenticación de certificados'
ms.date: 03/30/2017
ms.assetid: ef19c91a-b9df-4bf0-a28e-eb1e99c4bc95
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5f94cabb482a237395854fcdc91df476c567069c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2019
ms.locfileid: "64599508"
---
# <a name="mitigation-wcf-services-and-certificate-authentication"></a>Mitigación: Servicios WCF y autenticación de certificados
.NET Framework 4.6 agrega TLS 1.1 y TLS 1.2 a la lista predeterminada de protocolos SSL de WCF. Cuando los equipos cliente y servidor tienen .NET Framework 4.6 o posterior instalado, se usa TLS 1.2 para la negociación.  
  
## <a name="impact"></a>Impacto  
 TLS 1.2 no admite la autenticación de certificado MD5. Como resultado, si un cliente utiliza un certificado SSL que utiliza MD5 para el algoritmo hash, el cliente WCF no se puede conectar al servicio WCF. Para más información, vea [Mitigación: Servicios WCF y autenticación de certificados](../../../docs/framework/migration-guide/mitigation-wcf-services-and-certificate-authentication.md).  
  
## <a name="mitigation"></a>Mitigación  
 Puede evitar este problema para que el cliente WCF pueda conectarse a un servidor WCF realizando alguno de los siguientes procedimientos:  
  
- Actualizar el certificado para que no use el algoritmo MD5. Esta es la solución recomendada.  
  
- Si la vinculación no se configura dinámicamente en el código fuente, actualice el archivo de configuración de la aplicación para usar TLS 1.1 o una versión anterior del protocolo. Esto le permite seguir usando un certificado con el algoritmo hash MD5.  
  
    > [!CAUTION]
    >  Esta solución no es recomendable, puesto que se considera que el algoritmo hash MD5 no es seguro.  
  
     El archivo de configuración siguiente realiza esta tarea:  
  
    ```xml  
    <configuration>  
        <system.serviceModel>  
            <bindings>  
                <netTcpBinding>  
                    <binding>  
                        <security mode= "None|Transport|Message|TransportWithMessageCredential" >  
                            <transport clientCredentialType="None|Windows|Certificate"  
                                                protectionLevel="None|Sign|EncryptAndSign"  
                                                sslProtocols="Ssl3|Tls1|Tls11">  
                            </transport>  
                        </security>  
                    </binding>  
                </netTcpBinding>  
            </bindings>  
        </system.ServiceModel>  
    </configuration>  
    ```  
  
- Si la vinculación se configura dinámicamente en el código fuente, actualice la propiedad <xref:System.ServiceModel.TcpTransportSecurity.SslProtocols%2A?displayProperty=nameWithType> para usar TLS 1.1 (<xref:System.Security.Authentication.SslProtocols.Tls11?displayProperty=nameWithType>) o una versión anterior del protocolo en el código fuente.  
  
    > [!CAUTION]
    >  Esta solución no es recomendable, puesto que se considera que el algoritmo hash MD5 no es seguro.  
  
## <a name="see-also"></a>Vea también

- [Cambios en el runtime](../../../docs/framework/migration-guide/runtime-changes-in-the-net-framework-4-6.md)
