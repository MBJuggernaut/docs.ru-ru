---
title: XML литералы и XML свойства не поддерживаются во встроенном в ASP.NET коде
ms.date: 07/20/2015
f1_keywords:
- vbc31200
- bc31200
helpviewer_keywords:
- BC31200
ms.assetid: 053e8cba-8584-45cc-9fa0-43d122779772
ms.openlocfilehash: d96386f8495685391203826fea85efba47c44951
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163263"
---
# <a name="bc31200-xml-literals-and-xml-properties-are-not-supported-in-embedded-code-within-aspnet"></a>BC31200: XML-литералы и XML-свойства не поддерживаются в внедренном коде в ASP.NET

XML-литералы и XML-свойства не поддерживаются во внедренном коде в ASP.NET. Чтобы использовать функции XML, переместите код в код программной части.

 XML-литерал или свойство оси XML определяются внутри внедренного кода ( `<%= =>` ) в файле ASP.NET.

 **Идентификатор ошибки:** BC31200

## <a name="to-correct-this-error"></a>Исправление ошибки

- Переместите код, включающий XML-литерал или свойство оси XML, в файл кода программной части ASP.NET.

## <a name="see-also"></a>См. также

- [XML-литералы](../xml-literals/index.md)
- [Свойства оси XML](../xml-axis/index.md)
- [XML](../../programming-guide/language-features/xml/index.md)
