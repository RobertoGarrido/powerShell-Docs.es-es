---
ms.date: 2017-06-12T00:00:00.000Z
contributor: manikb
ms.topic: reference
keywords: gallery,powershell,cmdlet,psget
title: Arrancar el proveedor de NuGet y NuGet.exe
ms.openlocfilehash: 0036972eb9a0c20469da1aadafe223e6ec80f16a
ms.sourcegitcommit: a5c0795ca6ec9332967bff9c151a8572feb1a53a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/27/2017
---
# <a name="bootstrap-both-nuget-provider-and-nugetexe-or-bootstrap-only-nuget-provider"></a>Arranque del proveedor de NuGet y NuGet.exe o arranque solo del proveedor de NuGet

El proveedor de NuGet más reciente no incluye NuGet.exe.
Para operaciones de publicación de un módulo o script, PowerShellGet requiere el archivo ejecutable binario NuGet.exe.
Solo se requiere el proveedor de NuGet para todas las demás operaciones, como *buscar*, *instalar*, *guardar* y *desinstalar*.
PowerShell incluye una lógica para controlar un arranque combinado del proveedor de NuGet y NuGet.exe o el arranque únicamente del proveedor de NuGet.
Cualquiera sea el caso, solo debe haber un mensaje de solicitud.
Si la máquina no está conectada a Internet, el usuario o un administrador debe copiar una instancia de confianza del proveedor de NuGet o del archivo NuGet.exe en la máquina desconectada.

