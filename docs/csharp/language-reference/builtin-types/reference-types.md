---
title: Встроенные ссылочные типы — справочник по C#
description: Дополнительные сведения о ссылочных типах, имеющих ключевые слова C#, которые можно использовать для их объявления.
ms.date: 06/25/2019
f1_keywords:
- object_CSharpKeyword
- object
- delegate_CSharpKeyword
- delegate
- dynamic_CSharpKeyword
- string
- string_CSharpKeyword
helpviewer_keywords:
- object keyword [C#]
- delegate keyword [C#]
- function pointers [C#]
- dynamic [C#]
- dynamic keyword [C#]
- strings [C#], reference
- '@ string literal'
- string literals [C#]
- string keyword [C#]
ms.openlocfilehash: c2c03f47babd9ccf87eb60d33b9d65d1a9c82e2e
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223508"
---
# <a name="built-in-reference-types-c-reference"></a>Встроенные ссылочные типы (справочник по C#)

В C# есть ряд встроенных ссылочных типов. У них есть ключевые слова или операторы, которые являются синонимами типа в библиотеке .NET.

## <a name="the-object-type"></a>Тип object

Тип `object` является псевдонимом <xref:System.Object?displayProperty=nameWithType> в .NET. В унифицированной системе типов C# все типы, стандартные и определяемые пользователем, ссылочные типы и типы значений напрямую или косвенно наследуются из <xref:System.Object?displayProperty=nameWithType>. Переменным типа `object` можно назначать значения любого типа. Любой переменной `object` можно назначить значение по умолчанию с помощью литерала `null`. Если переменная значимого типа преобразуется в объект, она считается *упакованной* . Если переменная типа `object` преобразуется в значимый тип, она считается *распакованной* . Дополнительные сведения см. в разделе [Упаковка-преобразование и распаковка-преобразование](../../programming-guide/types/boxing-and-unboxing.md).

## <a name="the-string-type"></a>Тип string

Тип `string` представляет последовательность, состоящую из нуля или более символов в кодировке Юникод. `string` является псевдонимом для <xref:System.String?displayProperty=nameWithType> в .NET.

Несмотря на то что `string` представляет собой ссылочный тип, [операторы равенства `==` и `!=`](../operators/equality-operators.md#string-equality) по определению сравнивают не ссылки, а значения объектов `string`. Это делает проверку равенства строк более интуитивно понятной. Пример:

```csharp-interactive
string a = "hello";
string b = "h";
// Append to contents of 'b'
b += "ello";
Console.WriteLine(a == b);
Console.WriteLine(object.ReferenceEquals(a, b));
```

Отображается значение True, а затем False, поскольку содержимое строк эквивалентно, однако `a` и `b` не относятся к одному и тому же экземпляру строки.

[Оператор +](../operators/addition-operator.md#string-concatenation) объединяет строки:

```csharp
string a = "good " + "morning";
```

При этом создается строковый объект, содержащий слова "good morning".

Строки *неизменяемы* , т. е. содержимое созданного строкового объекта изменить нельзя, хотя синтаксис выглядит так, будто это возможно. Например, при написании кода компилятор фактически создает новый строковый объект для хранения новой последовательности символов, а затем этот новый объект назначается `b`. Память, выделенная для `b` (если он содержит строку h), затем доступна для сборки мусора.

```csharp
string b = "h";
b += "ello";
```

 [Оператор](../operators/member-access-operators.md#indexer-operator-)`[]` позволяет предоставить к отдельным символам строки доступ только на чтение. Допустимые значения индекса начинаются с `0` и должны быть меньше, чем длина строки:

```csharp
string str = "test";
char x = str[2];  // x = 's';
```

Также оператор `[]` можно использовать для итерации каждого символа в строке:

```csharp-interactive
string str = "test";

for (int i = 0; i < str.Length; i++)
{
  Console.Write(str[i] + " ");
}
// Output: t e s t
```

Строковые литералы имеют тип `string` и могут быть записаны в двух формах: в кавычках (") или в кавычках с префиксом `@`. Строковые литералы в кавычках заключаются в двойные кавычки ("):

```csharp
"good morning"  // a string literal
```

Строковые литералы могут содержать любые символьные литералы. Escape-последовательности включены. В следующем примере escape-последовательность `\\` используется для получения обратной косой черты, `\u0066` — для получения буквы f, и `\n` — для получения новой строки.

```csharp-interactive
string a = "\\\u0066\n F";
Console.WriteLine(a);
// Output:
// \f
//  F
```

> [!NOTE]
> Escape-код `\udddd` (где `dddd` состоит из четырех цифр) представляет символ Юникода U+`dddd`. Также распознаются восьмизначные escape-коды Юникода: `\Udddddddd`.

[Буквальные строковые литералы](../tokens/verbatim.md) начинаются с `@` и также заключаются в двойные кавычки. Пример:

```csharp
@"good morning"  // a string literal
```

Преимущество буквальных строк состоит в том, что escape-последовательности *не* обрабатываются, что позволяет легко написать, например, полное имя файла Windows:

```csharp
@"c:\Docs\Source\a.txt"  // rather than "c:\\Docs\\Source\\a.txt"
```

Чтобы добавить в строку @-quoted двойные кавычки, продублируйте этот символ:

```csharp
@"""Ahoy!"" cried the captain." // "Ahoy!" cried the captain.
```

## <a name="the-delegate-type"></a>Тип delegate

Объявление типа делегата аналогично сигнатуре метода. Оно имеет возвращаемое значение и любое число параметров любого типа:

```csharp
public delegate void MessageDelegate(string message);
public delegate int AnotherDelegate(MyType m, long num);
```

В .NET типы `System.Action` и `System.Func` предоставляют общие определения для многих распространенных делегатов. Скорее всего, не нужно определять новые пользовательские типы делегата. Вместо этого можно создать экземпляры предоставленных универсальных типов.

Ключевое слово `delegate` имеет ссылочный тип, который можно использовать для инкапсуляции именованного или анонимного метода. Делегаты аналогичны используемым в языке C++ указателям функций, но являются типобезопасными и безопасными. Сведения о применении делегатов см. в разделах [Делегаты](../../programming-guide/delegates/index.md) и [Универсальные делегаты](../../programming-guide/generics/generic-delegates.md). Делегаты являются основой [событий](../../programming-guide/events/index.md). Экземпляры делегата могут создаваться путем его связывания с именованным или анонимным методом.

Делегат должен быть создан при помощи метода или лямбда-выражения, имеющего совместимые возвращаемый тип и входные параметры. Дополнительные сведения о допустимой степени вариации сигнатур методов см. в разделе [Вариативность в делегатах](../../programming-guide/concepts/covariance-contravariance/using-variance-in-delegates.md). Для использования с анонимными методами делегат и код, который должен быть связан с ним, должны быть объявлены вместе.

## <a name="the-dynamic-type"></a>Тип dynamic

Тип `dynamic` указывает, что использование переменной и ссылок на ее члены обходит проверку типа во время компиляции. Такие операции разрешаются во время выполнения. Тип `dynamic` упрощает доступ к API COM, таким как API автоматизации Office, к динамическим API, таким как библиотеки IronPython, и к HTML-модели DOM.

Тип `dynamic` в большинстве случаев ведет себя как тип `object`. В частности, можно преобразовать любое выражение, отличное от NULL, в тип `dynamic`. Тип `dynamic` отличается от `object` тем, что операции, которые содержат выражения типа `dynamic`, не разрешаются или тип проверяется компилятором. Компилятор объединяет сведения об операции, которые впоследствии будут использоваться для оценки этой операции во время выполнения. В рамках этого процесса переменные типа `dynamic` компилируются в переменные типа `object`. Таким образом, тип `dynamic` существует только во время компиляции, но не во время выполнения.

В следующем примере переменной типа `dynamic` противопоставляется переменная типа `object`. Чтобы проверить тип каждой переменной во время компиляции, наведите указатель мыши на `dyn` или `obj` в операторах `WriteLine`. Скопируйте следующий код в редактор, где доступен IntelliSense. IntelliSense отображает **dynamic** для `dyn` и **object** для `obj`.

[!code-csharp[csrefKeywordsTypes#21](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/dynamic1.cs#21)]

Операторы <xref:System.Console.WriteLine%2A> отображают типы времени выполнения `dyn` и `obj`. На этом этапе оба имеют один и тот же тип — целое число. Выводятся следующие результаты.

```console
System.Int32
System.Int32
```

Чтобы увидеть разницу между `dyn` и `obj` во время компиляции, добавьте между объявлениями и операторами `WriteLine` в предыдущем примере следующие две строки:

```csharp
dyn = dyn + 3;
obj = obj + 3;
```

 При попытке добавления целого числа и объекта в выражение `obj + 3` выдается ошибка компилятора. При этом для `dyn + 3` ошибка не возникает. Выражение, которое содержит `dyn`, не проверяется во время компиляции, поскольку тип `dyn` имеет значение `dynamic`.

В следующем примере `dynamic` используется в нескольких объявлениях. Метод `Main` также противопоставляет проверку типов во время компиляции.

[!code-csharp[csrefKeywordsTypes#25](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/dynamic2.cs#25)]

### <a name="see-also"></a>См. также

- [Справочник по C#](../index.md)
- [Ключевые слова в C#](../keywords/index.md)
- [События](../../programming-guide/events/index.md)
- [Использование типа dynamic](../../programming-guide/types/using-type-dynamic.md)
- [Рекомендации по использованию строк](../../../standard/base-types/best-practices-strings.md)
- [Базовые операции со строками в .NET Framework](../../../standard/base-types/basic-string-operations.md)
- [Создание строк](../../../standard/base-types/creating-new.md)
- [Операторы приведения и тестирования типов](../operators/type-testing-and-cast.md)
- [Практическое руководство. Безопасное приведение с помощью сопоставления шаблонов, а также операторов is и as](../../how-to/safely-cast-using-pattern-matching-is-and-as-operators.md)
- [Пошаговое руководство. Создание и использование динамических объектов (C# и Visual Basic)](../../programming-guide/types/walkthrough-creating-and-using-dynamic-objects.md)
- <xref:System.Object?displayProperty=nameWithType>
- <xref:System.String?displayProperty=nameWithType>
- <xref:System.Dynamic.DynamicObject?displayProperty=nameWithType>
