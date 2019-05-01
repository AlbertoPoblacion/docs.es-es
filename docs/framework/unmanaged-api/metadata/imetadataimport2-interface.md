---
title: IMetaDataImport2 (Interfaz)
ms.date: 03/30/2017
api_name:
- IMetaDataImport2
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport2
helpviewer_keywords:
- IMetaDataImport2 interface [.NET Framework metadata]
ms.assetid: d39b2b87-ba53-4771-ae53-952a68452511
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6717c48fca14f2200f783a984594388ef3b29c15
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62042476"
---
# <a name="imetadataimport2-interface"></a>IMetaDataImport2 (Interfaz)
Extiende la [IMetaDataImport](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md) interfaz para proporcionar la capacidad de trabajar con tipos genéricos.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descripción|  
|------------|-----------------|  
|[EnumGenericParamConstraints (método)](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-enumgenericparamconstraints-method.md)|Obtiene un enumerador para una matriz de restricciones de parámetros genéricos asociados con el parámetro genérico representado por el token especificado.|  
|[EnumGenericParams (método)](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-enumgenericparams-method.md)|Obtiene un enumerador para una matriz de los tokens de parámetro genérico asociado con la definición de tipo especificado o MethodDef (token).|  
|[EnumMethodSpecs (método)](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-enummethodspecs-method.md)|Obtiene un enumerador para una matriz de símbolos (tokens) de MethodSpec asociada al MethodDef o MemberRef especificado (token).|  
|[GetGenericParamConstraintProps (método)](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-getgenericparamconstraintprops-method.md)|Obtiene los metadatos asociados con la restricción de parámetro genérico representada por el token de restricción especificada.|  
|[GetGenericParamProps (método)](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-getgenericparamprops-method.md)|Obtiene los metadatos asociados con el parámetro genérico representado por el token especificado.|  
|[GetMethodSpecProps (método)](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-getmethodspecprops-method.md)|Obtiene la firma de metadatos del método al que hace referencia el MethodSpec especificado (token).|  
|[GetPEKind (método)](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-getpekind-method.md)|Obtiene un valor que identifica la naturaleza del código en un archivo ejecutable portable (PE) de archivo, normalmente un archivo DLL o EXE, definido en el ámbito de metadatos actual|  
|[GetVersionString (método)](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-getversionstring-method.md)|Obtiene el número de versión del runtime que se usó para generar el ensamblado.|  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: Cor.h  
  
 **Biblioteca:** Usar como un recurso en MsCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- <xref:System.Reflection.PortableExecutableKinds>
- [Interfaces de metadatos](../../../../docs/framework/unmanaged-api/metadata/metadata-interfaces.md)
- [IMetaDataImport (interfaz)](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