>**Nota**: A partir de la versión 6, el proveedor de NuGet se incluye en la instalación de PowerShell. [http://github.com/powershell/powershell](http://github.com/powershell/powershell)

## <a name="resolving-error-when-the-nuget-provider-has-not-been-installed-on-a-machine-that-is-internet-connected"></a>Resolución de errores cuando el proveedor de NuGet no está instalado en una máquina conectada a Internet

```powershell
PS C:\> Find-Module -Repository PSGallery -Verbose -Name Contoso

NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet provider must be available in 'C:\Program Files\PackageManagement\ProviderAssemblies' or
'C:\Users\manikb\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running 'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and import the NuGet provider
now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): n
Find-Module : NuGet provider is required to interact with NuGet-based repositories. Please ensure that '2.8.5.201' or newer version of NuGet provider is installed.
At line:1 char:1
+ Find-Module -Repository PSGallery -Verbose -Name Contoso
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Find-Module], InvalidOperationException
   + FullyQualifiedErrorId : CouldNotInstallNuGetProvider,Find-Module

PS C:\> Find-Module -Repository PSGallery -Verbose -Name Contoso

NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet provider must be available in 'C:\Program Files\PackageManagement\ProviderAssemblies' or
'C:\Users\manikb\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running 'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and import the NuGet provider
now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
VERBOSE: Installing NuGet provider.

Version    Name                                Type       Repository           Description
-------    ----                                ----       ----------           -----------
2.5        Contoso                             Module     PSGallery        Contoso module
```
## <a name="resolving-error-when-the-nuget-provider-is-available-and-nugetexe-is-not-available-during-the-publish-operation-on-a-machine-that-is-internet-connected"></a>Resolución de errores cuando el proveedor de NuGet está disponible y NuGet.exe no lo está durante la operación de publicación en una máquina conectada a Internet

```powershell
PS C:\> Publish-Module -Name Contoso -Repository PSGallery -Verbose

NuGet.exe is required to continue
PowerShellGet requires NuGet.exe to publish an item to the NuGet-based repositories. NuGet.exe must be available under one of the paths specified in PATH environment variable value. Do you want PowerShellGet to install NuGet.exe now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): N
Publish-Module : NuGet.exe is required to interact with NuGet-based repositories. Please ensure that NuGet.exe is available under one of the paths specified in PATH environment variable value.
At line:1 char:1
+ Publish-Module -Name Contoso -Repository PSGallery -Verbose
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Publish-Module], InvalidOperationException
    + FullyQualifiedErrorId : CouldNotInstallNuGetExe,Publish-Module

PS C:\> Publish-Module -Name Contoso -Repository PSGallery -Verbose

NuGet.exe is required to continue
PowerShellGet requires NuGet.exe to publish an item to the NuGet-based repositories. NuGet.exe must be available under one of the paths specified in PATH environment variable value. Do you want PowerShellGet to install NuGet.exe now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
VERBOSE: Installing NuGet.exe.
VERBOSE: Successfully published module 'Contoso' to the module publish location 'https://www.powershellgallery.com/api/v2/'. Please allow few minutes for 'Contoso' to show up in the search results.
```

## <a name="resolving-error-when-both-nuget-provider-and-nugetexe-are-not-available-during-the-publish-operation-on-a-machine-that-is-internet-connected"></a>Resolución de errores cuando ni el proveedor de NuGet ni NuGet.exe están disponibles durante la operación de publicación en una máquina conectada a Internet

```powershell
PS C:\> Publish-Module -Name Contoso -Repository PSGallery -Verbose

NuGet.exe and NuGet provider are required to continue
PowerShellGet requires NuGet.exe and NuGet provider version '2.8.5.201' or newer to interact with the NuGet-based repositories. Do you want PowerShellGet to install both NuGet.exe and NuGet provider now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): N
Publish-Module : PowerShellGet requires NuGet.exe and NuGet provider version '2.8.5.201' or newer to interact with the NuGet-based repositories. Please ensure that '2.8.5.201' or newer version of NuGet provider is installed and NuGet.exe is available under 
one of the paths specified in PATH environment variable value.
At line:1 char:1
+ Publish-Module -Name Contoso -Repository PSGallery -Verbose
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Publish-Module], InvalidOperationException
    + FullyQualifiedErrorId : CouldNotInstallNuGetBinaries,Publish-Module

PS C:\> Publish-Module -Name Contoso -Repository PSGallery -Verbose

NuGet.exe and NuGet provider are required to continue
PowerShellGet requires NuGet.exe and NuGet provider version '2.8.5.201' or newer to interact with the NuGet-based repositories. Do you want PowerShellGet to install both NuGet.exe and NuGet provider now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
VERBOSE: Installing NuGet provider.
VERBOSE: Installing NuGet.exe.
VERBOSE: Successfully published module 'Contoso' to the module publish location 'https://www.powershellgallery.com/api/v2/'. Please allow few minutes for 'Contoso' to show up in the search results.
```

## <a name="manually-bootstrapping-the-nuget-provider-on-a-machine-that-is-not-connected-to-the-internet"></a>Arranque manual del proveedor de NuGet en una máquina no conectada a Internet

En los procesos mostrados anteriormente se presume que la máquina está conectada a Internet y que se pueden descargar archivos desde una ubicación pública.
Si no es posible, la única opción es arrancar una máquina con los procesos mencionados y copiar manualmente el proveedor en el nodo aislado a través de un proceso de confianza sin conexión.
El caso de uso más común de este escenario se da cuando una galería privada está disponible para admitir un entorno aislado.

Después de seguir el proceso anterior para arrancar una máquina conectada a Internet, encontrará los archivos de proveedor en esta ubicación:
```
C:\Program Files\PackageManagement\ProviderAssemblies\
```

La estructura de carpetas/archivos del proveedor de NuGet será la siguiente (posiblemente con un número de versión distinto):

NuGet<br>
--2.8.5.208<br>
----Microsoft.PackageManagement.NuGetProvider.dll

Copie estas carpetas y archivos con un proceso de confianza en las máquinas sin conexión.

## <a name="manually-bootstrapping-nugetexe-to-support-publish-operations-on-a-machine-that-is-not-connected-to-the-internet"></a>Arranque manual de NuGet.exe para admitir operaciones de publicación en una máquina no conectada a Internet

Además del proceso para arrancar manualmente el proveedor de NuGet, si la máquina se usará para publicar módulos o scripts en una galería privada con los cmdlets *Publish-Module* o *Publish-Script*, se requerirá el archivo ejecutable binario NuGet.exe.
El caso de uso más común de este escenario se da cuando una galería privada está disponible para admitir un entorno aislado.
Hay dos opciones para obtener el archivo NuGet.exe.

Una opción es arrancar una máquina conectada a Internet y copiar los archivos en las máquinas sin conexión mediante un proceso de confianza.
Después de arrancar la máquina conectada a Internet, el archivo binario NuGet.exe se ubicará en una de estas dos carpetas:

Si los cmdlets *Publish-Module* o *Publish-Script* se ejecutaron con permisos elevados (como administrador):
```
$env:ProgramData\Microsoft\Windows\PowerShell\PowerShellGet
```

Si los cmdlets se ejecutaron como usuario sin permisos elevados:
```
$env:userprofile\AppData\Local\Microsoft\Windows\PowerShell\PowerShellGet\
```

Otra opción es descargar NuGet.exe desde el sitio web de NuGet.org: [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)<br>
Cuando se selecciona una versión de NuGet para máquinas de producción, asegúrese de que sea una versión posterior a 2.8.5.208 e identifique la versión etiquetada como "recomendada".
Recuerde desbloquear el archivo si se descargó con un explorador.
Para ello, use el cmdlet *Unblock-File*.

En cualquier caso, el archivo NuGet.exe se puede copiar a cualquier ubicación en *$env:path*, pero las ubicaciones estándar son las siguientes:

Para hacer que el ejecutable esté disponible para que todos los usuarios puedan usar los cmdlets *Publish-Module* y *Publish-Script*:
```
$env:ProgramData\Microsoft\Windows\PowerShell\PowerShellGet
```

Para hacer que el ejecutable esté disponible solo para un usuario específico, cópielo en la ubicación solo dentro del perfil de ese usuario:
```
$env:userprofile\AppData\Local\Microsoft\Windows\PowerShell\PowerShellGet\
```

