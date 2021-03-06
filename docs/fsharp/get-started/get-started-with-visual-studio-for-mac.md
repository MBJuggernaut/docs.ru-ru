---
title: Начало работы с F# в Visual Studio для Mac
description: Узнайте, как использовать F# с Visual Studio для Mac.
ms.date: 07/03/2018
ms.openlocfilehash: cd45ab9c59cef76e4bf85a93f39d8e2ee063d200
ms.sourcegitcommit: 93762e1a0dae1b5f64d82eebb7b705a6d566d839
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/27/2019
ms.locfileid: "74552370"
---
# <a name="get-started-with-f-in-visual-studio-for-mac"></a>Начало работы с F# в Visual Studio для Mac

F#и визуальные F# средства поддерживаются в интегрированной среде разработки Visual Studio для Mac. Убедитесь, что [установлен Visual Studio для Mac](install-fsharp.md#install-f-with-visual-studio-for-mac).

## <a name="creating-a-console-application"></a>Создание консольного приложения

Одним из самых основных проектов в Visual Studio для Mac является консольное приложение.  Вот как это делается.  После открытия Visual Studio для Mac:

1. В меню **файл** укажите пункт **создать решение**.

2. В диалоговом окне Новый проект есть два разных шаблона для консольного приложения.  В другом > .NET, предназначенный для .NET Framework.  Другой шаблон находится в приложении .NET Core — >, предназначенном для .NET Core.  В этой статье должен работать один из шаблонов.

3. В разделе консольное приложение C# при F# необходимости измените на.  Нажмите кнопку **Далее** , чтобы перейти вперед.  

4. Присвойте проекту имя и выберите нужные параметры для приложения.  Обратите внимание, что панель предварительного просмотра находится сбоку экрана, где отображается структура каталогов, которая будет создана на основе выбранных параметров.  

5. Нажмите кнопку **Создать**.  Теперь вы увидите F# проект в Обозреватель решений.

## <a name="writing-your-code"></a>Написание кода

Приступим к работе, сначала напишем некоторый код.  Убедитесь, что файл `Program.fs` открыт, и замените его содержимое следующим:

[!code-fsharp[HelloSquare](~/samples/snippets/fsharp/getting-started/hello-square.fs)]

В предыдущем примере кода определена функция `square`, которая принимает входные данные с именем `x` и умножает ее на саму себя.  Поскольку F# использует [вывод типа](../language-reference/type-inference.md), указывать тип `x` не нужно.  F# Компилятор понимает типы, в которых умножение является допустимым, и присвоит тип `x` в зависимости от того, как вызывается `square`.  При наведении указателя мыши на `square`вы должны увидеть следующее:

```console
val square: x:int -> int
```

Это называется сигнатурой типа функции.  Его можно прочитать следующим образом: "Square — это функция, которая принимает целое число с именем" x "и создает целое число".  Обратите внимание, что компилятор выдает `square` тип `int` для Now, так как умножение не является универсальным для *всех* типов, а является универсальным по отношению к закрытому набору типов.  F# Компилятор выбрал `int` на этом этапе, но при вызове `square` с другим типом входных данных, например `float`, будет настроена сигнатура типа.

Определена другая функция `main`, которая снабжена атрибутом `EntryPoint`, чтобы сообщить F# компилятору, что должно начаться выполнение программы.  Он соответствует тому же соглашению, что и другие [языки программирования в стиле C](https://en.wikipedia.org/wiki/Entry_point#C_and_C.2B.2B), где аргументы командной строки могут передаваться в эту функцию, и возвращается целочисленный код (обычно `0`).

Эта функция вызывает функцию `square` с аргументом `12`.  Затем F# компилятор назначает тип `square` `int -> int` (то есть функция, которая принимает `int` и создает `int`).  Вызов `printfn` является отформатированной функцией печати, которая использует строку формата, аналогичную языку программирования в стиле C, параметры, соответствующие указанным в строке формата, а затем выводят результат и новую строку.

