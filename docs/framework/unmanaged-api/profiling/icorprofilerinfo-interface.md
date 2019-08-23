---
title: ICorProfilerInfo (Interfaz)
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo
helpviewer_keywords:
- ICorProfilerInfo interface [.NET Framework profiling]
ms.assetid: eb4e4ce0-06e7-4469-bbc4-edc2eb5da4b1
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 3b82d9ac610cb393696ef94fb797a48b737b0231
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69965744"
---
# <a name="icorprofilerinfo-interface"></a>ICorProfilerInfo (Interfaz)
Proporciona métodos para que los profileres de código puedan usar para comunicarse con el Common Language Runtime (CLR) para controlar la supervisión de eventos y la información de las solicitudes.  
  
> [!NOTE]
> Cada método de la `ICorProfilerInfo` interfaz devuelve un valor HRESULT que indica si se ha realizado correctamente o no. Vea CorError. h para obtener una lista de posibles códigos de retorno.  
  
## <a name="methods"></a>Métodos  
  
|Método|DESCRIPCIÓN|  
|------------|-----------------|  
|[BeginInprocDebugging (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-begininprocdebugging-method.md)|Inicializa la compatibilidad con la depuración en proceso. Este método está obsoleto en la .NET Framework versión 2,0.|  
|[EndInprocDebugging (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-endinprocdebugging-method.md)|Cierra una sesión de depuración en proceso. Este método está obsoleto en la .NET Framework versión 2,0.|  
|[ForceGC (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-forcegc-method.md)|Fuerza la recolección de elementos no utilizados en el tiempo de ejecución.|  
|[GetAppDomainInfo (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getappdomaininfo-method.md)|Obtiene información sobre el dominio de aplicación especificado.|  
|[GetAssemblyInfo (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getassemblyinfo-method.md)|Obtiene información acerca del ensamblado especificado.|  
|[GetClassFromObject (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getclassfromobject-method.md)|Obtiene el `ClassID` de un<br /><br /> objeto, dado su `ObjectID`.|  
|[GetClassFromToken (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getclassfromtoken-method.md)|Obtiene el identificador de la clase, dado el token de metadatos. Este método está obsoleto en la .NET Framework versión 2,0. Use en su lugar el método [ICorProfilerInfo2:: GetClassFromTokenAndTypeArgs (](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getclassfromtokenandtypeargs-method.md) .|  
|[GetClassIDInfo (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getclassidinfo-method.md)|Obtiene el módulo primario y el token de metadatos para la clase especificada.|  
|[GetCodeInfo (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getcodeinfo-method.md)|Obtiene la extensión del código nativo asociado al identificador de función especificado. Este método está obsoleto. Use en su lugar el método [ICorProfilerInfo2:: GetCodeInfo2 (](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getcodeinfo2-method.md) .|  
|[GetCurrentThreadID (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getcurrentthreadid-method.md)|Obtiene el identificador del subproceso actual, si es un subproceso administrado.|  
|[GetEventMask (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-geteventmask-method.md)|Obtiene las categorías de eventos actuales para las que el generador de perfiles desea recibir notificaciones de eventos de CLR.|  
|[GetFunctionFromIP (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getfunctionfromip-method.md)|Asigna un puntero de instrucción de código administrado `FunctionID`a un.|  
|[GetFunctionFromToken (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getfunctionfromtoken-method.md)|Obtiene el identificador de una función. Este método está obsoleto en la .NET Framework versión 2,0. Use en su lugar el método [ICorProfilerInfo2:: GetFunctionFromTokenAndTypeArgs (](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getfunctionfromtokenandtypeargs-method.md) .|  
|[GetFunctionInfo (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getfunctioninfo-method.md)|Obtiene la clase primaria y el token de metadatos para la función especificada.|  
|[GetHandleFromThread (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-gethandlefromthread-method.md)|Asigna el identificador de un subproceso a un identificador de subproceso de Win32.|  
|[GetILFunctionBody (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getilfunctionbody-method.md)|Obtiene un puntero al cuerpo de un método en el código del lenguaje intermedio de Microsoft (MSIL), comenzando en su encabezado.|  
|[GetILFunctionBodyAllocator (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getilfunctionbodyallocator-method.md)|Obtiene una interfaz que proporciona un método para asignar la memoria que se va a usar para intercambiar el cuerpo de un método en código MSIL.|  
|[GetILToNativeMapping (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getiltonativemapping-method.md)|Obtiene una asignación de desplazamientos de MSIL a desplazamientos nativos para el código contenido en la función especificada.|  
|[GetInprocInspectionInterface (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getinprocinspectioninterface-method.md)|Obtiene un objeto que se puede consultar para una interfaz ICorDebugProcess. Este método está obsoleto en la .NET Framework versión 2,0.|  
|[GetInprocInspectionIThisThread (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getinprocinspectionithisthread-method.md)|Obtiene un objeto que se puede consultar para la interfaz ICorDebugThread. Este método está obsoleto en la .NET Framework versión 2,0.|  
|[GetModuleInfo (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getmoduleinfo-method.md)|A partir de un identificador de módulo, devuelve el nombre de archivo del módulo y el identificador del ensamblado primario del módulo.|  
|[GetModuleMetaData (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getmodulemetadata-method.md)|Obtiene una instancia de la interfaz de metadatos que se asigna al módulo especificado.|  
|[GetObjectSize (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getobjectsize-method.md)|Obtiene el tamaño de un objeto especificado.|  
|[GetThreadContext (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getthreadcontext-method.md)|Obtiene la identidad de contexto asociada actualmente al subproceso especificado.|  
|[GetThreadInfo (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getthreadinfo-method.md)|Obtiene la identidad del subproceso de Win32 actual para el subproceso especificado.|  
|[GetTokenAndMetadataFromFunction (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-gettokenandmetadatafromfunction-method.md)|Obtiene el token de metadatos y una instancia de la interfaz de metadatos que se puede usar con el token para la función especificada.|  
|[IsArrayClass (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-isarrayclass-method.md)|Determina si la clase especificada es una clase de matriz.|  
|[SetEnterLeaveFunctionHooks (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setenterleavefunctionhooks-method.md)|Especifica las funciones implementadas por el generador de perfiles a las que se llamará en los enlaces "Enter", "Leave" y "llamada" de las funciones administradas.|  
|[SetEventMask (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-seteventmask-method.md)|Establece un valor que especifica los tipos de eventos para los que el generador de perfiles desea recibir notificaciones de CLR.|  
|[SetFunctionIDMapper (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setfunctionidmapper-method.md)|Especifica la función implementada por el generador de perfiles a la que se llamará para asignar los valores `FunctionID` a valores alternativos, que se pasan los enlaces de entrada y salida de función del generador de perfiles.|  
|[SetFunctionReJIT (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setfunctionrejit-method.md)|Sin implementar. No usar.|  
|[SetILFunctionBody (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setilfunctionbody-method.md)|Reemplaza el cuerpo de la función especificada en el módulo especificado.|  
|[SetILInstrumentedCodeMap (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setilinstrumentedcodemap-method.md)|Especifica cómo se asignan los desplazamientos del MSIL original de una función especificada a los nuevos desplazamientos del MSIL modificado por el generador de perfiles de la función.|  
  
## <a name="remarks"></a>Comentarios  
 Un generador de perfiles llama a un `ICorProfilerInfo` método de la interfaz para comunicarse con CLR para controlar la supervisión de eventos y solicitar información.  
  
 El CLR implementa los `ICorProfilerInfo` métodos de la interfaz mediante el modelo de subprocesamiento libre. Cada método devuelve un valor HRESULT para indicar un resultado correcto o erróneo. Vea CorError. h para obtener una lista de posibles códigos de retorno.  
  
 El CLR pasa, a través de la implementación del generador de perfiles de [ICorProfilerCallback:: Initialize](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-initialize-method.md), una `ICorProfilerInfo` interfaz para cada generador de perfiles de código durante la inicialización. Un generador de perfiles de código puede llamar a `ICorProfilerInfo` los métodos de la interfaz para obtener información sobre el código administrado que se ejecuta bajo el control de CLR.  
  
## <a name="requirements"></a>Requisitos  
 **Select** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: Corprof. idl, Corprof. h  
  
 **Biblioteca** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [Interfaces para generación de perfiles](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [ICorProfilerInfo2 (interfaz)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md)
