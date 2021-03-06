---
title: Руководство по программированию на C#. Тестирование на равенство (идентичность) ссылок
description: Сведения о проверке на равенство (идентичность) ссылок. Изучите пример кода и ознакомьтесь с дополнительными ресурсами.
ms.date: 07/20/2015
helpviewer_keywords:
- object identity [C#]
- reference equality [C#]
ms.assetid: 91307fda-267b-4fd2-a338-2aada39ee791
ms.openlocfilehash: 1d1a0e5d80ac8d2a689e75acbc6099b92e16f23f
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/24/2020
ms.locfileid: "91151445"
---
# <a name="how-to-test-for-reference-equality-identity-c-programming-guide"></a>Руководство по программированию на C#. Тестирование на равенство (идентичность) ссылок

Вам не требуется реализовывать настраиваемую логику, чтобы обеспечить поддержку проверки ссылок на равенство в типах. Эту возможность для всех типов реализует метод <xref:System.Object.ReferenceEquals%2A?displayProperty=nameWithType>.  
  
 В следующем примере показано, как проверить две переменные на *равенство ссылок*, то есть как определить, ссылаются ли они на один и тот же объект в памяти.  
  
 В этом примере также показано, почему <xref:System.Object.ReferenceEquals%2A?displayProperty=nameWithType> всегда возвращает `false` для типов значений и почему не следует использовать <xref:System.Object.ReferenceEquals%2A> для проверки строк на равенство.  
  
## <a name="example"></a>Пример  

 [!code-csharp[csProgGuideObjects#90](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#90)]  
  
 Реализация `Equals` в универсальном базовом классе <xref:System.Object?displayProperty=nameWithType> также выполняет проверку на равенство ссылок, однако использовать такой подход не рекомендуется, поскольку в случае переопределения метода в классе результат может отличаться от ожидаемого. Это справедливо также для операторов `==` и `!=`. При работе со ссылочными типами операторы `==` и `!=` по умолчанию выполняют проверку на равенство ссылок. Тем не менее производные классы могут перегружать оператор для проверки на равенство значений. Чтобы свести к минимуму вероятность появления ошибки, рекомендуется всегда использовать <xref:System.Object.ReferenceEquals%2A> в тех случаях, когда требуется проверить два объекта на равенство ссылок.  
  
 Константные строки в рамках одной сборки всегда интернируются во время выполнения. Таким образом, всегда присутствует только один экземпляр каждого уникального строкового литерала. Тем не менее во время выполнения не гарантируется интернирование строк, созданных во время выполнения, а также интернирование двух равных константных строк из разных сборок.  
  
## <a name="see-also"></a>См. также

- [Сравнения на равенство](./equality-comparisons.md)
