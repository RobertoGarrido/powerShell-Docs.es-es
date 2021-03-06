---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 5b9eea1c90bfd5a8cee3897d832bf7775a750308
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2017
---
# <a name="separation-of-node-and-configuration-ids"></a>Separación de los identificadores de nodo y de configuración

## <a name="overview"></a>Introducción

Con el fin de proporcionar una experiencia más flexible y simplificada al usar DSC en modo de extracción, hemos agregado una serie de características en esta versión. Estas características están diseñadas para que pueda tener la flexibilidad de configurar e implementar con facilidad las configuraciones en varios nodos, y seguir realizando el seguimiento de la información de estado y generación de informes de cada nodo individualmente. Estas características son:

* Un nombre de configuración que identifica la configuración de un equipo. Este nombre pueden compartirlo varios nodos de destino. 
* Un identificador de agente que identifica de forma única un solo nodo.
* Un paso de registro que solo se produce la primera vez que un nodo de destino se conecta a un servidor de extracción.

**Nota:** Estas características y funciones se han agregado, pero no reemplazan los conceptos ni las características de extracción existentes. Puede usar estas nuevas características o las anteriores con el nuevo servidor de extracción que se incluye en esta versión.

Para más información, consulte [Configuración de un cliente de extracción mediante nombres de configuración](https://msdn.microsoft.com/powershell/dsc/pullclientconfignames)

