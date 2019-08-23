---
title: Elemento <clear> para <configSections>
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/configSections/clear
helpviewer_keywords:
- clear Element
- <clear> Element
ms.assetid: 77f1d761-ff45-4001-8f36-3a3e5c41fa63
author: rpetrusha
ms.author: mairaw
ms.openlocfilehash: c06fca8b83638fb47bedb21863cb9b200cd211f3
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69927732"
---
# <a name="clear-element-for-configsections"></a>\<borrar > elemento para \<configSections >

Borra todas las secciones y grupos de sección definidos previamente.

[ **\<configuration>** ](configuration-element.md)   
&nbsp;&nbsp;[ **\<configSections>** ](configsections-element-for-configuration.md)   
&nbsp;&nbsp;&nbsp;&nbsp; **\<clear>**

## <a name="syntax"></a>Sintaxis

```xml
<clear/>
```

## <a name="attribute"></a>Atributo

|           | DESCRIPCIÓN |
| --------- | ----------- |
| **name**  | Atributo necesario.<br><br>Especifica el nombre de la sección o grupo de secciones que se va a quitar. |

## <a name="parent-element"></a>Elemento primario

|     | DESCRIPCIÓN |
| --- | ----------- |
| [configSections (elemento >)  **\<** ](configsections-element-for-configuration.md) | Contiene la sección de configuración y las declaraciones de espacio de nombres. |

## <a name="child-elements"></a>Elementos secundarios

None

## <a name="remarks"></a>Comentarios

El elemento Clear > quita todas las secciones y grupos de secciones de la aplicación que se definieron anteriormente en el archivo de configuración actual o en un nivel superior en la jerarquía del archivo de configuración.  **\<**

## <a name="example"></a>Ejemplo

En este ejemplo se define un archivo de configuración del equipo y un archivo de configuración de la aplicación y se muestra cómo usar el  **\<elemento Clear >** en un archivo de configuración de la aplicación para borrar las secciones definidas anteriormente en la configuración del equipo. filesystem.

El siguiente código de archivo de configuración de máquina declara dos secciones,  **\<sampleSection >** y  **\<anotherSampleSection >** , que se leen antes del archivo de configuración de la aplicación:

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

El siguiente código de archivo de configuración de la aplicación borra todas las secciones declaradas previamente. La aplicación no puede usar ni recuperar la configuración de ninguna de las secciones que se han declarado en el archivo de configuración del equipo. Sin embargo, puede usar la configuración de  **\<anotherSection >** porque va después del elemento de  **\<>** de borrado.

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
