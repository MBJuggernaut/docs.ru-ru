---
title: Метод ISymUnmanagedWriter::OpenScope
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.OpenScope
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::OpenScope
helpviewer_keywords:
- OpenScope method, ISymUnmanagedWriter interface [.NET Framework debugging]
- ISymUnmanagedWriter::OpenScope method [.NET Framework debugging]
ms.assetid: dbea0644-3873-4329-90b8-624163e87467
topic_type:
- apiref
ms.openlocfilehash: 2808606be24399c9a4fe03df4c53202d31cbbe91
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501720"
---
# <a name="isymunmanagedwriteropenscope-method"></a>Метод ISymUnmanagedWriter::OpenScope
Открывает новую лексическую область видимости в текущем методе. Область становится новой текущей областью и помещается в стек областей. Области должны образовывать иерархию. Не допускается перекрытие одноуровневых элементов.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
HRESULT OpenScope(  
    [in] ULONG32 startOffset,  
    [out, retval] ULONG32* pRetVal);  
```  
  
## <a name="parameters"></a>Параметры  
 `startOffset`  
 окне Смещение первой инструкции в лексической области в байтах от начала метода.  
  
 `pRetVal`  
 заполняет Указатель на объект `ULONG32` , который получает идентификатор области.  
  
## <a name="return-value"></a>Возвращаемое значение  
 S_OK, если метод выполнен. в противном случае E_FAIL или другой код ошибки.  
  
## <a name="remarks"></a>Примечания  
 `ISymUnmanagedWriter::OpenScope`возвращает непрозрачный идентификатор области, который можно использовать с [ISymUnmanagedWriter:: сетскоперанже](isymunmanagedwriter-setscoperange-method.md) для определения начального и конечного смещения области в более позднее время. В этом случае смещения, передаваемые в `ISymUnmanagedWriter::OpenScope` и [ISymUnmanagedWriter:: CloseScope](isymunmanagedwriter-closescope-method.md) , игнорируются. Идентификаторы областей допустимы только в текущем методе.  
  
## <a name="requirements"></a>Требования  
 **Заголовок:** Корсим. idl, Корсим. h  
  
## <a name="see-also"></a>См. также

- [Интерфейс ISymUnmanagedWriter](isymunmanagedwriter-interface.md)
