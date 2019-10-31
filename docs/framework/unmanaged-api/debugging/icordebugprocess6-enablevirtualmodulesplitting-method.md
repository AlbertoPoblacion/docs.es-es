---
title: Método ICorDebugProcess6::EnableVirtualModuleSplitting
ms.date: 03/30/2017
ms.assetid: e7733bd3-68da-47f9-82ef-477db5f2e32d
ms.openlocfilehash: 32648f40046959ffd8676fe67a1e0a123b0e801f
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2019
ms.locfileid: "73123504"
---
# <a name="icordebugprocess6enablevirtualmodulesplitting-method"></a>Método ICorDebugProcess6::EnableVirtualModuleSplitting
Habilita o deshabilita la división de módulos virtuales.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT EnableVirtualModuleSplitting(  
   BOOL enableSplitting  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `enableSplitting`  
 `true` para habilitar la división de módulos virtuales; `false` para deshabilitarla.  
  
## <a name="remarks"></a>Comentarios  
 La división de módulos virtuales hace que [ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md) reconozca los módulos que se combinaron durante el proceso de compilación y los presenta como un grupo de módulos independientes en lugar de un único módulo grande. Esto cambia el comportamiento de los diversos métodos [ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md) descritos a continuación.  
  
> [!NOTE]
> Este método solo está disponible con .NET Native.  
  
 Puede llamar a este método y cambiar el valor de `enableSplitting` en cualquier momento. No provoca ningún cambio funcional con estado en un objeto [ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md) , a excepción de la modificación del comportamiento de los métodos enumerados en las secciones [División de módulos virtuales y API de depuración no administradas](#APIs) en el momento en que se llaman. El uso de módulos virtuales hace que el rendimiento disminuya cuando se llama a estos métodos. Además, es posible que se necesite un almacenamiento en caché considerable de los metadatos virtualizados para implementar correctamente las API de [IMetaDataImport](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md) , y estas cachés se pueden conservar incluso después de que se haya desactivado la división de módulos virtuales.  
  
## <a name="terminology"></a>Terminología  
 Los siguientes términos sirven para describir la división de módulos virtuales:  
  
 módulos de contenedor o contenedores  
 Son los módulos agregados.  
  
 submódulos o módulos virtuales  
 Son los módulos incluidos en un contenedor.  
  
 módulos regulares  
 Módulos que no se han combinado en tiempo de compilación. No son ni módulos de contenedor ni submódulos.  
  
 Los módulos de contenedor y los submódulos se representan mediante objetos de interfaz ICorDebugModule. Sin embargo, el comportamiento de la interfaz es ligeramente diferente en cada caso, como se describe en la sección \<x-Ref a la sección >.  
  
## <a name="modules-and-assemblies"></a>Módulos y ensamblados  
 En los escenarios donde se combinan ensamblados no se admiten ensamblados con varios módulos, por lo que hay una relación de uno a uno entre un módulo y un ensamblado. Cada objeto ICorDebugModule, independientemente de si representa un módulo contenedor o un submódulo, tiene un objeto ICorDebugAssembly correspondiente. El método [ICorDebugModule:: getassembly (](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getassembly-method.md) convierte el módulo en el ensamblado. Para asignar en la otra dirección, el método [ICorDebugAssembly:: enumeratemodules (](../../../../docs/framework/unmanaged-api/debugging/icordebugassembly-enumeratemodules-method.md) solo enumera 1 módulo. Dado que ensamblado y módulo conforman un par estrechamente unido en este caso, los términos módulo y ensamblado se han convertido en prácticamente intercambiables.  
  
## <a name="behavioral-differences"></a>Diferencias de comportamiento  
 Los módulos del contenedor tienen los siguientes comportamientos y características:  
  
- Sus metadatos para todos los submódulos que lo conforman se combinan entre sí.  
  
- Sus nombres de tipo se pueden alterar.  
  
- El método [ICorDebugModule:: GetName](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getname-method.md) devuelve la ruta de acceso a un módulo en disco.  
  
- El método [ICorDebugModule::FUL](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getsize-method.md) devuelve el tamaño de la imagen.  
  
- El método ICorDebugAssembly3.EnumerateContainedAssemblies enumera los submódulos.  
  
- El método ICorDebugAssembly3.GetContainerAssembly devuelve `S_FALSE`.  
  
 Los submódulos tienen los siguientes comportamientos y características:  
  
- Tienen un conjunto reducido de metadatos que corresponde únicamente al ensamblado original que se ha combinado.  
  
- Los nombres de los metadatos no se alteran.  
  
- Es improbable que los tokens de los metadatos coincidan con los tokens del ensamblado original antes de que combinarse en el proceso de compilación.  
  
- El método [ICorDebugModule:: GetName](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getname-method.md) devuelve el nombre del ensamblado, no una ruta de acceso del archivo.  
  
- El método [ICorDebugModule::FUL](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getsize-method.md) devuelve el tamaño original de la imagen sin combinar.  
  
- El método ICorDebugModule3.EnumerateContainedAssemblies devuelve `S_FALSE`.  
  
- El método ICorDebugAssembly3.GetContainerAssembly devuelve el módulo contenedor.  
  
## <a name="interfaces-retrieved-from-modules"></a>Interfaces obtenidas de los módulos  
 Se pueden crear y recuperar diversas interfaces de los módulos. Algunas de ellas son:  
  
- Un objeto ICorDebugClass, devuelto por el método [ICorDebugModule:: GetClassFromToken (](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getclassfromtoken-method.md) .  
  
- Un objeto ICorDebugAssembly, devuelto por el método [ICorDebugModule:: getassembly (](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getassembly-method.md) .  
  
 Este tipo de objetos siempre se almacenan en caché por [ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)y tendrán la misma identidad de puntero independientemente de si se crearon o consultaron desde el módulo contenedor o un submódulo. El submódulo proporciona una vista filtrada de estos objetos en caché, no una memoria caché independiente con sus propias copias.  
  
<a name="APIs"></a>   
## <a name="virtual-module-splitting-and-the-unmanaged-debugging-apis"></a>División de módulos virtuales y API de depuración no administradas  
 En la siguiente tabla se muestra cómo la división de módulos virtuales afecta al comportamiento de otros métodos en una API de depuración no administrada.  
  
|Método|`enableSplitting` = `true`|`enableSplitting` = `false`|  
|------------|---------------------------------|----------------------------------|  
|[ICorDebugFunction:: GetModule](../../../../docs/framework/unmanaged-api/debugging/icordebugfunction-getmodule-method.md)|Devuelve el submódulo en el que esta función se definió originalmente.|Devuelve el módulo contenedor con el que esta función se combinó.|  
|[ICorDebugClass:: GetModule](../../../../docs/framework/unmanaged-api/debugging/icordebugclass-getmodule-method.md)|Devuelve el submódulo en el que esta clase se definió originalmente.|Devuelve el módulo contenedor con el que esta clase se combinó.|  
|ICorDebugModuleDebugEvent::GetModule|Devuelve el módulo contenedor que se cargó. Los submódulos no tienen eventos load, independientemente de esta configuración.|Devuelve el módulo contenedor que se cargó.|  
|[ICorDebugAppDomain:: EnumerateAssemblies (](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain-enumerateassemblies-method.md)|Devuelve una lista de los subensamblados y ensamblados regulares; no se incluyen ensamblados de contenedor. **Nota:**  Si faltan símbolos en algún ensamblado de contenedor, no se enumerará ninguno de sus Subensamblados. Si faltan símbolos en algún ensamblado regular, puede que se enumere o no.|Devuelve una lista de ensamblados de contenedor y ensamblados regulares; no se incluyen subensamblados. **Nota:**  Si faltan símbolos en algún ensamblado normal, se puede enumerar o no.|  
|[ICorDebugCode:: getCode](../../../../docs/framework/unmanaged-api/debugging/icordebugcode-getcode-method.md) (solo cuando se hace referencia a código Il)|Devuelve el código IL que sería válido en una imagen de ensamblado antes de la fusión mediante combinación. En concreto, cualquier token de metadatos en línea será correctamente un token TypeRef o MemberRef cuando los tipos a los que se hace referencia no están definidos en el módulo virtual que contiene el IL. Estos tokens TypeRef o MemberRef se pueden buscar en el objeto [IMetaDataImport](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md) del objeto ICorDebugModule virtual correspondiente.|Devuelve el IL de la imagen de ensamblado posterior a la combinación.|  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Vea [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Vea también

- [ICorDebugProcess6 (interfaz)](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess6-interface.md)
- [Interfaces de depuración](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
