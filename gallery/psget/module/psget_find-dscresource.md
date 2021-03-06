---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: gallery,powershell,cmdlet,psget
title: Find-DscResource
ms.openlocfilehash: 37ba7925d6f73c453126f25e0818b3f8839d3b3b
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2017
---
# <a name="find-dscresource"></a>Find-DscResource

Encuentra recursos de DSC en módulos.

## <a name="description"></a>Descripción

El cmdlet Find-DscResource busca recursos de [configuración de estado deseado (DSC)](https://msdn.microsoft.com/en-us/PowerShell/dsc/overview) contenidos en módulos que coincidan con los criterios especificados desde repositorios registrados.
Para cada módulo detectado por este cmdlet, Find-DscResource devuelve un objeto PSGetDscResourceInfo que se puede canalizar a Install-Module para instalar los módulos que contienen los recursos que este cmdlet devuelve.

DSC es una nueva plataforma de administración de Windows PowerShell que permite implementar y administrar datos de configuración de servicios de software y administrar el entorno en el que se ejecutan estos servicios.

Los recursos de la configuración de estado deseado (DSC) ofrecen los bloques de creación para una configuración DSC. Un recurso expone las propiedades que se pueden configurar (el esquema) y contiene las funciones de script de PowerShell a las que el administrador de configuración local (LCM) llama para "que sea así".

Un recurso puede modelar algo tan genérico como un archivo o tan específico como una configuración de servidor IIS. Grupos de recursos similares se combinan en un módulo de DSC, que organiza todos los archivos necesarios en una estructura portátil que incluye los metadatos para identificar cómo están diseñados para usarse los recursos.

- Find-DscResource puede filtrar con parámetros de versión: MinimumVersion, RequiredVersion y AllVersions.
  - Estos parámetros se excluyen mutuamente.
  - Estos parámetros de versión solo se permiten con el nombre de módulo único sin ningún carácter comodín.
  - Si no se especifica el parámetro RequiredVersion, Find-DscResource devuelve la versión más reciente del módulo que sea igual o mayor que la versión mínima especificada, o la versión más reciente del módulo si no se especifica ninguna versión mínima.
  - Si se especifica el parámetro RequiredVersion, Find-DscResource solo devuelve la versión del módulo que coincida exactamente con la versión especificada.
- Find-DscResource puede filtrar por los metadatos del módulo con el parámetro -Tag.
- Find-DscResource puede filtrar por el idioma de búsqueda específico del repositorio con el parámetro -Filter.
- Find-DscResource puede filtrar por los módulos de todos o algunos de los repositorios registrados.

## <a name="cmdlet-syntax"></a>Sintaxis de cmdlet
```powershell
Get-Command -Name Find-DscResource -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>Referencia de la ayuda en línea de cmdlet

[Find-DscResource](http://go.microsoft.com/fwlink/?LinkId=517196)

## <a name="example-commands"></a>Comandos de ejemplo
```powershell

# Find a specific DSC Resource
Find-DscResource -Name xIisFeatureDelegation

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
xIisFeatureDelegation               1.10.0.0   xWebAdministration                  PSGallery

# Find all available DSC Resources from all registered repositories
Find-DscResource

# Find a DSC resource by name
Find-DscResource -Name xWebsite

# Find multiple DSC Resources
Find-DscResource -Name xIisHandler, xFirewall

# Find all DSC resources contained within a specific module
Find-DscResource -ModuleName xNetworking
Find-DscResource -ModuleName xWebAdministration

# Find all DSC resources in modules with DSCResourceKit or DesiredStateConfiguration
Find-DscResource -Tag DesiredStateConfiguration, DSCResourceKit

# Find available DSC Resources from few registered repositories
Find-DscResource -Repository PSGallery,PrivatePSGallery

# Find all DSC Resources in a specified repository
Find-DscResource -Repository PSGallery

# Find DSC Resources from all versions of a module
Find-DscResource -ModuleName xNetworking -AllVersions

# Find DSC Resources with module name and MinimumVersion.
Find-DscResource -ModuleName xNetworking -MinimumVersion 1.1

# Find DSC Resources with module name and exact version
Find-DscResource -ModuleName xNetworking -RequiredVersion 2.1.1

# Find DSC Resources defined modules with -Filter based search. -Filter searches in description and module names
Find-DscResource -Filter Domain

# Find all DSC Resources with tags Azure or DSC in module metadata
Find-DscResource -Tag Azure, DSC

```

