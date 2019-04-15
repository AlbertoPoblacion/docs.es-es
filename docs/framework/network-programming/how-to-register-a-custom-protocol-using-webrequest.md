---
title: Procedimiento para registrar un protocolo personalizado mediante WebRequest
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 98ddbdb9-66b1-4080-92ad-51f5c447fcf8
ms.openlocfilehash: 5c9a81fc61a2272056ba34fa387fdafee6203824
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59079505"
---
# <a name="how-to-register-a-custom-protocol-using-webrequest"></a>Procedimiento para registrar un protocolo personalizado mediante WebRequest
En este ejemplo se muestra cómo registrar una clase específica del protocolo que se define en otro lugar. En este ejemplo, `CustomWebRequestCreator` es el objeto implementado por el usuario que implementa el método **Create** que devuelve el objeto `CustomWebRequest`. El ejemplo del código presupone que ha escrito el código `CustomWebRequest` que implementa el protocolo personalizado.  
  
## <a name="example"></a>Ejemplo  
  
```csharp  
WebRequest.RegisterPrefix("custom", new CustomWebRequestCreator());  
WebRequest req = WebRequest.Create("custom://customHost.contoso.com/");  
```  
  
```vb  
WebRequest.RegisterPrefix("custom", New CustomWebRequestCreator())  
Dim req As WebRequest = WebRequest.Create("custom://customHost.contoso.com/")  
```  
  
## <a name="compiling-the-code"></a>Compilar el código  
 Para este ejemplo se necesita:  
  
 Referencias al espacio de nombres <xref:System.Net>.  
  
## <a name="see-also"></a>Vea también

- [programar protocolos acoplables](../../../docs/framework/network-programming/programming-pluggable-protocols.md)
