---
title: IServerVirtualDeviceSet2::BeginConfiguration
titlesuffix: SQL Server VDI reference
description: В этой статье приводятся справочные сведения о команде IServerVirtualDeviceSet2::BeginConfiguration.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: d188c79a558fcfe03b713a973cf0681822e24ba5
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2020
ms.locfileid: "85887615"
---
# <a name="iservervirtualdeviceset2beginconfiguration-vdi"></a>IServerVirtualDeviceSet2::BeginConfiguration (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

Сервер вызывает функцию **BeginConfiguration** для начала настройки набора виртуальных устройств.

## <a name="syntax"></a>Синтаксис

```c
HRESULT IServerVirtualDeviceSet2::BeginConfiguration (
   DWORD   dwFeatures,
   DWORD   dwAlignment,
   DWORD   dwBlockSize,
   DWORD   dwMaxTransferSize,
   DWORD   dwTimeout
);
```

## <a name="parameters"></a>Параметры

*dwFeatures* — маска измененных функций. VDF_WriteMedia и (или) VDF_ReadMedia.

*dwAlignment* — итоговое выравнивание. Если указано значение 0, по умолчанию используется dwBlockSize. Значение должно быть степенью двойки, не менее dwBlockSize и не более 64 КБ.

*dwBlockSize* — минимальная единица передачи в байтах. Значение должно быть степенью двойки, не менее 512 и не более 64 КБ.

*dwMaxTransferSize* — максимально возможный передаваемый объем. Значение должно быть кратно 64 КБ.

*dwTimeout* — время ожидания (в миллисекундах) завершения объявления основным клиентом предоставляемых областей буфера.

## <a name="return-value"></a>Возвращаемое значение

|Возвращаемое значение | Объяснение |
|---|---|
| NOERROR | Набор виртуальных устройств находится в настраиваемом состоянии. |
| VD_E_ABORT | Вызван SignalAbort. |
| VD_E_PROTOCOL | Набор виртуальных устройств находится в подключенном состоянии. |

## <a name="remarks"></a>Remarks

После вызова этой функции набор виртуальных устройств переходит в настраиваемое состояние, в котором выбирается макет буфера.
После задания базовой конфигурации (согласно параметрам) эти значения сохраняются в течение всего времени существования набора виртуальных устройств. Свойство выравнивания для набора виртуальных устройств служит для управления выравниванием буферов данных. Это значение определяет минимальное выравнивание, которое можно переопределять для отдельных буферов.

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения см. в [справке по интерфейсу виртуальных устройств SQL Server](reference-virtual-device-interface.md).