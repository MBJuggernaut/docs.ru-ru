---
title: Практическое руководство. Отмена цикла Parallel.For или Parallel.ForEach
description: Вы можете отменить цикл Parallel.For или Parallel.ForEach в .NET, предоставив методу объект токена отмены в параметре ParallelOptions.
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parallel foreach loop, how to cancel
- parallel for loops, how to cancel
ms.assetid: 9d19b591-ea95-4418-8ea7-b6266af9905b
ms.openlocfilehash: 0a22794f3c45e685a80d36a42ecd849461936c7b
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2020
ms.locfileid: "84769006"
---
# <a name="how-to-cancel-a-parallelfor-or-foreach-loop"></a>Практическое руководство. Отмена цикла Parallel.For или Parallel.ForEach
Метод <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> и <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> поддерживают отмену с применением маркеров отмены. Дополнительные сведения о механизмах отмены в целом см. в [этой статье](../threading/cancellation-in-managed-threads.md). В параллельном цикле <xref:System.Threading.CancellationToken> передается в методу через параметр <xref:System.Threading.Tasks.ParallelOptions>, и этот параллельный вызов заключен в блок try-catch.  
  
## <a name="example"></a>Пример  
 Следующий пример демонстрирует, как отменить вызов <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType>. Этот же подход вы можете применить и к вызову <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType>.  
  
 [!code-csharp[TPL_Parallel#29](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/parallel_cancel.cs#29)]
 [!code-vb[TPL_Parallel#29](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/cancelloop.vb#29)]  
  
 Если маркер, сообщающий об отмене, совпадает с указанным в экземпляре <xref:System.Threading.Tasks.ParallelOptions>маркером, то параллельный цикл создаст для отмены одно исключение <xref:System.OperationCanceledException>. Если отмена вызвана другим маркером, цикл создаст исключение <xref:System.AggregateException> и вложит в него <xref:System.OperationCanceledException> в качестве значения InnerException.  
  
## <a name="see-also"></a>См. также

- [Параллелизм данных](data-parallelism-task-parallel-library.md)
- [Лямбда-выражения в PLINQ и TPL](lambda-expressions-in-plinq-and-tpl.md)
