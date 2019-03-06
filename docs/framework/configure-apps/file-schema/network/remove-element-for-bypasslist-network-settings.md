---
title: <remove> (Elemento para bypasslist, Configuración de red)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy/bypasslist/remove
- http://schemas.microsoft.com/.NetConfiguration/v2.0#remove
helpviewer_keywords:
- <bypasslist>, remove element
- remove element, bypasslist
- bypasslist, remove element
- remove element, bypasslist
ms.assetid: 61dcfb4a-e3d9-4abf-a2cd-7d685fe2f64b
ms.openlocfilehash: a04cca3e57af5cc422776c5b2444a140e86f98b9
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2019
ms.locfileid: "57354263"
---
# <a name="remove-element-for-bypasslist-network-settings"></a>\<Quitar > elemento para bypasslist (configuración de red)

Quita una dirección IP o nombre DNS de la lista de omisión de proxy.

\<configuration>\
\<system.net>\
\<defaultProxy>\
\<bypasslist>\
\<remove>

## <a name="syntax"></a>Sintaxis

```xml
<remove
  address="regular expression"
/>
```

## <a name="attributes-and-elements"></a>Atributos y elementos

En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.

### <a name="attributes"></a>Atributos

|**Attribute**|**Descripción**|
|-------------------|---------------------|
|`address`|Una expresión regular que describe una dirección IP o nombre DNS.|

### <a name="child-elements"></a>Elementos secundarios

Ninguno.

### <a name="parent-elements"></a>Elementos primarios

|**Element**|**Descripción**|
|-----------------|---------------------|
|[bypasslist](../../../../../docs/framework/configure-apps/file-schema/network/bypasslist-element-network-settings.md)|Proporciona un conjunto de expresiones regulares que describen direcciones que no se usa a un proxy.|

## <a name="remarks"></a>Comentarios

El `remove` elemento quita expresiones regulares que describen direcciones IP o nombres de servidor DNS en la lista de direcciones que omitir un servidor proxy. Las direcciones definidas anteriormente en el archivo de configuración o en un nivel superior de la jerarquía de configuración.

El valor de la `address` atributo debe ser una expresión regular que describe un conjunto de direcciones IP o nombres de host.

Para obtener más información sobre las expresiones regulares, vea. [Expresiones regulares de .NET framework](../../../../../docs/standard/base-types/regular-expressions.md).

## <a name="configuration-files"></a>Archivos de configuración

Este elemento se puede usar en el archivo de configuración de la aplicación o en el archivo de configuración del equipo (Machine.config).

## <a name="example"></a>Ejemplo

El ejemplo siguiente quita cualquier definición anterior para el dominio adventure-works.com y, a continuación, agrega el dominio contoso.com a la lista de omisión.

```xml
<configuration>
  <system.net>
    <defaultProxy>
      <bypasslist>
        <remove address="[a-z]+\.adventure-works\.com$" />
        <add address="[a-z]+\.contoso\.com$" />
      </bypasslist>
    </defaultProxy>
  </system.net>
</configuration>
```

## <a name="see-also"></a>Vea también

- <xref:System.Net.WebProxy?displayProperty=nameWithType>
- [Esquema de la configuración de red](../../../../../docs/framework/configure-apps/file-schema/network/index.md)
