---
description: Занятие 1-8. Добавление заметок и форматирование пакета занятия 1
title: Шаг 8. Добавление заметок и форматирование пакета занятия 1 | Документация Майкрософт
ms.custom: ''
ms.date: 06/29/2020
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: e3751e53-77c7-47d0-8fe8-73ed1a53413a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 08e5668fcdc3fe41e54965b01db9325c861fa98f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462043"
---
# <a name="lesson-1-8-annotate-and-format-the-lesson-1-package"></a>Занятие 1-8. Добавление заметок и форматирование пакета занятия 1 

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



После завершения настройки пакета, созданного на занятии 1, можно приступить к приведению его макета в порядок. Если фигуры в макетах элементов управления и потока данных имеют разные размеры или распределены неравномерно, то структуру пакета может быть трудно понять.  
  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools предоставляет средства, которые облегчают форматирование макета пакета. К функциям форматирования относится возможность создавать фигуры одного размера, выравнивать их, а также изменять пространство между фигурами по горизонтали и вертикали.  
  
Другим способом добиться лучшего понимания функциональности пакета является добавление заметок, описывающих функциональность пакета.  
  
В этой задаче используются функции форматирования [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools для улучшения макета потока данных и добавления к нему заметки.  
  
## <a name="format-the-layout-of-the-data-flow"></a>Форматирование макета потока данных  
  
1.  Если пакет, созданный на занятии 1, еще не открыт, дважды щелкните файл **Lesson 1.dtsx** в **обозревателе решений**.  
  
2.  Перейдите на вкладку **Поток данных**.  
  
3.  Чтобы выбрать сразу все компоненты потока данных, используйте команду **Правка** > **Выбрать все**.
  
4.  В меню **Формат** выберите команду **Установить тот же размер** и щелкните **Оба**.  
  
5.  При выделенных объектах потока данных в меню **Формат** выберите пункт **Выравнивание**, а затем пункт **По центру**.  

6.  При выделенных объектах потока данных в меню **Формат** наведите указатель на пункт **Интервал по вертикали** и выберите пункт **Сделать равным**.  
  
## <a name="add-an-annotation-to-the-data-flow"></a>Добавление заметки к потоку данных  
  
1.  Щелкните правой кнопкой мыши в области конструктора потока данных и выберите команду **Добавить заметку**.  
  
2.  В поле заметки введите или вставьте приведенный ниже текст.  
  
    Поток данных извлекает данные из файла, находит значения в столбце CurrencyKey таблицы DimCurrency и в столбце DateKey таблицы DimDate, после чего записывает данные в таблицу NewFactCurrencyRate.
  
    Чтобы в поле заметки перенести текст на следующую строку, поместите курсор в то место, где должна начинаться новая строка, и нажмите клавишу **ВВОД**.  
  
    Если в поле заметки текст не введен, то оно закрывается при щелчке за его пределами.  Поэтому если нужно вставить текст в поле заметки, скопируйте текст в буфер обмена перед выбором команды "Добавить заметку". 
  
## <a name="go-to-next-task"></a>Переход к следующей задаче
[Шаг 9. Тестирование пакета занятия 1](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
  
  
