---
title: <providerOption> (Elemento)
ms.date: 03/30/2017
f1_keywords:
- provideroption
helpviewer_keywords:
- <provideroption> element
- providerOptions
- provideroption element
ms.assetid: 014f2e0b-c0b5-4fc4-92d3-73f02978b2a1
ms.openlocfilehash: 9c69ea7bf95b311a796ec29d90410a77b748c3c6
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59229789"
---
# <a name="provideroption-element"></a>\<providerOption > elemento
Especifica los atributos de versión del compilador para un proveedor de lenguaje.  
  
 \<Elemento de configuración >  
\<system.codedom Element>  
\<Elemento compilers >  
\<compilador > elemento  
\<providerOption > elemento  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<providerOption  
  name="option-name"  
  value="option-value"  
/>  
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|`name`|Atributo necesario.<br /><br /> Especifica el nombre de la opción; Por ejemplo, "CompilerVersion".|  
|`value`|Atributo necesario.<br /><br /> Especifica el valor de la opción; Por ejemplo, "v3.5".|  
  
### <a name="child-elements"></a>Elementos secundarios  
 Ninguno.  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[Elemento \<configuration>](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)|Elemento raíz necesario en cada archivo de configuración utilizado por Common Language Runtime y las aplicaciones de .NET Framework.|  
|[\<system.codedom> Element](../../../../../docs/framework/configure-apps/file-schema/compiler/system-codedom-element.md)|Especifica los valores de configuración del compilador para los proveedores de lenguaje disponibles.|  
|[\<los compiladores > elemento](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md)|Contenedor para los elementos de configuración de compilador; contiene cero o más `<compiler>` elementos.|  
|[Elemento \<compiler>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md)|Especifica los atributos de configuración del compilador para un proveedor de lenguaje.|  
  
## <a name="remarks"></a>Comentarios  
 En la versión 3.5 de .NET Framework, los proveedores de código de Code Document Object Model (CodeDOM) pueden admitir opciones específicas del proveedor utilizando el `<providerOption>` elemento.  
  
 .NET Framework 3.5 incluye ensamblados de .NET Framework 2.0 actualizados y proporciona nuevos ensamblados de la versión 3.5 que contienen nuevos tipos. Los proveedores de código de Microsoft C# y Visual Basic se encuentran en ensamblados de .NET Framework 2.0, pero se han actualizado para admitir los compiladores de la versión 3.5. De forma predeterminada, los proveedores de código actualizado generan código para los compiladores de la versión 2.0. Puede usar el `<providerOption>` elemento para cambiar la versión del compilador de destino a la versión 3.5. Para ello, especifique "CompilerVersion" para el `name` atributo y "v3.5" para el `value` atributo. Debe preceder el número de versión con una letra minúscula "v".  
  
 Puede hacer que la especificación de versión global añadiendo el `<providerOption>` elemento al archivo raíz Web.config o Machine.config de .NET Framework 2.0. Si actualiza la versión del compilador predeterminada a 3.5 en el archivo Machine.config, puede cambiar a 2.0 por la aplicación mediante el `<providerOption>` elemento en el archivo de configuración de la aplicación.  
  
 Los implementadores de proveedor de código codeDOM pueden procesar opciones personalizadas proporcionando un constructor que toma un `providerOptions` parámetro de tipo <xref:System.Collections.Generic.IDictionary%602>.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra cómo especificar que se debe usar esa versión 3.5 del proveedor de código C#.  
  
```xml  
<configuration>  
  <system.codedom>  
    <compilers>  
      <!-- zero or more compiler elements -->  
      <compiler  
        language="c#;cs;csharp"  
        extension=".cs"  
        type="Microsoft.CSharp.CSharpCodeProvider, System,   
          Version=2.0.3600.0, Culture=neutral,   
          PublicKeyToken=b77a5c561934e089"  
        compilerOptions="/optimize"  
        warningLevel="1" >  
          <providerOption  
            name="CompilerVersion"  
            value="v3.5" />  
      </compiler>  
    </compilers>  
  </system.codedom>  
</configuration>  
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.CodeDom.Compiler.CompilerInfo>
- <xref:System.CodeDom.Compiler.CodeDomProvider>
- [Esquema de los archivos de configuración](../../../../../docs/framework/configure-apps/file-schema/index.md)
- [\<los compiladores > elemento](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md)
- [Especificar nombres de tipo completos](../../../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md)
- [Elemento Compiler aplicado a compilers para compilation (esquema de configuración de ASP.NET)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/a15ebt6c(v=vs.100))
