---
title: Combinación de protocolos de confianza en escenarios federados
ms.date: 03/30/2017
ms.assetid: d7b5fee9-2246-4b09-b8d7-9e63cb817279
ms.openlocfilehash: 18f486b9de83db48e186bb3856aff6cc6ccb56b1
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2019
ms.locfileid: "64606510"
---
# <a name="mixing-trust-protocols-in-federated-scenarios"></a>Combinación de protocolos de confianza en escenarios federados
Puede haber situaciones en las que los clientes federados se comuniquen con un servicio y un servicio de tokens de seguridad (STS) que no tengan la misma versión de confianza. El WSDL del servicio puede contener una aserción `RequestSecurityTokenTemplate` con elementos WS-Trust que sean de versiones diferentes que las de STS. En tales casos, un cliente de Windows Communication Foundation (WCF) convierte los elementos de WS-Trust recibidos de la `RequestSecurityTokenTemplate` para que coincida con el STS de confianza versión. WCF controla las versiones de confianza no coincidentes solo para los enlaces estándares. Todos los parámetros del algoritmo estándar que son reconocidos por WCF forman parte del enlace estándar. En este tema se describe el comportamiento WCF con distintas configuraciones de confianza entre el servicio y el STS.  
  
## <a name="rp-feb-2005-and-sts-feb-2005"></a>RP Feb 2005 y STS Feb 2005  
 El WSDL de Usuario de confianza (RP) contiene los elementos siguientes en la sección `RequestSecurityTokenTemplate`:  
  
- `CanonicalizationAlgorithm`  
  
- `EncryptionAlgorithm`  
  
- `EncryptWith`  
  
- `SignWith`  
  
- `KeySize`  
  
- `KeyType`  
  
 El archivo de configuración del cliente contiene una lista de parámetros.  
  
 WCF no puede diferenciar entre los parámetros del cliente y el servicio; Agrega todos los parámetros y los envía en el `RequestSecurityTokenTemplate` (RST).  
  
## <a name="rp-trust-13-and-sts-trust-13"></a>RP Trust 1.3 y STS Trust 1.3  
 El WSDL de RP contiene los elementos siguientes en la sección `RequestSecurityTokenTemplate`:  
  
- `CanonicalizationAlgorithm`  
  
- `EncryptionAlgorithm`  
  
- `EncryptWith`  
  
- `SignWith`  
  
- `KeySize`  
  
- `KeyType`  
  
- `KeyWrapAlgorithm`  
  
 El archivo de configuración del cliente tiene un elemento `secondaryParameters` que contiene los parámetros especificados por RP.  
  
 WCF quita el `EncryptionAlgorithm`, `CanonicalizationAlgorithm` y `KeyWrapAlgorithm` elementos desde el elemento de nivel superior bajo RST si éstos están presentes dentro del `SecondaryParameters` elemento. WCF se anexa el `SecondaryParameters` elemento al RST de salida sin modificar.  
  
## <a name="rp-trust-feb-2005-and-sts-trust-13"></a>RP Trust Feb 2005 y STS Trust 1.3  
 El WSDL de RP contiene los elementos siguientes en la sección `RequestSecurityTokenTemplate`:  
  
- `CanonicalizationAlgorithm`  
  
- `EncryptionAlgorithm`  
  
- `EncryptWith`  
  
- `SignWith`  
  
- `KeySize`  
  
- `KeyType`  
  
 El archivo de configuración del cliente contiene una lista de parámetros.  
  
 Desde el archivo de configuración de cliente WCF no puede diferenciar entre los parámetros de servicio y cliente. Por lo tanto, WCF convierte todos los parámetros en un espacio de nombres de la versión 1.3 de confianza.  
  
 WCF controla la `KeyType`, `KeySize`, y `TokenType` elementos como sigue:  
  
- Descargue el WSDL, cree el enlace y asigne `KeyType`, `KeySize` y `TokenType` de los parámetros RP. A continuación se genera el archivo de configuración del cliente.  
  
- Ahora, el cliente puede cambiar cualquier parámetro del archivo de configuración.  
  
- En tiempo de ejecución, WCF copia todos los parámetros especificados en el `AdditionalTokenParameters` sección del archivo de configuración del cliente excepto `KeyType`, `KeySize` y `TokenType`, ya que estos parámetros se tienen en cuenta durante el archivo de configuración generación.  
  
## <a name="rp-trust-13-and-sts-trust-feb-2005"></a>RP Trust 1.3 y STS Trust Feb 2005  
 El WSDL de RP contiene los elementos siguientes en la sección `RequestSecurityTokenTemplate`:  
  
- `CanonicalizationAlgorithm`  
  
- `EncryptionAlgorithm`  
  
- `EncryptWith`  
  
- `SignWith`  
  
- `KeySize`  
  
- `KeyType`  
  
- `KeyWrapAlgorithm`  
  
 El archivo de configuración del cliente tiene un elemento `secondaryParamters` que contiene los parámetros especificados por RP.  
  
 WCF copia todos los parámetros especificados dentro de la `SecondaryParameters` sección para el elemento RST de nivel superior, pero no se convierten en el espacio de nombres de WS-Trust de 2005.
