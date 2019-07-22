---
ms.openlocfilehash: 9678c077e278a9d76ffd5c2ce10e63ebe3ad09f7
ms.sourcegitcommit: 4d8efe00f2e5ab42e598aff298d13b8c052d9593
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68235516"
---
### <a name="x509certificateclaimsetfindclaims-considers-all-claimtypes"></a>X509CertificateClaimSet.FindClaims considera todos los argumentos claimType

|   |   |
|---|---|
|Detalles|En las aplicaciones destinadas a .NET Framework 4.6.1, si un conjunto de notificaciones X509 se inicializó desde un certificado con varias entradas DNS en su campo SAN, el método <xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims(System.String,System.String)?displayProperty=name> trata de hacer coincidir el argumento claimType con todas las entradas DNS. En las aplicaciones destinadas a versiones anteriores de .NET Framework, el método <xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims(System.String,System.String)?displayProperty=name> solo trata de hacer coincidir el argumento claimType con la última entrada DNS.|
|Sugerencia|Este cambio solo afecta a las aplicaciones que tengan como destino .NET Framework 4.6.1. Este cambio puede deshabilitarse (o habilitarse si se establece como destino una versión anterior a la 4.6.1) con el modificador de compatibilidad [DisableMultipleDNSEntries](~/docs/framework/migration-guide/mitigation-x509certificateclaimset-findclaims-method.md#mitigation).|
|Ámbito|Secundaria|
|Versión|4.6.1|
|Tipo|Redestinación|
|API afectadas|<ul><li><xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims(System.String,System.String)?displayProperty=nameWithType></li></ul>|
