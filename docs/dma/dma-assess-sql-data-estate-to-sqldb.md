---
title: Оценить готовность недвижимости данных SQL Server, переход на базу данных SQL Azure | Документация Майкрософт
description: Узнайте, как использовать Data Migration Assistant для переноса пространства данных SQL Server для миграции в базу данных SQL Azure
ms.custom: ''
ms.date: 07/16/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: jroth
ms.openlocfilehash: d317fb3f0c2227744318eeaead71514095afbdec
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/16/2019
ms.locfileid: "68269386"
---
# <a name="assess-the-readiness-of-a-sql-server-data-estate-migrating-to-azure-sql-database-using-the-data-migration-assistant"></a>Оценить готовность недвижимости данных SQL Server, переход на базу данных SQL Azure с помощью Data Migration Assistant

Миграция сотни экземпляров SQL Server и тысяч баз данных в базу данных SQL Azure, наши предложением платформа как услуга (PaaS), выполняется много. Чтобы оптимизировать процесс настолько, насколько возможно, вам потребуется уверены, что относительный готовность к миграции. Определение титанических усилий, включая серверы и базы данных, полностью готовых или, требует минимальных усилий по подготовке к переходу, упрощает и ускоряет ваши усилия.

Эта статья содержит пошаговые инструкции по использованию [Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview?view=sql-server-2017) для суммирования результатов готовности и разместить их на ["Миграция Azure"](https://portal.azure.com/?feature.customPortal=false#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview) концентратора.

## <a name="create-a-project-and-add-a-tool"></a>Создайте проект и добавить средство

Настройка нового проекта "Миграция Azure" в подписке Azure, а затем добавьте это средство.

Это проект с "Миграция Azure" используется для хранения ознакомления, оценки и миграции метаданные, собранные из среды вы оценки или миграции. Проект также использовать для отслеживания обнаруженных активов и координирования внутренней оценки и миграции.

1. Войдите на портал Azure, выберите **все службы**, а затем найдите "Миграция Azure".
2. В разделе **служб**выберите **"Миграция Azure"** .

   !["Миграция Azure" — выберите службы](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-services.png)

3. На **Обзор** выберите **оценка и миграция баз данных**.

   !["Миграция Azure" — Запуск оценки](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

4. В **баз данных**в разделе **Приступая к работе**выберите **добавьте произведите**.

   ![Служба "Миграция Azure" — Добавление средств](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tools.png)

5. На **проекта "Миграция"** выберите вашей подписке и группе ресурсов Azure (если у вас еще нет группы ресурсов, создайте ее).
6. В разделе **сведения о проекте**, укажите имя проекта и geography, в котором вы хотите создать проект.

    ![Служба "Миграция Azure" — Добавление диалогового окна инструментов](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tool-dialog.png)

    Можно создать проект "Миграция Azure" в любом из этих географических регионах.

    | **Geography**  | **Регион расположения хранилища** |
    | ------------- | ------------- |
    | Азия | Юго-Восточная Азия и Восточная Азия |
    | Европа | Южная Европа и Западная Европа |
    | United Kingdom | Южная часть соединенного Королевства или Западная часть соединенного Королевства |
    | США | Центральная часть США или Западная часть США 2 |

    Geography, указанной для проекта используется только для хранения метаданные, полученные из локальных виртуальных машин. Вы можете выбрать любой целевой регион фактической миграции.

7. Выберите **Далее**, а затем добавьте средство оценки.

   > [!NOTE]
   > При создании проекта, необходимо добавить хотя бы один инструмент оценки или миграции.

8. На **средство оценки выберите** вкладке **"Миграция Azure": Оценку базы данных** отображается как средство оценки для добавления. Если вам не нужны в данный момент средство оценки, выберите **пропустить добавление средство оценки сейчас** "флажок". Выберите **Далее**.

    !["Миграция Azure" - Вкладка инструментов выберите оценки](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-assessment-tool.png)

9. На **выберите миграция** вкладке **"Миграция Azure": Миграция базы данных** отображается как средство миграции, чтобы добавить. Если вам не требуется в настоящее время средство миграции, выберите **пропустить добавление средства миграции сейчас**. Выберите **Далее**.

    !["Миграция Azure" - Вкладка инструментов выберите миграции](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-migration-tool.png)

10. В **просмотрите + добавить средства**, просмотрите параметры затем выберите **добавить средства**.

    !["Миграция Azure" — Проверка + добавить вкладку инструменты](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-tools.png)

    После создания проекта, можно выбрать дополнительные средства для оценки и миграции серверов и рабочих нагрузок, баз данных и веб-приложений.

## <a name="assess-and-upload-assessment-results"></a>Оценить и отправить результаты оценки

После успешного создания проекта миграции, в разделе **инструменты оценки**в **"Миграция Azure": Оценку базы данных** поле, инструкции по скачиванию и с помощью Data Migration Assistant средство отображения.

   !["Миграция Azure" — добавлены средства оценки](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessment-tool-added.png)

1. Скачайте помощник по миграции данных с помощью приведенной ссылке и установите его на компьютере с доступом к экземплярам SQL Server источника.
2. Запустите помощник по миграции данных.

### <a name="create-an-assessment"></a>Создать оценку

1. С левой стороны экрана выберите **+** значок, а затем выберите оценку **тип проекта**
2. Укажите имя проекта, а затем выберите исходный и целевой сервер типов.

    При обновлении на локальный экземпляр SQL Server до более поздней версии SQL Server или SQL Server, размещенных на виртуальной Машине Azure, задайте тип исходной и целевой сервер **SQL Server**. Задайте тип целевого сервера **Azure базы данных SQL управляемого экземпляра** для оценки готовности целевой базы данных SQL Azure (PaaS).

3. Выберите **Создать**.

   !["Миграция Azure" — интерфейс помощника по миграции данных](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-interface.png)

### <a name="choose-assessment-options"></a>Выберите параметры оценки

1. Выбор типа отчета.

    Можно выбрать один или оба из следующих типов отчетов:
    * Проверка совместимости базы данных
    * Проверка четности компонентов.

   ![Экран параметров оценки Azure - Data Migration Assistant - служба "Миграция"](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-options-screen.png)

2. Выберите **Далее**.

### <a name="add-databases-to-assess"></a>Добавление баз данных для оценки

1. Выберите **добавить источники** для открытия подключения вылете меню.
2. Введите имя экземпляра SQL server, выберите тип проверки подлинности, задайте свойства подключения и затем выберите **Connect**.
3. Выберите базы данных для оценки, а затем выберите **добавить**.

   > [!NOTE]
   > Можно удалить несколько баз данных, выбрав их, удерживая нажатой клавишу Shift или Ctrl, а затем нажать клавишу удалить источники. Также можно добавлять базы данных с несколькими экземплярами SQL Server с помощью кнопки Добавить источники.

4. Выберите **Далее** для запуска оценки.

   ![Экран выбора источников Azure - Data Migration Assistant - служба "Миграция"](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-select-sources-screen.png)

5. После завершения оценки выберите **отправить в "Миграция Azure"** .

   ![Результаты Пересмотр Azure - Data Migration Assistant - служба "Миграция"](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-review-results-screen.png)

6. Войдите на портал Azure.

   ![Результаты Пересмотр Azure - Data Migration Assistant - служба "Миграция"](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-signin.png)

7. Выберите подписку и проекта "Миграция Azure", в которые вы хотите отправить результаты оценки, а затем выберите **отправить**.

   Дождитесь подтверждения отправки оценки.

## <a name="view-target-readiness-assessment-results"></a>Просмотр результатов оценки готовности целевой объект

1. Выполните вход на портале Azure, найдите "Миграция Azure" и выберите **"Миграция Azure"** .

   ![Служба поиска Azure — портал Azure — служба "Миграция"](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-search.png)

2. Выберите **оценка и миграция баз данных** для получения результатов оценки.

   !["Миграция Azure" — Просмотр результатов оценки](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

    Можно просмотреть сводку готовности к SQL Server, убедитесь, что вы в проекте миграции справа, в противном случае используйте изменений, параметр, чтобы выбрать другой миграции проекта.

    При каждом обновлении результатов оценки в Azure перенести проект, "Миграция Azure" Центр все результаты объединения и обеспечения сводного отчета.  Можно выполнять несколько оценок помощник по миграции данных в параллельном режиме и отправить результаты в проект миграций, чтобы получить отчет о готовности консолидированные.

   !["Миграция Azure" — Просмотр готовности результатов](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-readiness.png)

    **Экземпляры базы данных, оценивается ли**:  Число экземпляров SQL Server, оценивается ли данный момент.
    **Базы данных, оценивается ли**: Общее количество баз данных, оценивается ли для одного или нескольких экземпляров SQL Server, оценивается ли **баз данных, готовые для баз данных SQL**:  Число баз данных, готовы к миграции базы данных SQL Azure (PaaS).
    **Базы данных, готовые к виртуальной Машине SQL Azure**:  Количество баз данных включать один или несколько проблем, препятствующих миграции к базе данных SQL Azure (PaaS), но готовы к миграции виртуальных машин Azure SQL Server.

3. Выберите **экземпляров баз данных, оценивается ли** получить представление уровня экземпляра SQL Server.

   !["Миграция Azure" — Проверка готовности экземпляр](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-instances.png)

    Можно найти состояние готовности в процентах каждого экземпляра SQL Server, переход на базу данных SQL Azure (PaaS).

4. Выберите конкретный экземпляр, чтобы получить представление о готовности базы данных.

   !["Миграция Azure" — Проверка готовности базы данных](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-databases.png)

    Вы увидите число блокирований миграции для каждой базы данных предназначено для каждой базы данных в представлении выше.

5. Просмотрите результаты оценки DMA для получения дополнительных сведений для решения проблем, препятствующих миграции.

   !["Миграция Azure" — ошибки проверки переноса](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-migration-blockers.png)

## <a name="see-also"></a>См. также

* [Data Migration Assistant (DMA)](../dma/dma-overview.md)
* [Помощник по миграции данных: Параметры конфигурации](../dma/dma-configurationsettings.md)
* [Помощник по миграции данных: Советы и рекомендации](../dma/dma-bestpractices.md)