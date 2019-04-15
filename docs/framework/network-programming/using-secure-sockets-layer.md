---
title: Usar la capa de sockets seguros
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Networking
- SSL
- Secure Sockets Layer
- requesting data from Internet, Secure Sockets Layer
- sending data, Secure Sockets Layer
- Network Resources
- data requests, Secure Sockets Layer
- receiving data, Secure Sockets Layer
- Internet, Secure Sockets Layer
ms.assetid: 6e4289e6-d1b7-4e82-ab0d-e83e3b6063ed
ms.openlocfilehash: a0af2fa8bbe2efb2dc4fb3d1177c4950dcec87cf
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59135811"
---
# <a name="using-secure-sockets-layer"></a>Usar la capa de sockets seguros
Las clases <xref:System.Net> usan la Capa de sockets seguros (SSL) para cifrar la conexión de varios protocolos de red.  
  
 Para las conexiones http, las clases <xref:System.Net.WebRequest> y <xref:System.Net.WebResponse> usan SSL para comunicarse con hosts web que admiten SSL. Es la clase <xref:System.Net.WebRequest> la que toma la decisión de usar SSL, según el URI que se le proporcione. Si el URI comienza con "https:", se usa SSL; si el URI comienza con "http:", se usa una conexión no cifrada.  
  
 Para usar SSL con el protocolo de transferencia de archivos (FTP), establezca la propiedad <xref:System.Net.FtpWebRequest.EnableSsl> en true antes de llamar a <xref:System.Net.FtpWebRequest.GetResponse>. Del mismo modo, para usar SSL con el Protocolo simple de transferencia de correo (SMTP), establezca la propiedad <xref:System.Net.Mail.SmtpClient.EnableSsl> en true antes de enviar el correo electrónico.  
  
 La clase <xref:System.Net.Security.SslStream> proporciona una abstracción basada en flujos para SSL y ofrece varias maneras de configurar el protocolo de enlace SSL.  
  
## <a name="example"></a>Ejemplo  
  
### <a name="code"></a>Código  
  
```vb  
Dim MyURI As String = "https://www.contoso.com/"  
Dim Wreq As WebRequest = WebRequest.Create(MyURI)  
  
Dim serverUri As String = "ftp://ftp.contoso.com/file.txt"  
Dim request As FtpWebRequest = CType(WebRequest.Create(serverUri), FtpWebRequest)  
request.Method = WebRequestMethods.Ftp.DeleteFile  
request.EnableSsl = True  
Dim response As FtpWebResponse = CType(request.GetResponse(), FtpWebResponse)  
```  
  
```csharp  
String MyURI = "https://www.contoso.com/";  
WebRequest WReq = WebRequest.Create(MyURI);  
  
String serverUri = "ftp://ftp.contoso.com/file.txt"  
FtpWebRequest request = (FtpWebRequest)WebRequest.Create(serverUri);  
request.EnableSsl = true;  
request.Method = WebRequestMethods.Ftp.DeleteFile;  
FtpWebResponse response = (FtpWebResponse)request.GetResponse();  
```  
  
## <a name="compiling-the-code"></a>Compilar el código  
 Para este ejemplo se necesita:  
  
-   Referencias al espacio de nombres **System.Net**.  
  
## <a name="see-also"></a>Vea también

- [Seguridad en la programación para redes](../../../docs/framework/network-programming/security-in-network-programming.md)
- [Programación para redes en .NET Framework](../../../docs/framework/network-programming/index.md)
- [Selección y validación de certificados](../../../docs/framework/network-programming/certificate-selection-and-validation.md)
