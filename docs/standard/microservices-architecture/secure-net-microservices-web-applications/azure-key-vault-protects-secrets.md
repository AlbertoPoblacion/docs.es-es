---
title: Usar Azure Key Vault para proteger secretos en tiempo de producción
description: 'Seguridad en microservicios de .NET y aplicaciones web: Azure Key Vault es una forma excelente de gestionar secretos de aplicación controlados en su totalidad por administradores. Los administradores incluso pueden asignar y revocar valores de desarrollo sin necesidad de que los desarrolladores tengan que gestionarlos.'
author: mjrousos
ms.author: wiwagn
ms.date: 10/19/2018
ms.openlocfilehash: 99049dca3d127f82ba5312c94d5246940bb71ba8
ms.sourcegitcommit: 7156c0b9e4ce4ce5ecf48ce3d925403b638b680c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/26/2019
ms.locfileid: "58466132"
---
# <a name="use-azure-key-vault-to-protect-secrets-at-production-time"></a>Usar Azure Key Vault para proteger secretos en tiempo de producción

Los secretos almacenados como variables de entorno o almacenados por la herramienta Administrador de secretos todavía se almacenan localmente y se descifran en el equipo. Una opción más segura para almacenar secretos es [Azure Key Vault](https://azure.microsoft.com/services/key-vault/), que proporciona una ubicación central y segura para almacenar claves y secretos.

El paquete **Microsoft.Extensions.Configuration.AzureKeyVault** permite que una aplicación de ASP.NET Core lea información de configuración de Azure Key Vault. Siga estos pasos para empezar a usar secretos de Azure Key Vault:

1. Registre la aplicación como una aplicación de Azure AD. (el acceso a los almacenes de claves se administra mediante Azure AD). Puede hacerlo a través del portal de administración de Azure.\

   Como alternativa, si quiere que la aplicación se autentique mediante un certificado en lugar de hacerlo con una contraseña o un secreto de cliente, puede usar el cmdlet de PowerShell [New-AzureRmADApplication](/powershell/module/azurerm.resources/new-azurermadapplication). El certificado que registre en Azure Key Vault solo necesita su clave pública (la aplicación usará la clave privada).

2. Conceda a la aplicación registrada acceso al almacén de claves creando una entidad de servicio. Puede hacerlo usando los siguientes comandos de PowerShell:

   ```powershell
   $sp = New-AzureRmADServicePrincipal -ApplicationId "<Application ID guid>"
   Set-AzureRmKeyVaultAccessPolicy -VaultName "<VaultName>" -ServicePrincipalName $sp.ServicePrincipalNames[0] -PermissionsToSecrets all -ResourceGroupName "<KeyVault Resource Group>"
   ```

3. Incluya el almacén de claves como origen de configuración en la aplicación llamando al método de extensión <xref:Microsoft.Extensions.Configuration.AzureKeyVaultConfigurationExtensions.AddAzureKeyVault%2A?displayProperty=nameWithType> cuando cree una instancia de <xref:Microsoft.Extensions.Configuration.IConfigurationRoot>. Tenga en cuenta que, al llamar a `AddAzureKeyVault` necesitará el Id. de la aplicación registrada y a la que se concedió acceso al almacén de claves en los pasos anteriores.

   También puede usar una sobrecarga de `AddAzureKeyVault` que toma un certificado en lugar del secreto de cliente solo incluyendo una referencia al paquete [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory).

> [!IMPORTANT]
> Le recomendamos que registre Azure Key Vault como el último proveedor de configuración para que pueda invalidar los valores de configuración de proveedores anteriores.

## <a name="additional-resources"></a>Recursos adicionales

- **Using Azure Key Vault to protect application secrets (Usar Azure Key Vault para proteger secretos de aplicaciones)** \
  [https://docs.microsoft.com/azure/guidance/guidance-multitenant-identity-keyvault](/azure/guidance/guidance-multitenant-identity-keyvault)

- **Safe storage of app secrets during development (Almacenamiento seguro de secretos de aplicación durante el desarrollo)** \
  [https://docs.microsoft.com/aspnet/core/security/app-secrets](/aspnet/core/security/app-secrets)

- **Configuring data protection (Configuración de la protección de datos)** \
  [https://docs.microsoft.com/aspnet/core/security/data-protection/configuration/overview](/aspnet/core/security/data-protection/configuration/overview)

- **Administración y duración de las claves de protección de datos en ASP.NET Core** \
  [https://docs.microsoft.com/aspnet/core/security/data-protection/configuration/default-settings](/aspnet/core/security/data-protection/configuration/default-settings)

- Repositorio de GitHub **Microsoft.Extensions.Configuration.KeyPerFile**. \
  [https://github.com/aspnet/Configuration/tree/master/src/Config.KeyPerFile](https://github.com/aspnet/Configuration/tree/master/src/Config.KeyPerFile)

>[!div class="step-by-step"]
>[Anterior](developer-app-secrets-storage.md)
>[Siguiente](../key-takeaways.md)
