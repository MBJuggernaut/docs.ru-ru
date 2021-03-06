---
title: Поддержка SqlClient LocalDB
ms.date: 03/30/2017
ms.assetid: cf796898-5575-46f2-ae6e-21e5aa8c4123
ms.openlocfilehash: 841c455605b0b32668d26cab16a6207dc1c0f716
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/24/2020
ms.locfileid: "91203427"
---
# <a name="sqlclient-support-for-localdb"></a>Поддержка SqlClient LocalDB

Начиная с названия кода Denali в SQL Server, будет доступна облегченная версия SQL Server, называемая LocalDB. В этом разделе обсуждаются способы подключения к базе данных в LocalDB.  
  
## <a name="remarks"></a>Remarks  

 Дополнительные сведения о LocalDB, включая способы его установки и настройки, см. в электронной документации на SQL Server.  
  
 Чтобы получить сводные сведения о возможностях работы с LocalDB, выполните следующие действия.  
  
- Создайте и запустите экземпляры LocalDB с помощью sqllocaldb.exe или файла app.config.  
  
- Для добавления и изменения баз данных в локальном экземпляре LocalDB можно воспользоваться программой sqlcmd.exe. Например, `sqlcmd -S (localdb)\myinst`.  
  
- Используйте ключевое слово строки подключения `AttachDBFilename`, чтобы добавить базу данных в экземпляр LocalDB. Если при использовании `AttachDBFilename` не указано имя базы данных в ключевом слове строки подключения `Database`, то база данных будет удалена из экземпляра LocalDB при закрытии приложения.  
  
- Чтобы указать экземпляр LocalDB в строке подключения, выполните указанные ниже действия. Например, у вас есть экземпляр с именем `myInstance`, строка подключения будет включать:  
  
    `server=(localdb)\\myInstance`  
  
 `User Instance=True` не допускается при подключении к базе данных LocalDB.  
  
 Базу данных LocalDB можно скачать из [пакета дополнительных компонентов Microsoft SQL Server 2012](https://www.microsoft.com/download/en/details.aspx?id=29065). Если необходимо изменение данных в экземпляре LocalDB с помощью программы sqlcmd.exe, то необходимо пользоваться версией sqlcmd из SQL Server 2012. Эту программу можно также получить из пакета дополнительных компонентов SQL Server 2012.  
  
## <a name="programmatically-create-a-named-instance"></a>Создание именованного экземпляра программным путем  

 Приложение может создать именованный экземпляр и указать базу данных, как показано ниже.  
  
- Укажите экземпляры LocalDB, чтобы добавить в файл app.config сведения, как показано ниже.  Номер версии экземпляра должен совпадать с номером версии установки LocalDB.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <configSections>  
        <section  
        name="system.data.localdb"  
        type="System.Data.LocalDBConfigurationSection,System.Data,Version=4.0.0.0,Culture=neutral,PublicKeyToken=b77a5c561934e089"/>  
      </configSections>  
      <system.data.localdb>  
        <localdbinstances>  
          <add name="myInstance" version="11.0" />  
        </localdbinstances>  
      </system.data.localdb>  
    </configuration>  
    ```  
  
- Укажите имя экземпляра с помощью ключевого слова строки подключения `server`.  Имя экземпляра, указанное в ключевом слове строки подключения `server`, должно соответствовать имени, указанному в файле app.config.  
  
- Используйте ключевое слово строки подключения `AttachDBFilename`, чтобы указать MDF-файл.  
  
## <a name="see-also"></a>См. также раздел

- [SQL Server функций и ADO.NET](sql-server-features-and-adonet.md)
- [Общие сведения об ADO.NET](../ado-net-overview.md)
