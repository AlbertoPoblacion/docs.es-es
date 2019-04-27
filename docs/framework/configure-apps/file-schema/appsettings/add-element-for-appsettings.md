---
title: Elemento <add> para <appSettings>
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/appSettings/add
helpviewer_keywords:
- add Element
- <add> Element
ms.assetid: 8734efdc-00f6-4a65-bba6-084c5bc65246
author: guardrex
ms.author: mairaw
ms.openlocfilehash: dde773dc722cf75da9d922ccf28af4bf4a09636c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61674875"
---
# <a name="add-element-for-appsettings"></a>\<Agregar > elemento para \<appSettings >

Agrega una configuración de aplicación personalizada.

[**\<configuration>**](~/docs/framework/configure-apps/file-schema/configuration-element.md)   
&nbsp;&nbsp;[**\<appSettings>**](~/docs/framework/configure-apps/file-schema/appsettings/appsettings-element-for-configuration.md)   
&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**

## <a name="syntax"></a>Sintaxis

```xml
<appSettings>
  <add key="Key of custom setting" value="Value of custom setting" />
</appSettings>
```

## <a name="attributes"></a>Atributos

|           | Descripción |
| --------- | ----------- |
| **key**   | Atributo necesario.<br><br>Especifica el nombre de la clave para agregar. |
| **value** | Atributo necesario.<br><br>Especifica el valor de la clave para agregar. |

## <a name="parent-element"></a>Elemento primario

|     | Descripción |
| --- | ----------- |
| [**\<appSettings>**](~/docs/framework/configure-apps/file-schema/appsettings/appsettings-element-for-configuration.md) | Contiene valores de configuración de aplicación personalizados, como rutas de acceso de archivo, direcciones URL del servicio Web XML o cualquier otra información de configuración personalizada para una aplicación. |

## <a name="child-elements"></a>Elementos secundarios

Ninguna

## <a name="example"></a>Ejemplo

El ejemplo siguiente muestra cómo agregar un valor de configuración personalizado para el nombre de la aplicación:

```xml
<appSettings>
  <add key="ApplicationName" value="MyApplication" />
</appSettings>
```

En el ejemplo siguiente se usa el `<add>` elemento para definir dos configuraciones de compatibilidad de una aplicación ASP.NET:

```xml
<appSettings>
  <add key="AppContext.SetSwitch:Switch.System.Globalization.NoAsyncCurrentCulture" value="true" />
  <add key="AppContext.SetSwitch:Switch.System.Uri.DontEnableStrictRFC3986ReservedCharacterSets" value="true" />
</appSettings>
```

## <a name="see-also"></a>Vea también

- [Esquema de archivo de configuración de .NET Framework](~/docs/framework/configure-apps/file-schema/index.md)
