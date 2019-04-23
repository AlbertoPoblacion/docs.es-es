---
title: Elemento <system.codedom>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.codedom
- http://schemas.microsoft.com/.NetConfiguration/v2.0#system.codedom
helpviewer_keywords:
- compiler configuration elements, <system.codedom> element
- system.codedom element
- <system.codedom> element
ms.assetid: 672a68f7-e69f-4479-ac30-e980085ec4fe
ms.openlocfilehash: 0f47255bb4073007a847e4a8b85ccfd34100582b
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59101619"
---
# <a name="systemcodedom-element"></a>\<system.codedom> Element
Especifica los valores de configuración del compilador para los proveedores de lenguaje disponibles.  
  
 \<Configuración > elemento  
\<system.codedom> Element  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<system.codedom>  
  <compilers> ... </compilers>  
</system.codedom>  
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
 Ninguno.  
  
### <a name="child-elements"></a>Elementos secundarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<compilers>](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md)|Contenedor para los elementos de configuración del compilador; contiene cero o más elementos [\<compiler>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md).|  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<configuration>](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)|Elemento raíz de cada archivo de configuración usado por las aplicaciones de Common Language Runtime y .NET Framework.|  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="net-framework-version-20"></a>Versión de .NET framework 2.0  
 El [ \<system.codedom >](../../../../../docs/framework/configure-apps/file-schema/compiler/system-codedom-element.md) elemento contiene la configuración de compilador para los proveedores de lenguaje instalados en un equipo, además de los proveedores predeterminados que se instalan con .NET Framework, como la <xref:Microsoft.CSharp.CSharpCodeProvider> y <xref:Microsoft.VisualBasic.VBCodeProvider>. El [ \<compiladores >](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md) elemento contiene cero o más [ \<compilador >](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md) elementos. Cada [ \<compilador >](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md) elemento especifica los atributos de configuración de compilador para un proveedor de lenguaje específico.  
  
 Los desarrolladores y proveedores de compiladores pueden agregar valores de configuración al archivo de configuración del equipo (Machine.config) para un nuevo <xref:System.CodeDom.Compiler.CodeDomProvider> implementación. Use el <xref:System.CodeDom.Compiler.CodeDomProvider.GetAllCompilerInfo%2A?displayProperty=nameWithType> método para enumerar mediante programación los proveedores de lenguaje predeterminados y los proveedores de lenguaje identificados por los valores de configuración del compilador en un equipo.  
  
> [!NOTE]
>  En las versiones de .NET Framework 1.0 y 1.1, el idioma predeterminado proveedores proporcionados por .NET Framework se identifican en el [ \<compiladores >](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md) elemento. En la versión 2.0 de .NET Framework, los proveedores de lenguaje predeterminado no se identifican en el [ \<compiladores >](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md) elemento, pero se pueden enumerar mediante la <xref:System.CodeDom.Compiler.CodeDomProvider.GetAllCompilerInfo%2A> método.  
  
## <a name="net-framework-versions-10-and-11"></a>Versiones 1.0 y 1.1 de .NET framework  
 El [ \<system.codedom >](../../../../../docs/framework/configure-apps/file-schema/compiler/system-codedom-element.md) elemento contiene los valores de configuración de compilador para los proveedores de lenguaje en un equipo. El [ \<compiladores >](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md) elemento contiene cero o más [ \<compilador >](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md) elementos. Cada [ \<compilador >](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md) elemento especifica los atributos de configuración de compilador para un proveedor de lenguaje específico.  
  
 .NET Framework define la configuración inicial del compilador en el archivo de configuración del equipo (Machine.config). Los desarrolladores y los proveedores de compiladores pueden agregar valores de configuración para una nueva implementación de <xref:System.CodeDom.Compiler.CodeDomProvider>. Use el método <xref:System.CodeDom.Compiler.CodeDomProvider.GetAllCompilerInfo%2A?displayProperty=nameWithType> para enumerar mediante programación los valores de configuración del compilador y del proveedor de lenguaje en un equipo.  
  
## <a name="configuration-file"></a>Archivo de configuración  
 Este elemento se puede usar en el archivo de configuración del equipo y el archivo de configuración de la aplicación.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente ilustra una configuración de compilador típico.  
  
```xml  
<configuration>  
  <system.codedom>  
    <compilers>  
      <!-- zero or more compiler elements -->  
      <compiler   
        language="c#;cs;csharp"  
        extension=".cs"  
        type="Microsoft.CSharp.CSharpCodeProvider, System,   
          Version=1.0.5000.0, Culture=neutral,   
          PublicKeyToken=b77a5c561934e089"  
        compilerOptions=""  
        warningLevel="1" />  
    </compilers>  
  </system.codedom>  
</configuration>  
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.CodeDom.Compiler.CompilerInfo>
- <xref:System.CodeDom.Compiler.CodeDomProvider>
- [Esquema de los archivos de configuración](../../../../../docs/framework/configure-apps/file-schema/index.md)
- [Esquema de configuración de compilador y proveedor de lenguaje](../../../../../docs/framework/configure-apps/file-schema/compiler/index.md)
- [Elemento \<compiler>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md)
