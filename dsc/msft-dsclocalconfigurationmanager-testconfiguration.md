---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: dsc,powershell,configuration,setup
title: "Método TestConfiguration de la clase MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: 8e9986837aaf41b1396a2399c58675bc51b0b708
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2017
---
# <a name="testconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Método TestConfiguration de la clase MSFT_DSCLocalConfigurationManager

Envía el documento de configuración al nodo administrado y prueba la configuración actual frente al documento.

<a name="syntax"></a>Sintaxis
------

```mof
uint32 TestConfiguration(
  [in]  uint8                          configurationData[],
  [out] boolean                        InDesiredState,
  [out] MSFT_ResourceInDesiredState    ResourcesInDesiredState[],
  [out] MSFT_ResourceNotInDesiredState ResourcesNotInDesiredState[]
);
```

<a name="parameters"></a>Parámetros
----------

*configurationData* \[in\]  
Datos del entorno para la configuración.

*InDesiredState* \[out\]  
En la devolución, especifica si el nodo administrado está en el estado especificado por el documento de configuración.

*ResourcesInDesiredState* \[out\]  
En la devolución, contiene una instancia incrustada de la clase **MSFT_ResourceInDesiredState**, que especifica los recursos que están en el estado deseado.

*ResourcesNotInDesiredState* \[out\]  
En la devolución, contiene una instancia incrustada de la clase **MSFT_ResourceNotInDesiredState**, que especifica los recursos que no están en el estado deseado.

## <a name="return-value"></a>Valor devuelto
------------

Devuelve cero si se ejecuta correctamente; de lo contrario, devuelve un código de error.

## <a name="remarks"></a>Observaciones

Se trata de un método estático.

## <a name="requirements"></a>Requisitos
------------
>**MOF:** DscCore.mof

>**Espacio de nombres**: Root\Microsoft\Windows\DesiredStateConfiguration


## <a name="see-also"></a>Vea también


[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)


 

 



