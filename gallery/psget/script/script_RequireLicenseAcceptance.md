---
ms.date: 2017-06-09
schema: 2.0.0
keywords: powershell
title: RequireLicenseAcceptanceScript
ms.openlocfilehash: 7092fb2e63b9e2b1eca59cd418317631bff8b172
ms.sourcegitcommit: cd66d4f49ea762a31887af2c72d087b219ddbe10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/11/2017
---
# <a name="requiring-license-acceptance-for-scripts"></a>Requerir la aceptación de la licencia para Scripts

No se admite la aceptación de la licencia para los scripts. Sin embargo, sí se admite el escenario en que un script depende de un módulo que requiere la aceptación de la licencia.

Los comandos de script (Install-Script/Save-Script/Update-Script) admiten un parámetro nuevo, -AcceptLicense, que se comporta como si el usuario hubiese visto la licencia. Si no se especifica -AcceptLicense, el usuario verá el archivo license.txt para el módulo dependiente y se le pedirá que acepte la licencia.

## <a name="examples"></a>EJEMPLOS

### <a name="example-1-install-script-with-dependencies-requiring-license-acceptance"></a>Ejemplo 1: instalación de un script con dependencias que requiere la aceptación de la licencia
El script "ScriptRequireLicenseAcceptance" depende del módulo "ModuleRequireLicenseAcceptance". Se solicita al usuario que acepte la licencia.
```PowerShell
PS C:\> Install-Script -Name ScriptRequireLicenseAcceptance

License Acceptance
MIT License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): 
```

### <a name="example-2-install-script-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a>Ejemplo 2: instalación de un script con dependencias que requiere la aceptación de la licencia y -AcceptLicense
El script "ScriptRequireLicenseAcceptance" depende del módulo "ModuleRequireLicenseAcceptance". No se le pide al usuario que acepte la licencia porque se especifica -AcceptLicense.
```PowerShell
PS C:\> Install-Script -Name ScriptRequireLicenseAcceptance -AcceptLicense
```

## <a name="more-details"></a>Más detalles
### <a name="require-license-acceptance-support-for-modulesmodulerequirelicenseacceptancemd"></a>[Compatibilidad de Requerir la aceptación de la licencia para los módulos](../module/RequireLicenseAcceptance.md)

### <a name="require-license-acceptance-support-on-powershellgallerypsgallerypsgalleryrequireslicenseacceptancemd"></a>[Compatibilidad de Requerir la aceptación de la licencia en PowerShellGallery](../../psgallery/psgallery_requires_license_acceptance.md)

### <a name="require-license-acceptance-on-deploy-to-azure-automationpsgallerypsgallerydeploytoazureautomationrequirelicenseacceptancemd"></a>[Requerir la aceptación de licencia de Implementar en Azure Automation](../../psgallery/psgallery_deploy_to_azure_automation_requireLicenseAcceptance.md)
