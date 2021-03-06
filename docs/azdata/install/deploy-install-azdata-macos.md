---
title: Установка azdata для macOS
titleSuffix: ''
description: Узнайте, как установить средство azdata в macOS.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 19a3542f77708dcf779cf01d5299e7ff6add8273
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725245"
---
# <a name="install-azdata-on-macos"></a>Установка `azdata` в macOS

`azdata-cli` можно установить на платформе macOS с помощью диспетчера пакетов Homebrew. Пакет CLI протестирован с macOS следующих версий:

- 10.13 High Sierra;
- 10.14 Mojave;
- 10.15 Catalina.

## <a name="install-with-homebrew"></a>Установка с помощью Homebrew

```bash
brew tap microsoft/azdata-cli-release
brew update
brew install azdata-cli
```

>[!IMPORTANT]
>`azdata-cli` имеет зависимость от пакетов Homebrew `python3`, `freetds`, `unixodbc` и `zeromq`, поэтому устанавливает их автоматически. Для `azdata-cli` гарантируется совместимость с последними версиями этих зависимостей, опубликованными в Homebrew.

## <a name="verify-install"></a>Проверка установки

```bash
azdata
azdata --version
```

## <a name="update"></a>Update

Обновите сведения о локальном репозитории, а затем — сам пакет `azdata-cli`.

```bash
brew tap microsoft/azdata-cli-release
brew update
brew upgrade azdata-cli
```

## <a name="uninstall"></a>Удаление

Для удаления пакета `azdata-cli` воспользуйтесь Homebrew.

```bash
brew uninstall azdata-cli
```

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о кластерах больших данных см. в статье [Что такое [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md).

Использование azdata со [службами данных с поддержкой Azure Arc](/azure/azure-arc/data/)
