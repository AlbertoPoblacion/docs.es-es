---
title: Elemento <clear> para <configSections>
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/configSections/clear
helpviewer_keywords:
- clear Element
- <clear> Element
ms.assetid: 77f1d761-ff45-4001-8f36-3a3e5c41fa63
author: mairaw
ms.author: mairaw
ms.openlocfilehash: a45572d0dcb2737558e11f5c38ac2ccc338c754a
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2019
ms.locfileid: "73119083"
---
# <a name="clear-element-for-configsections"></a>\<borrar > elemento para \<configSections >

Borra todas las secciones y grupos de sección definidos previamente.

[ **\<configuration>** ](configuration-element.md)   
&nbsp;&nbsp;[ **\<configSections >** ](configsections-element-for-configuration.md)   
&nbsp;&nbsp;&nbsp;&nbsp; **\<clear >**

## <a name="syntax"></a>Sintaxis

```xml
<clear/>
```

## <a name="attribute"></a>Atributo

|           | Descripción |
| --------- | ----------- |
| **name**  | Atributo necesario.<br><br>Especifica el nombre de la sección o grupo de secciones que se va a quitar. |

## <a name="parent-element"></a>Elemento primario

|     | Descripción |
| --- | ----------- |
| [ **\<configSections >** Element](configsections-element-for-configuration.md) | Contiene la sección de configuración y las declaraciones de espacio de nombres. |

## <a name="child-elements"></a>Elementos secundarios

Ninguno

## <a name="remarks"></a>Comentarios

El elemento **\<clear >** quita todas las secciones y grupos de secciones de la aplicación que se definieron anteriormente en el archivo de configuración actual o en un nivel superior en la jerarquía del archivo de configuración.

## <a name="example"></a>Ejemplo

En este ejemplo se define un archivo de configuración del equipo y un archivo de configuración de la aplicación y se muestra cómo usar el elemento **\<clear >** en un archivo de configuración de la aplicación para borrar las secciones definidas anteriormente en el archivo de configuración del equipo.

El siguiente código de archivo de configuración de máquina declara dos secciones, **\<sampleSection >** y **\<anotherSampleSection >** , que se leen antes del archivo de configuración de la aplicación:

```xml
<!-- Machine.config file -->
<configuration>
  <configSections>
    <section name="sampleSection"
             type="System.Configuration.SingleTagSectionHandler" />
    <section name="anotherSampleSection"
             type="System.Configuration.NameValueSectionHandler" />
  </configSections>
  <sampleSection setting1="Value1" 
                 setting2="value two" 
                 setting3="third value" />
</configuration>
```

El siguiente código de archivo de configuración de la aplicación borra todas las secciones declaradas previamente. La aplicación no puede usar ni recuperar la configuración de ninguna de las secciones que se han declarado en el archivo de configuración del equipo. Sin embargo, puede usar la configuración de **\<anotherSection >** porque va después del elemento de **> Clear\<** .

```xml
<!-- Application configuration file -->
<configuration>
  <configSections>
    <clear/>
    <section name="anotherSection"
             type="System.Configuration.NameValueSectionHandler" />
  </configSections>
  <anotherSection setting1="Value1" 
                 setting2="value two" 
                 setting3="third value" />
</configuration>
```

## <a name="configuration-file"></a>Archivo de configuración

Este elemento puede usarse en el archivo de configuración de la aplicación, el archivo de configuración del equipo (*Machine. config*) y los archivos *Web. config* que no están en el nivel de directorio de la aplicación.

## <a name="see-also"></a>Vea también

- [Esquema del archivo de configuración para el .NET Framework](index.md)