## <a name="running-your-code"></a>Выполнение кода

Можно запустить код и просмотреть результаты, щелкнув **запустить** в меню верхнего уровня, а затем **запустить без отладки**.  Это приведет к запуску программы без отладки и позволяет просмотреть результаты.

Теперь в окне консоли, которое Visual Studio для Mac выводится на экран, должны отобразиться следующие сведения:

```console
12 squared is 144!
```

Поздравляем!  Вы создали первый F# проект в Visual Studio для Mac, записали F# функцию на печать результатов вызова этой функции и запустили проект, чтобы увидеть некоторые результаты.

## <a name="using-f-interactive"></a>Использование F# интерактивного

Одной из лучших функций визуального F# инструментария в Visual Studio для Mac является F# интерактивное окно.  Он позволяет отправить код в процесс, в котором можно вызвать этот код и просмотреть результат в интерактивном режиме.

Чтобы приступить к работе, выделите функцию `square`, определенную в коде.  Затем в меню верхнего уровня щелкните **Edit (изменить** ).  Затем выберите **Отправить выделенный F# фрагмент в интерактивный**.  Это приведет к выполнению кода в F# интерактивном окне.  Кроме того, можно щелкнуть выделенный фрагмент правой кнопкой мыши и выбрать пункт **Отправить выделенное в F# интерактивное**окно.  Вы должны увидеть F# интерактивное окно, в котором отображается следующее:

```console
>

val square : x:int -> int

>
```

Здесь показана та же сигнатура функции для функции `square`, которую вы видели ранее при наведении указателя мыши на функцию.  Поскольку `square` теперь определен в F# интерактивном процессе, его можно вызвать с различными значениями:

```console
> square 12;;
val it : int = 144
>square 13;;
val it : int = 169
```

Эта функция выполняет функцию, привязывает результат к новому имени `it`и отображает тип и значение `it`.  Обратите внимание, что каждая строка должна завершаться `;;`.  Таким способом интерактивно известно о F# завершении вызова функции.  Вы также можете определить новые функции в F# интерактивном режиме:

```console
> let isOdd x = x % 2 <> 0;;

val isOdd : x:int -> bool

> isOdd 12;;
val it : bool = false
```

В приведенном выше примере определяется новая функция, `isOdd`, которая принимает `int` и проверяет, нечетна ли она!  Эту функцию можно вызвать, чтобы увидеть, что она возвращает с различными входными данными.  Функции можно вызывать внутри вызовов функций:

```console
> isOdd (square 15);;
val it : bool = true
```

Можно также использовать [оператор переадресации канала](../language-reference/symbol-and-operator-reference/index.md) для передачи значения в две функции:

```console
> 15 |> square |> isOdd;;
val it : bool = true
```

Оператор переадресации канала и многое другое рассматривается в последующих руководствах.

Это лишь краткий обзор того, что можно сделать с F# помощью интерактивного.  Дополнительные сведения см. в [интерактивном программировании F#с помощью ](../tutorials/fsharp-interactive/index.md).

## <a name="next-steps"></a>Следующие шаги

Если вы еще этого не сделали, ознакомьтесь с [обзором F# ](../tour.md), в котором рассматриваются некоторые основные функции F# языка.  Вы получите общие сведения о некоторых F#возможностях и предоставьте достаточное количество примеров кода, которые вы можете скопировать в Visual Studio для Mac и выполнить.  Есть также некоторые отличные внешние ресурсы, которые можно использовать, выдемонстрируемые в этом [ F# руководством](../index.yml).

## <a name="see-also"></a>См. также:

- [F#программ](../index.yml)
- [Обзор языка F#](../tour.md)
- [F#Справочник по языку](../language-reference/index.md)
- [Определение типа](../language-reference/type-inference.md)
- [Справочник по символам и операторам](../language-reference/symbol-and-operator-reference/index.md)
