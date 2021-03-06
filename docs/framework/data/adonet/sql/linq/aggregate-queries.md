---
title: Статистические запросы
ms.date: 03/30/2017
ms.assetid: 13ec5580-05ce-4a1f-9d3d-8660be7891a2
ms.openlocfilehash: 8dfe24a84c707b6d21afb7ccfc57ac7b0423942f
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/24/2020
ms.locfileid: "91161546"
---
# <a name="aggregate-queries"></a>Статистические запросы

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] поддерживает агрегатные операторы `Average`, `Count`, `Max`, `Min` и `Sum`. Обратите внимание на следующие характеристики агрегатных операторов в [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
- Агрегатные запросы выполняются немедленно.  
  
     Дополнительные сведения см. в разделе [Введение в запросы LINQ (C#)](../../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md).  
  
- Агрегатные запросы обычно возвращают число, а не коллекцию.  
  
     Дополнительные сведения см. в разделе [операции агрегирования](/previous-versions/visualstudio/visual-studio-2013/bb546138(v=vs.120)).  
  
- В анонимном типе вызвать агрегаты нельзя.  
  
 В следующих разделах используются примеры из учебной базы данных Northwind. Дополнительные сведения см. в статье [Загрузка образцов баз данных](downloading-sample-databases.md).  
  
## <a name="in-this-section"></a>в этом разделе  

 [Возврат среднего значения из числовой последовательности](return-the-average-value-from-a-numeric-sequence.md)  
 Демонстрируется использование оператора <xref:System.Linq.Enumerable.Average%2A>.  
  
 [Подсчет количества элементов в последовательности](count-the-number-of-elements-in-a-sequence.md)  
 Демонстрируется использование оператора <xref:System.Linq.Enumerable.Count%2A>.  
  
 [Нахождение максимального значения в числовой последовательности](find-the-maximum-value-in-a-numeric-sequence.md)  
 Демонстрируется использование оператора <xref:System.Linq.Enumerable.Max%2A>.  
  
 [Нахождение минимального значения в числовой последовательности](find-the-minimum-value-in-a-numeric-sequence.md)  
 Демонстрируется использование оператора <xref:System.Linq.Enumerable.Min%2A>.  
  
 [Вычисление суммы значений в числовой последовательности](compute-the-sum-of-values-in-a-numeric-sequence.md)  
 Демонстрируется использование оператора <xref:System.Linq.Enumerable.Sum%2A>.  
  
## <a name="related-sections"></a>См. также  

 [Примеры запросов](query-examples.md)  
 Содержит ссылки на запросы [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] в Visual Basic и C#.  
  
 [Основные принципы запросов](query-concepts.md)  
 Содержит ссылки на разделы, в которых объясняются основные понятия для разработки запросов LINQ в [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] .  
  
 [Введение в запросы LINQ (C#)](../../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md)  
 Объясняет, как работают запросы в LINQ.
