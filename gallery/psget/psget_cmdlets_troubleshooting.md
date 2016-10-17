## Cómo resolver el problema "WARNING: Package 'your package name' failed to download" (ADVERTENCIA: No se pudo descargar el paquete 'nombre del paquete'")




Se ha notificado que a veces se produce un error en Install-Module o Update-Module en algunos equipos.
Según nuestras investigaciones, este problema está relacionado con la conexión de red.
Hemos actualizado recientemente el proveedor de NuGet para que pueda descargar paquetes de forma confiable.
Puede seguir las instrucciones siguientes para instalar la compilación más reciente del proveedor de NuGet y, después, instalar o actualizar el módulo.
En este ejemplo se usa el módulo "Azure".

```powershell
Install-PackageProvider NuGet -MinimumVersion 2.8.5.206 -Force
Launch new PowerShell Console
Update-Module Azure -Verbose
```


<!--HONumber=Aug16_HO3-->

