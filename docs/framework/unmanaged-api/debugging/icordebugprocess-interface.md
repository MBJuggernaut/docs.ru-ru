---
title: Интерфейс ICorDebugProcess
ms.date: 03/30/2017
api_name:
- ICorDebugProcess
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess
helpviewer_keywords:
- ICorDebugProcess interface [.NET Framework debugging]
ms.assetid: be86f4b5-418a-4c5c-a67c-97148c65ed8c
topic_type:
- apiref
ms.openlocfilehash: ab48efccc88787f099a182627777db95304cdc3e
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212078"
---
# <a name="icordebugprocess-interface"></a>Интерфейс ICorDebugProcess
Представляет процесс, выполняющий управляемый код. Этот интерфейс является подклассом ICorDebugController.  
  
## <a name="methods"></a>Методы  
  
|Метод|Описание|  
|------------|-----------------|  
|[Метод ClearCurrentException](icordebugprocess-clearcurrentexception-method.md)|Очищает текущее неуправляемое исключение для данного потока.|  
|[Метод EnableLogMessages](icordebugprocess-enablelogmessages-method.md)|Включает и отключает отправку сообщений журнала отладчику.|  
|[Метод EnumerateAppDomains](icordebugprocess-enumerateappdomains-method.md)|Перечисляет все домены приложений в процессе.|  
|[Метод EnumerateObjects](icordebugprocess-enumerateobjects-method.md)|Не реализовано.|  
|[Метод GetHandle](icordebugprocess-gethandle-method.md)|Возвращает маркер процесса.|  
|[Метод GetHelperThreadID](icordebugprocess-gethelperthreadid-method.md)|Возвращает идентификатор потока операционной системы (ОС) для внутреннего вспомогательного потока отладчика.|  
|[Метод GetID](icordebugprocess-getid-method.md)|Возвращает идентификатор операционной системы (ОС) процесса.|  
|[Метод GetObject](icordebugprocess-getobject-method.md)|Не реализовано.|  
|[Метод GetThread](icordebugprocess-getthread-method.md)|Возвращает экземпляр ICorDebugThread с указанным ИДЕНТИФИКАТОРом потока ОС.|  
|[Метод GetThreadContext](icordebugprocess-getthreadcontext-method.md)|Возвращает контекст для заданного потока.|  
|[Метод IsOSSuspended](icordebugprocess-isossuspended-method.md)|Определяет, был ли поток приостановлен в результате остановки процесса отладчиком.|  
|[Метод IsTransitionStub](icordebugprocess-istransitionstub-method.md)|Определяет, находится ли адрес в заглушке, что приведет к переходу в управляемый код.|  
|[Метод ModifyLogSwitch](icordebugprocess-modifylogswitch-method.md)|Задает уровень серьезности указанного переключателя журнала.|  
|[Метод ReadMemory](icordebugprocess-readmemory-method.md)|Считывает память из процесса.|  
|[Метод SetThreadContext](icordebugprocess-setthreadcontext-method.md)|Задает контекст для заданного потока.|  
|[Метод ThreadForFiberCookie](icordebugprocess-threadforfibercookie-method.md)|Не рекомендуется.|  
|[Метод WriteMemory](icordebugprocess-writememory-method.md)|Записывает данные в область памяти в процессе.|  
  
## <a name="remarks"></a>Remarks  
  
> [!NOTE]
> Этот интерфейс не поддерживает удаленные вызовы между компьютерами или между процессами.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** см. раздел [Требования к системе](../../get-started/system-requirements.md).  
  
 **Заголовок:** CorDebug.idl, CorDebug.h  
  
 **Библиотека:** CorGuids.lib  
  
 **.NET Framework версии:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Интерфейс ICorDebug](icordebug-interface.md)
- [Интерфейсы отладки](debugging-interfaces.md)
