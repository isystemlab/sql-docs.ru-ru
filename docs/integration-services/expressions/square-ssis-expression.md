---
description: SQUARE (выражение служб SSIS)
title: SQUARE (выражение служб SSIS) | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQUARE
- square values
ms.assetid: cecf1bb2-3d55-40a6-9688-ed67bcc150b4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 314c6c36b7a7de24065e1051086158823feff46a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/17/2020
ms.locfileid: "88348100"
---
# <a name="square-ssis-expression"></a>SQUARE (выражение служб SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Возвращает квадрат числового выражения.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
SQUARE(numeric_expression)  
```  
  
## <a name="arguments"></a>Аргументы  
 *numeric_expression*  
 Числовое выражение любого типа числовых данных. Дополнительные сведения см. в разделе [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Типы результата  
 DT_R8  
  
## <a name="remarks"></a>Комментарии  
 Функция SQUARE возвращает значение NULL, если аргумент принимает значение NULL.  
  
 Перед операцией возведения в квадрат аргумент приводится к типу данных DT_R8.  
  
## <a name="expression-examples"></a>Примеры выражений  
 Этот пример возвращает квадрат числа 12. Возвращается результат 144.  
  
```  
SQUARE(12)  
```  
  
 Этот пример возвращает квадрат результата вычитания значений в двух столбцах. Если **Value1** содержит число 12, а **Value2** содержит число 4, функция SQUARE возвращает 64.  
  
```  
SQUARE(Value1 - Value2)  
```  
  
 Этот пример возвращает длину третьей стороны прямоугольного треугольника путем применения функции SQUARE к двум переменным, а затем вычисления квадратного корня из суммы получившихся значений. Если **Side1** содержит 3, а **Side2** содержит 4, функция SQRT возвращает 5.  
  
```  
SQRT(SQUARE(@Side1) + SQUARE(@Side2))  
```  
  
> [!NOTE]  
>  В выражениях имена переменных всегда содержат префикс \@.  
  
## <a name="see-also"></a>См. также:  
 [Функции (выражение служб SSIS)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
