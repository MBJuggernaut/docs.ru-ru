---
title: Интерфейс ICorProfilerCallback4
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback4
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback4
helpviewer_keywords:
- ICorProfilerCallback4 interface [.NET Framework profiling]
ms.assetid: 665f3cfc-cd6f-4880-906c-ea65ad384783
topic_type:
- apiref
ms.openlocfilehash: 295d3d440529623f4569fd6c5f4debe7e4558990
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499445"
---
# <a name="icorprofilercallback4-interface"></a>Интерфейс ICorProfilerCallback4
Предоставляет методы обратного вызова, используемые средой CLR для передачи информации в профилировщик.  
  
## <a name="methods"></a>Методы  
  
|Метод|Описание|  
|------------|-----------------|  
|[Метод GetReJITParameters](icorprofilercallback4-getrejitparameters-method.md)|Позволяет профилировщику кода устанавливать альтернативные флаги создания кода для нового текста перекомпилированного метода.|  
|[Метод MovedReferences2](icorprofilercallback4-movedreferences2-method.md)|Сообщает о новом макете объектов в куче в результате сборки мусора для сжатия.|  
|[Метод ReJITCompilationFinished](icorprofilercallback4-rejitcompilationfinished-method.md)|Уведомляет профилировщик о том, что JIT-компилятор завершил повторную компиляцию функции.|  
|[Метод ReJITCompilationStarted](icorprofilercallback4-rejitcompilationstarted-method.md)|Уведомляет профилировщик о том, что JIT-компилятор начал перекомпилировать функцию.|  
|[Метод ReJITError](icorprofilercallback4-rejiterror-method.md)|Сообщает об ошибке, возникшей при обработке запроса на перекомпиляцию.|  
|[Метод SurvivingReferences2](icorprofilercallback4-survivingreferences2-method.md)|Предоставляет информацию о структуре объектов в куче в результате сборки мусора без сжатия.|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="requirements"></a>Требования  
 **Платформы:** см. раздел [Требования к системе](../../get-started/system-requirements.md).  
  
 **Заголовок:** CorProf.idl, CorProf.h  
  
 **Библиотека:** CorGuids.lib  
  
 **.NET Framework версии:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Интерфейс ICorProfilerCallback2](icorprofilercallback2-interface.md)
- [Профилирующие интерфейсы](profiling-interfaces.md)
- [Интерфейс ICorProfilerInfo](icorprofilerinfo-interface.md)
