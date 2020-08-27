---
title: Набор данных и руководство по безопасности DataTable
ms.date: 07/14/2020
dev_langs:
- csharp
ms.openlocfilehash: 24c8a830f8638bc2d9dd20c2384c8230a682d817
ms.sourcegitcommit: 9c45035b781caebc63ec8ecf912dc83fb6723b1f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/25/2020
ms.locfileid: "88812241"
---
# <a name="dataset-and-datatable-security-guidance"></a><span data-ttu-id="23af8-102">Набор данных и руководство по безопасности DataTable</span><span class="sxs-lookup"><span data-stu-id="23af8-102">DataSet and DataTable security guidance</span></span>

<span data-ttu-id="23af8-103">Эта статья относится к следующим продуктам:</span><span class="sxs-lookup"><span data-stu-id="23af8-103">This article applies to:</span></span>

* <span data-ttu-id="23af8-104">.NET Framework (все версии)</span><span class="sxs-lookup"><span data-stu-id="23af8-104">.NET Framework (all versions)</span></span>
* <span data-ttu-id="23af8-105">.NET Core и более поздние версии</span><span class="sxs-lookup"><span data-stu-id="23af8-105">.NET Core and later</span></span>
* <span data-ttu-id="23af8-106">.NET 5.0 и более поздней версии</span><span class="sxs-lookup"><span data-stu-id="23af8-106">.NET 5.0 and later</span></span>

<span data-ttu-id="23af8-107">Типы [DataSet](/dotnet/api/system.data.dataset) и [DataTable](/dotnet/api/system.data.datatable) являются устаревшими компонентами .NET, которые позволяют представлять наборы данных как управляемые объекты.</span><span class="sxs-lookup"><span data-stu-id="23af8-107">The [DataSet](/dotnet/api/system.data.dataset) and [DataTable](/dotnet/api/system.data.datatable) types are legacy .NET components that allow representing data sets as managed objects.</span></span> <span data-ttu-id="23af8-108">Эти компоненты появились в .NET 1,0 как часть исходной [инфраструктуры ADO.NET](/dotnet/framework/data/adonet/dataset-datatable-dataview/).</span><span class="sxs-lookup"><span data-stu-id="23af8-108">These components were introduced in .NET 1.0 as part of the original [ADO.NET infrastructure](/dotnet/framework/data/adonet/dataset-datatable-dataview/).</span></span> <span data-ttu-id="23af8-109">Их цель — предоставить управляемое представление по реляционному набору данных, чтобы отказаться от того, является ли базовый источник данных XML, SQL или другой технологией.</span><span class="sxs-lookup"><span data-stu-id="23af8-109">Their goal was to provide a managed view over a relational data set, abstracting away whether the underlying source of the data was XML, SQL, or another technology.</span></span>

<span data-ttu-id="23af8-110">Дополнительные сведения о ADO.NET, включая более современные парадигмы представления данных, см. [в документации по ADO.NET](/dotnet/framework/data/adonet/).</span><span class="sxs-lookup"><span data-stu-id="23af8-110">For more information on ADO.NET, including more modern data view paradigms, see [the ADO.NET documentation](/dotnet/framework/data/adonet/).</span></span>

## <a name="default-restrictions-when-deserializing-a-dataset-or-datatable-from-xml"></a><span data-ttu-id="23af8-111">Ограничения по умолчанию при десериализации набора данных или DataTable из XML</span><span class="sxs-lookup"><span data-stu-id="23af8-111">Default restrictions when deserializing a DataSet or DataTable from XML</span></span>

<span data-ttu-id="23af8-112">Во всех поддерживаемых версиях .NET Framework, .NET Core и .NET, а также `DataSet` `DataTable` накладываются следующие ограничения на типы объектов, которые могут присутствовать в десериализованных данных.</span><span class="sxs-lookup"><span data-stu-id="23af8-112">On all supported versions of .NET Framework, .NET Core, and .NET, `DataSet` and `DataTable` place the following restrictions on what types of objects may be present in the deserialized data.</span></span> <span data-ttu-id="23af8-113">По умолчанию этот список ограничен:</span><span class="sxs-lookup"><span data-stu-id="23af8-113">By default, this list is restricted to:</span></span>

* <span data-ttu-id="23af8-114">Примитивы и примитивные эквиваленты: `bool` , `char` , `sbyte` , `byte` , `short` , `ushort` , `int` , `uint` ,,, `long` `ulong` `float` `double` `decimal` `DateTime` `DateTimeOffset` `TimeSpan` `string` `Guid` `SqlBinary` `SqlBoolean` `SqlByte` `SqlBytes` `SqlChars` `SqlDateTime` `SqlDecimal` `SqlDouble` `SqlGuid` `SqlInt16` `SqlInt32` `SqlInt64` `SqlMoney` `SqlSingle` `SqlString` ,,,,,,,,,,,,,,,,,,,,,, и.</span><span class="sxs-lookup"><span data-stu-id="23af8-114">Primitives and primitive equivalents: `bool`, `char`, `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `float`, `double`, `decimal`, `DateTime`, `DateTimeOffset`, `TimeSpan`, `string`, `Guid`, `SqlBinary`, `SqlBoolean`, `SqlByte`, `SqlBytes`, `SqlChars`, `SqlDateTime`, `SqlDecimal`, `SqlDouble`, `SqlGuid`, `SqlInt16`, `SqlInt32`, `SqlInt64`, `SqlMoney`, `SqlSingle`, and `SqlString`.</span></span>
* <span data-ttu-id="23af8-115">Часто используемые не примитивы: `Type` , `Uri` и `BigInteger` .</span><span class="sxs-lookup"><span data-stu-id="23af8-115">Commonly used non-primitives: `Type`, `Uri`, and `BigInteger`.</span></span>
* <span data-ttu-id="23af8-116">Часто используемые типы _System. Drawing_ : `Color` , `Point` , `PointF` , `Rectangle` , `RectangleF` , `Size` и `SizeF` .</span><span class="sxs-lookup"><span data-stu-id="23af8-116">Commonly used _System.Drawing_ types: `Color`, `Point`, `PointF`, `Rectangle`, `RectangleF`, `Size`, and `SizeF`.</span></span>
* <span data-ttu-id="23af8-117">`Enum` типов.</span><span class="sxs-lookup"><span data-stu-id="23af8-117">`Enum` types.</span></span>
* <span data-ttu-id="23af8-118">Массивы и списки приведенных выше типов.</span><span class="sxs-lookup"><span data-stu-id="23af8-118">Arrays and lists of the above types.</span></span>

<span data-ttu-id="23af8-119">Если входящие XML-данные содержат объект, тип которого отсутствует в этом списке:</span><span class="sxs-lookup"><span data-stu-id="23af8-119">If the incoming XML data contains an object whose type is not in this list:</span></span>

* <span data-ttu-id="23af8-120">Исключение создается со следующим сообщением и трассировкой стека.</span><span class="sxs-lookup"><span data-stu-id="23af8-120">An exception is thrown with the following message and stack trace.</span></span>  
<span data-ttu-id="23af8-121">Сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="23af8-121">Error Message:</span></span>  
<span data-ttu-id="23af8-122">System. InvalidOperationException: тип " \<Type Name\> , версия = \<n.n.n.n\> , Culture = \<culture\> , PublicKeyToken = \<token value\> " не допускается здесь.</span><span class="sxs-lookup"><span data-stu-id="23af8-122">System.InvalidOperationException : Type '\<Type Name\>, Version=\<n.n.n.n\>, Culture=\<culture\>, PublicKeyToken=\<token value\>' is not allowed here.</span></span> <span data-ttu-id="23af8-123">[https://go.microsoft.com/fwlink/?linkid=2132227](https://go.microsoft.com/fwlink/?linkid=2132227)Дополнительные сведения см. в разделе.</span><span class="sxs-lookup"><span data-stu-id="23af8-123">See [https://go.microsoft.com/fwlink/?linkid=2132227](https://go.microsoft.com/fwlink/?linkid=2132227) for more details.</span></span>  
<span data-ttu-id="23af8-124">Трассировка стека:</span><span class="sxs-lookup"><span data-stu-id="23af8-124">Stack Trace:</span></span>  
<span data-ttu-id="23af8-125">в System. Data. Типелимитер. Енсуретипеисалловед (тип Type, Типелимитер Каптуредлимитер)</span><span class="sxs-lookup"><span data-stu-id="23af8-125">at System.Data.TypeLimiter.EnsureTypeIsAllowed(Type type, TypeLimiter capturedLimiter)</span></span>  
<span data-ttu-id="23af8-126">в System. Data. DataColumn. Упдатеколумнтипе (тип Type, StorageType typeCode)</span><span class="sxs-lookup"><span data-stu-id="23af8-126">at System.Data.DataColumn.UpdateColumnType(Type type, StorageType typeCode)</span></span>  
<span data-ttu-id="23af8-127">в System. Data. DataColumn. set_DataType (значение типа)</span><span class="sxs-lookup"><span data-stu-id="23af8-127">at System.Data.DataColumn.set_DataType(Type value)</span></span>  

* <span data-ttu-id="23af8-128">Операция десериализации завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="23af8-128">The deserialization operation fails.</span></span>

<span data-ttu-id="23af8-129">При загрузке XML в существующий `DataSet` экземпляр или `DataTable` можно учитывать существующие определения столбцов.</span><span class="sxs-lookup"><span data-stu-id="23af8-129">When loading XML into an existing `DataSet` or `DataTable` instance, the existing column definitions are also taken into account.</span></span> <span data-ttu-id="23af8-130">Если таблица уже содержит определение столбца пользовательского типа, этот тип временно добавляется в список разрешений на время выполнения операции десериализации XML.</span><span class="sxs-lookup"><span data-stu-id="23af8-130">If the table already contains a column definition of a custom type, that type is temporarily added to the allow list for the duration of the XML deserialization operation.</span></span>

```cs
XmlReader xmlReader = GetXmlReader();

// Assume the XML blob contains data for type MyCustomClass.
// The following call to ReadXml fails because MyCustomClass isn't in the allowed types list.

DataTable table = new DataTable("MyDataTable");
table.ReadXml(xmlReader);

// However, the following call to ReadXml succeeds, since the DataTable instance
// already defines a column of type MyCustomClass.

DataTable table = new DataTable("MyDataTable");
table.Columns.Add("MyColumn", typeof(MyCustomClass));
table.ReadXml(xmlReader); // this call will succeed
```

<span data-ttu-id="23af8-131">Ограничения типа объекта также применяются при использовании `XmlSerializer` для десериализации экземпляра `DataSet` или `DataTable` .</span><span class="sxs-lookup"><span data-stu-id="23af8-131">The object type restrictions also apply when using `XmlSerializer` to deserialize an instance of `DataSet` or `DataTable`.</span></span> <span data-ttu-id="23af8-132">Однако они могут не применяться при использовании `BinaryFormatter` для десериализации экземпляра `DataSet` или `DataTable` .</span><span class="sxs-lookup"><span data-stu-id="23af8-132">However, they may not apply when using `BinaryFormatter` to deserialize an instance of `DataSet` or `DataTable`.</span></span>

<span data-ttu-id="23af8-133">Ограничения типа объекта не применяются при использовании `DataAdapter.Fill` , например при `DataTable` заполнении экземпляра непосредственно из базы данных без использования API-интерфейсов десериализации XML.</span><span class="sxs-lookup"><span data-stu-id="23af8-133">The object type restrictions don't apply when using `DataAdapter.Fill`, such as when a `DataTable` instance is populated directly from a database without using the XML deserialization APIs.</span></span>

### <a name="extend-the-list-of-allowed-types"></a><span data-ttu-id="23af8-134">Расширение списка разрешенных типов</span><span class="sxs-lookup"><span data-stu-id="23af8-134">Extend the list of allowed types</span></span>

<span data-ttu-id="23af8-135">Приложение может расширить список разрешенных типов, включив в него пользовательские типы, а также встроенные типы, перечисленные выше.</span><span class="sxs-lookup"><span data-stu-id="23af8-135">An app can extend the allowed types list to include custom types in addition to the built-in types listed above.</span></span> <span data-ttu-id="23af8-136">При расширении списка разрешенных типов изменение затрагивает _все_ `DataSet` `DataTable` экземпляры приложения и в нем.</span><span class="sxs-lookup"><span data-stu-id="23af8-136">If extending the allowed types list, the change affects _all_ `DataSet` and `DataTable` instances within the app.</span></span> <span data-ttu-id="23af8-137">Невозможно удалить типы из списка разрешенных типов.</span><span class="sxs-lookup"><span data-stu-id="23af8-137">Types cannot be removed from the built-in allowed types list.</span></span>

#### <a name="extend-through-configuration-net-framework-40---48"></a><span data-ttu-id="23af8-138">Расширение через конфигурацию (.NET Framework 4,0-4,8)</span><span class="sxs-lookup"><span data-stu-id="23af8-138">Extend through configuration (.NET Framework 4.0 - 4.8)</span></span>

<span data-ttu-id="23af8-139">_App.config_ можно использовать для расширения списка разрешенных типов.</span><span class="sxs-lookup"><span data-stu-id="23af8-139">_App.config_ can be used to extend the allowed types list.</span></span> <span data-ttu-id="23af8-140">Чтобы расширить список разрешенных типов, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="23af8-140">To extend the allowed types list:</span></span>

* <span data-ttu-id="23af8-141">Используйте `<configSections>` элемент, чтобы добавить ссылку на раздел конфигурации _System. Data_ .</span><span class="sxs-lookup"><span data-stu-id="23af8-141">Use the `<configSections>` element to add a reference to the _System.Data_ configuration section.</span></span>
* <span data-ttu-id="23af8-142">Используйте `<system.data.dataset.serialization>` / `<allowedTypes>` для указания дополнительных типов.</span><span class="sxs-lookup"><span data-stu-id="23af8-142">Use `<system.data.dataset.serialization>`/`<allowedTypes>` to specify additional types.</span></span>

<span data-ttu-id="23af8-143">Каждый `<add>` элемент должен указывать только один тип, используя полное имя типа сборки.</span><span class="sxs-lookup"><span data-stu-id="23af8-143">Each `<add>` element must specify only one type by using its assembly qualified type name.</span></span> <span data-ttu-id="23af8-144">Чтобы добавить дополнительные типы в список разрешенных типов, используйте несколько `<add>` элементов.</span><span class="sxs-lookup"><span data-stu-id="23af8-144">To add additional types to the allowed types list, use multiple `<add>` elements.</span></span>

<span data-ttu-id="23af8-145">В следующем примере показано расширение списка разрешенных типов путем добавления пользовательского типа `Fabrikam.CustomType` .</span><span class="sxs-lookup"><span data-stu-id="23af8-145">The following sample shows extending the allowed types list by adding the custom type `Fabrikam.CustomType`.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <sectionGroup name="system.data.dataset.serialization" type="System.Data.SerializationSettingsSectionGroup, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">
      <section name="allowedTypes" type="System.Data.AllowedTypesSectionHandler, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"/>
    </sectionGroup>
  </configSections>
  <system.data.dataset.serialization>
    <allowedTypes>
      <!-- <add type="assembly qualified type name" /> -->
      <add type="Fabrikam.CustomType, Fabrikam, Version=1.0.0.0, Culture=neutral, PublicKeyToken=2b3831f2f2b744f7" />
      <!-- additional <add /> elements as needed -->
    </allowedTypes>
  </system.data.dataset.serialization>
</configuration>
```

<span data-ttu-id="23af8-146">Чтобы получить полное имя сборки типа, используйте свойство [Type. AssemblyQualifiedName](/dotnet/api/system.type.assemblyqualifiedname) , как показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="23af8-146">To retrieve the assembly qualified name of a type, use the [Type.AssemblyQualifiedName](/dotnet/api/system.type.assemblyqualifiedname) property, as demonstrated in the following code.</span></span>

```cs
string assemblyQualifiedName = typeof(Fabrikam.CustomType).AssemblyQualifiedName;
```

<a name="etc"></a>

#### <a name="extend-through-configuration-net-framework-20---35"></a><span data-ttu-id="23af8-147">Расширение через конфигурацию (.NET Framework 2,0-3,5)</span><span class="sxs-lookup"><span data-stu-id="23af8-147">Extend through configuration (.NET Framework 2.0 - 3.5)</span></span>

<span data-ttu-id="23af8-148">Если приложение предназначено для .NET Framework 2,0 или 3,5, вы по-прежнему можете использовать описанный выше механизм _App.config_ для расширения списка разрешенных типов.</span><span class="sxs-lookup"><span data-stu-id="23af8-148">If your app targets .NET Framework 2.0 or 3.5, you can still use the above _App.config_ mechanism to extend the allowed types list.</span></span> <span data-ttu-id="23af8-149">Однако `<configSections>` элемент будет выглядеть немного иначе, как показано в следующем коде:</span><span class="sxs-lookup"><span data-stu-id="23af8-149">However, your `<configSections>` element will look slightly different, as shown in the following code:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <!-- The below <sectionGroup> and <section> are specific to .NET Framework 2.0 and 3.5. -->
    <sectionGroup name="system.data.dataset.serialization" type="System.Data.SerializationSettingsSectionGroup, System.Data, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">
      <section name="allowedTypes" type="System.Data.AllowedTypesSectionHandler, System.Data, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"/>
    </sectionGroup>
  </configSections>
  <system.data.dataset.serialization>
    <allowedTypes>
      <!-- <add /> elements, as demonstrated in the .NET Framework 4.0 - 4.8 sample code above. -->
    </allowedTypes>
  </system.data.dataset.serialization>
</configuration>
```

#### <a name="extend-programmatically-net-framework-net-core-net-50"></a><span data-ttu-id="23af8-150">Расширение программным способом (.NET Framework, .NET Core, .NET 5.0 +)</span><span class="sxs-lookup"><span data-stu-id="23af8-150">Extend programmatically (.NET Framework, .NET Core, .NET 5.0+)</span></span>

<span data-ttu-id="23af8-151">Список разрешенных типов также можно расширить программно с помощью [AppDomain. SetData](/dotnet/api/system.appdomain.setdata) с хорошо известным ключом _System. Data. датасетдефаулталловедтипес_, как показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="23af8-151">The list of allowed types can also be extended programmatically by using [AppDomain.SetData](/dotnet/api/system.appdomain.setdata) with the well-known key _System.Data.DataSetDefaultAllowedTypes_, as shown in the following code.</span></span>

```cs
Type[] extraAllowedTypes = new Type[]
{
    typeof(Fabrikam.CustomType),
    typeof(Contoso.AdditionalCustomType)
};

AppDomain.CurrentDomain.SetData("System.Data.DataSetDefaultAllowedTypes", extraAllowedTypes);
```

<span data-ttu-id="23af8-152">При использовании механизма расширения значение, связанное с ключом _System. Data. датасетдефаулталловедтипес_ , должно иметь тип `Type[]` .</span><span class="sxs-lookup"><span data-stu-id="23af8-152">If using the extension mechanism, the value associated with the key _System.Data.DataSetDefaultAllowedTypes_ must be of type `Type[]`.</span></span>

<span data-ttu-id="23af8-153">В .NET Framework список разрешенных типов можно расширить с помощью _App.config_ и `AppDomain.SetData` .</span><span class="sxs-lookup"><span data-stu-id="23af8-153">On .NET Framework, the list of allowed types may be extended both with _App.config_ and `AppDomain.SetData`.</span></span> <span data-ttu-id="23af8-154">В этом случае `DataSet` и `DataTable` позволяет десериализовать объект как часть данных, если его тип имеется в любом из списков.</span><span class="sxs-lookup"><span data-stu-id="23af8-154">In this case, `DataSet` and `DataTable` will allow an object to be deserialized as part of the data if its type is present in either list.</span></span>

### <a name="run-an-app-in-audit-mode-net-framework"></a><span data-ttu-id="23af8-155">Запуск приложения в режиме аудита (.NET Framework)</span><span class="sxs-lookup"><span data-stu-id="23af8-155">Run an app in audit mode (.NET Framework)</span></span>

<span data-ttu-id="23af8-156">В .NET Framework `DataSet` и `DataTable` Предоставьте возможность режима аудита.</span><span class="sxs-lookup"><span data-stu-id="23af8-156">In .NET Framework, `DataSet` and `DataTable` provide an audit mode capability.</span></span> <span data-ttu-id="23af8-157">Если включен режим аудита `DataSet` и `DataTable` Сравнение типов входящих объектов со списком разрешенных типов.</span><span class="sxs-lookup"><span data-stu-id="23af8-157">When audit mode is enabled, `DataSet` and `DataTable` compare the types of incoming objects against the allowed types list.</span></span> <span data-ttu-id="23af8-158">Однако если объект, тип которого не разрешен, отображается, исключение **не** создается.</span><span class="sxs-lookup"><span data-stu-id="23af8-158">However, if an object whose type is not allowed is seen, an exception is **not** thrown.</span></span> <span data-ttu-id="23af8-159">Вместо этого `DataSet` и `DataTable` уведомлять все подключенные `TraceListener` экземпляры о наличии подозрительного типа, позволяя `TraceListener` записывать эти сведения в журнал.</span><span class="sxs-lookup"><span data-stu-id="23af8-159">Instead, `DataSet` and `DataTable` notify any attached `TraceListener` instances that a suspicious type is present, allowing the `TraceListener` to log this information.</span></span> <span data-ttu-id="23af8-160">Исключение не создается, и Операция десериализации сохраняется.</span><span class="sxs-lookup"><span data-stu-id="23af8-160">No exception is thrown and the deserialization operation continues.</span></span>

> [!WARNING]
> <span data-ttu-id="23af8-161">Запуск приложения в режиме аудита должен быть только временной мерой, используемой для тестирования.</span><span class="sxs-lookup"><span data-stu-id="23af8-161">Running an app in "audit mode" should only be a temporary measure used for testing.</span></span> <span data-ttu-id="23af8-162">Если включен режим аудита `DataSet` и `DataTable` не применяются ограничения типа, что может вызвать брешь в системе безопасности в приложении.</span><span class="sxs-lookup"><span data-stu-id="23af8-162">When audit mode is enabled, `DataSet` and `DataTable` do not enforce type restrictions, which can introduce a security hole inside your app.</span></span> <span data-ttu-id="23af8-163">Дополнительные сведения см. в разделах [Удаление всех ограничений на типы](#ratr) и [безопасность с учетом ненадежных входных данных](#swr).</span><span class="sxs-lookup"><span data-stu-id="23af8-163">For more information, see the sections titled [Removing all type restrictions](#ratr) and [Safety with regard to untrusted input](#swr).</span></span>

<span data-ttu-id="23af8-164">Режим аудита можно включить с помощью _App.config_:</span><span class="sxs-lookup"><span data-stu-id="23af8-164">Audit mode can be enabled through _App.config_:</span></span>

* <span data-ttu-id="23af8-165">Сведения о правильном значении для размещения элемента см. в разделе [расширение конфигурации](#etc) в этом документе `<configSections>` .</span><span class="sxs-lookup"><span data-stu-id="23af8-165">See the [Extending through configuration](#etc) section in this document for information on the proper value to put for the `<configSections>` element.</span></span>
* <span data-ttu-id="23af8-166">Используйте `<allowedTypes auditOnly="true">` для включения режима аудита, как показано в следующей разметке.</span><span class="sxs-lookup"><span data-stu-id="23af8-166">Use `<allowedTypes auditOnly="true">` to enable audit mode, as shown in the following markup.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <!-- See the section of this document titled "Extending through configuration" for the appropriate
         <sectionGroup> and <section> elements to put here, depending on whether you're running .NET
         Framework 2.0 - 3.5 or 4.0 - 4.8. -->
  </configSections>
  <system.data.dataset.serialization>
    <allowedTypes auditOnly="true"> <!-- setting auditOnly="true" enables audit mode -->
      <!-- Optional <add /> elements as needed. -->
    </allowedTypes>
  </system.data.dataset.serialization>
</configuration>
```

<span data-ttu-id="23af8-167">После включения режима аудита можно использовать _App.config_ , чтобы подключиться к `TraceListener` `DataSet` встроенному `TraceSource.` источнику трассировки по имени _System. Data. DataSet_.</span><span class="sxs-lookup"><span data-stu-id="23af8-167">Once audit mode is enabled, you can use _App.config_ to connect your preferred `TraceListener` to the `DataSet` built-in `TraceSource.` The name of the built-in trace source is _System.Data.DataSet_.</span></span> <span data-ttu-id="23af8-168">В следующем примере демонстрируется запись событий трассировки в консоль _и_ в файл журнала на диске.</span><span class="sxs-lookup"><span data-stu-id="23af8-168">The following sample demonstrates writing trace events to the console _and_ to a log file on disk.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.diagnostics>
    <sources>
      <source name="System.Data.DataSet"
              switchType="System.Diagnostics.SourceSwitch"
              switchValue="Warning">
        <listeners>
          <!-- write to the console -->
          <add name="console"
               type="System.Diagnostics.ConsoleTraceListener" />
          <!-- *and* write to a log file on disk -->
          <add name="filelog"
               type="System.Diagnostics.TextWriterTraceListener"
               initializeData="c:\logs\mylog.txt" />
        </listeners>
      </source>
    </sources>
  </system.diagnostics>
</configuration>
```

<span data-ttu-id="23af8-169">Дополнительные сведения о `TraceSource` и см `TraceListener` . в документе [практические руководства. использование TraceSource и фильтров с прослушивателями трассировки](../../../debug-trace-profile/how-to-use-tracesource-and-filters-with-trace-listeners.md).</span><span class="sxs-lookup"><span data-stu-id="23af8-169">For more information on `TraceSource` and `TraceListener`, see the document [How to: Use TraceSource and Filters with Trace Listeners](../../../debug-trace-profile/how-to-use-tracesource-and-filters-with-trace-listeners.md).</span></span>

> [!NOTE]
> <span data-ttu-id="23af8-170">Запуск приложения в режиме аудита недоступен в .NET Core или .NET 5,0 и более поздних версиях.</span><span class="sxs-lookup"><span data-stu-id="23af8-170">Running an app in audit mode is not available in .NET Core or in .NET 5.0 and later.</span></span>

<a name="ratr"></a>

### <a name="remove-all-type-restrictions"></a><span data-ttu-id="23af8-171">Удалить все ограничения типа</span><span class="sxs-lookup"><span data-stu-id="23af8-171">Remove all type restrictions</span></span>

<span data-ttu-id="23af8-172">Если приложение должно удалить все ограничения, ограничивающие тип `DataSet` , в и `DataTable` :</span><span class="sxs-lookup"><span data-stu-id="23af8-172">If an app must remove all type limiting restrictions from `DataSet` and `DataTable`:</span></span>

* <span data-ttu-id="23af8-173">Существует несколько вариантов отключения ограничений типа.</span><span class="sxs-lookup"><span data-stu-id="23af8-173">There are several options to suppress type limiting restrictions.</span></span>
* <span data-ttu-id="23af8-174">Доступные параметры зависят от платформы, для которой предназначено приложение.</span><span class="sxs-lookup"><span data-stu-id="23af8-174">The options available depend on the framework the app targets.</span></span>

> [!WARNING]
> <span data-ttu-id="23af8-175">Удаление всех ограничений типа может вызвать брешь в системе безопасности внутри приложения.</span><span class="sxs-lookup"><span data-stu-id="23af8-175">Removing all type restrictions can introduce a security hole inside the app.</span></span> <span data-ttu-id="23af8-176">При использовании этого механизма убедитесь, что приложение не **использует** `DataSet` или `DataTable` для чтения недоверенных входных данных.</span><span class="sxs-lookup"><span data-stu-id="23af8-176">When using this mechanism, ensure the app does **not** use `DataSet` or `DataTable` to read untrusted input.</span></span> <span data-ttu-id="23af8-177">Дополнительные сведения см. в статье [CVE-2020-1147](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2020-1147) и следующем разделе [безопасность с учетом ненадежных входов](#swr).</span><span class="sxs-lookup"><span data-stu-id="23af8-177">For more information, see [CVE-2020-1147](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2020-1147) and the following section titled [Safety with regard to untrusted input](#swr).</span></span>

#### <a name="through-appcontext-configuration-net-framework-46---48-net-core-21-and-later-net-50-and-later"></a><span data-ttu-id="23af8-178">Через AppContext Configuration (.NET Framework 4,6-4,8, .NET Core 2,1 и более поздних версий, .NET 5,0 и более поздние версии)</span><span class="sxs-lookup"><span data-stu-id="23af8-178">Through AppContext configuration (.NET Framework 4.6 - 4.8, .NET Core 2.1 and later, .NET 5.0 and later)</span></span>

<span data-ttu-id="23af8-179">`AppContext`Параметр, `Switch.System.Data.AllowArbitraryDataSetTypeInstantiation` при установке которого `true` удаляет все ограничения, ограничивающие типы `DataSet` , от и `DataTable` .</span><span class="sxs-lookup"><span data-stu-id="23af8-179">The `AppContext` switch, `Switch.System.Data.AllowArbitraryDataSetTypeInstantiation`, when set to `true` removes all type limiting restrictions from `DataSet` and `DataTable`.</span></span>

<span data-ttu-id="23af8-180">В .NET Framework этот коммутатор можно включить с помощью _App.config_, как показано в следующей конфигурации:</span><span class="sxs-lookup"><span data-stu-id="23af8-180">In .NET Framework, this switch can be enabled via _App.config_, as shown in the following configuration:</span></span>

```xml
<configuration>
   <runtime>
      <!-- Warning: setting the following switch can introduce a security problem. -->
      <AppContextSwitchOverrides value="Switch.System.Data.AllowArbitraryDataSetTypeInstantiation=true" />
   </runtime>
</configuration>
```

<span data-ttu-id="23af8-181">В ASP.NET `<AppContextSwitchOverrides>` элемент недоступен.</span><span class="sxs-lookup"><span data-stu-id="23af8-181">In ASP.NET, the `<AppContextSwitchOverrides>` element is not available.</span></span> <span data-ttu-id="23af8-182">Вместо этого коммутатор можно включить с помощью _Web.config_, как показано в следующей конфигурации:</span><span class="sxs-lookup"><span data-stu-id="23af8-182">Instead, the switch can be enabled via _Web.config_, as shown in the following configuration:</span></span>

```xml
<configuration>
    <appSettings>
        <!-- Warning: setting the following switch can introduce a security problem. -->
        <add key="AppContext.SetSwitch:Switch.System.Data.AllowArbitraryDataSetTypeInstantiation" value="true" />
    </appSettings>
</configuration>
```

<span data-ttu-id="23af8-183">Дополнительные сведения см. в описании [\<AppContextSwitchOverrides>](../../../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) элемента.</span><span class="sxs-lookup"><span data-stu-id="23af8-183">For more information, see the [\<AppContextSwitchOverrides>](../../../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) element.</span></span>

<span data-ttu-id="23af8-184">В .NET Core, .NET 5 и ASP.NET Core этот параметр управляется _runtimeconfig.jsв_, как показано в следующем примере JSON:</span><span class="sxs-lookup"><span data-stu-id="23af8-184">In .NET Core, .NET 5, and ASP.NET Core, this setting is controlled by _runtimeconfig.json_, as shown in the following JSON:</span></span>

```json
{
  "runtimeOptions": {
    "configProperties": {
      "Switch.System.Data.AllowArbitraryDataSetTypeInstantiation": true
    }
  }
}
```

<span data-ttu-id="23af8-185">Дополнительные сведения см. в разделе ["параметры конфигурации среды выполнения .NET Core"](/dotnet/core/run-time-config/).</span><span class="sxs-lookup"><span data-stu-id="23af8-185">For more information, see [".NET Core run-time configuration settings"](/dotnet/core/run-time-config/).</span></span>

<span data-ttu-id="23af8-186">`AllowArbitraryDataSetTypeInstantiation` также можно задать программно с помощью [AppContext. сетсвитч](/dotnet/api/system.appcontext.setswitch) вместо файла конфигурации, как показано в следующем коде:</span><span class="sxs-lookup"><span data-stu-id="23af8-186">`AllowArbitraryDataSetTypeInstantiation` can also be set programmatically via [AppContext.SetSwitch](/dotnet/api/system.appcontext.setswitch) instead of using a configuration file, as shown in the following code:</span></span>

```cs
// Warning: setting the following switch can introduce a security problem.
AppContext.SetSwitch("Switch.System.Data.AllowArbitraryDataSetTypeInstantiation", true);
```

 <span data-ttu-id="23af8-187">При выборе предыдущего программного подхода вызов метода `AppContext.SetSwitch` должен выполняться на раннем этапе запуска приложений.</span><span class="sxs-lookup"><span data-stu-id="23af8-187">If you choose the preceding programmatic approach, the call to `AppContext.SetSwitch` should occur early in the apps startup.</span></span>

#### <a name="through-the-machine-wide-registry-net-framework-20---48"></a><span data-ttu-id="23af8-188">Через реестр на уровне компьютера (.NET Framework 2,0-4,8);</span><span class="sxs-lookup"><span data-stu-id="23af8-188">Through the machine-wide registry (.NET Framework 2.0 - 4.8)</span></span>

<span data-ttu-id="23af8-189">Если параметр `AppContext` недоступен, проверка ограничений типов может быть отключена с помощью реестра Windows:</span><span class="sxs-lookup"><span data-stu-id="23af8-189">If `AppContext` is not available, type limiting checks can be disabled with the Windows registry:</span></span>

* <span data-ttu-id="23af8-190">Администратор должен настроить реестр.</span><span class="sxs-lookup"><span data-stu-id="23af8-190">An administrator must configure the registry.</span></span>
* <span data-ttu-id="23af8-191">Использование реестра является изменением на уровне компьютера и влияет на _все_ приложения, выполняющиеся на компьютере.</span><span class="sxs-lookup"><span data-stu-id="23af8-191">Using the registry is a machine-wide change and will affect _all_ apps running on the machine.</span></span>

| <span data-ttu-id="23af8-192">Тип</span><span class="sxs-lookup"><span data-stu-id="23af8-192">Type</span></span>  |  <span data-ttu-id="23af8-193">Значение</span><span class="sxs-lookup"><span data-stu-id="23af8-193">Value</span></span> |
|---|---|
| <span data-ttu-id="23af8-194">**Раздел реестра**</span><span class="sxs-lookup"><span data-stu-id="23af8-194">**Registry key**</span></span> | `HKLM\SOFTWARE\Microsoft\.NETFramework\AppContext` |
| <span data-ttu-id="23af8-195">**Имя значения**</span><span class="sxs-lookup"><span data-stu-id="23af8-195">**Value name**</span></span> | `Switch.System.Data.AllowArbitraryDataSetTypeInstantiation` |
| <span data-ttu-id="23af8-196">**Тип значения**</span><span class="sxs-lookup"><span data-stu-id="23af8-196">**Value type**</span></span> | `REG_SZ` |
| <span data-ttu-id="23af8-197">**Данные**</span><span class="sxs-lookup"><span data-stu-id="23af8-197">**Value data**</span></span> | `true` |

<span data-ttu-id="23af8-198">В 64-разрядной операционной системе это значение необходимо добавить как для 64-разрядного ключа (показанного выше), так и для ключа 32-bit.</span><span class="sxs-lookup"><span data-stu-id="23af8-198">On a 64-bit operating system, this value my need to be added for both the 64-bit key (shown above) and the 32-bit key.</span></span> <span data-ttu-id="23af8-199">32-разрядный ключ находится в папке `HKLM\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\AppContext` .</span><span class="sxs-lookup"><span data-stu-id="23af8-199">The 32-bit key is located at `HKLM\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\AppContext`.</span></span>

<span data-ttu-id="23af8-200">Дополнительные сведения об использовании реестра для настройки `AppContext` см. в разделе [«AppContext для потребителей библиотек»](/dotnet/api/system.appcontext#appcontext-for-library-consumers).</span><span class="sxs-lookup"><span data-stu-id="23af8-200">For more information on using the registry to configure `AppContext`, see ["AppContext for library consumers"](/dotnet/api/system.appcontext#appcontext-for-library-consumers).</span></span>

<a name="swr"></a>

## <a name="safety-with-regard-to-untrusted-input"></a><span data-ttu-id="23af8-201">Безопасность в отношении ненадежных входных данных</span><span class="sxs-lookup"><span data-stu-id="23af8-201">Safety with regard to untrusted input</span></span>

<span data-ttu-id="23af8-202">Хотя `DataSet` и `DataTable` накладывают ограничения по умолчанию на типы, которые могут присутствовать при ДЕСЕРИАЛИЗАЦИИ XML-полезных данных, __ `DataSet` и `DataTable` в общем случае ненадежны при заполнении недоверенными входными данными.__</span><span class="sxs-lookup"><span data-stu-id="23af8-202">While `DataSet` and `DataTable` do impose default limitations on the types that are allowed to be present while deserializing XML payloads, __`DataSet` and `DataTable` are in general not safe when populated with untrusted input.__</span></span> <span data-ttu-id="23af8-203">Ниже приведен неисчерпывающий список способов, с помощью которых `DataSet` `DataTable` экземпляр или может считывать ненадежные входные данные.</span><span class="sxs-lookup"><span data-stu-id="23af8-203">The following is a non-exhaustive list of ways that a `DataSet` or `DataTable` instance might read untrusted input.</span></span>

* <span data-ttu-id="23af8-204">Объект `DataAdapter` ссылается на базу данных, а `DataAdapter.Fill` метод используется для заполнения `DataSet` с помощью содержимого запроса к базе данных.</span><span class="sxs-lookup"><span data-stu-id="23af8-204">A `DataAdapter` references a database, and the `DataAdapter.Fill` method is used to populate a `DataSet` with the contents of a database query.</span></span>
* <span data-ttu-id="23af8-205">`DataSet.ReadXml`Метод или `DataTable.ReadXml` используется для чтения XML-файла, содержащего сведения о столбцах и строках.</span><span class="sxs-lookup"><span data-stu-id="23af8-205">The `DataSet.ReadXml` or `DataTable.ReadXml` method is used to read an XML file containing column and row information.</span></span>
* <span data-ttu-id="23af8-206">`DataSet`Экземпляр или `DataTable` сериализуется как часть ASP.NET (SOAP) веб-служб или КОНЕЧНОЙ точки WCF.</span><span class="sxs-lookup"><span data-stu-id="23af8-206">A `DataSet` or `DataTable` instance is serialized as part of a ASP.NET (SOAP) web services or WCF endpoint.</span></span>
* <span data-ttu-id="23af8-207">Сериализатор, такой как `XmlSerializer` , используется для десериализации `DataSet` `DataTable` экземпляра или из потока XML.</span><span class="sxs-lookup"><span data-stu-id="23af8-207">A serializer such as `XmlSerializer` is used to deserialize a `DataSet` or `DataTable` instance from an XML stream.</span></span>
* <span data-ttu-id="23af8-208">Сериализатор, такой как `JsonConvert` , используется для десериализации `DataSet` `DataTable` экземпляра или из потока JSON.</span><span class="sxs-lookup"><span data-stu-id="23af8-208">A serializer such as `JsonConvert` is used to deserialize a `DataSet` or `DataTable` instance from a JSON stream.</span></span> <span data-ttu-id="23af8-209">`JsonConvert` — Это метод в популярном [Newtonsoft.Jsе](https://www.newtonsoft.com/json) стороннего производителя для библиотеки.</span><span class="sxs-lookup"><span data-stu-id="23af8-209">`JsonConvert` is a method in the popular third-party [Newtonsoft.Json](https://www.newtonsoft.com/json) library.</span></span>
* <span data-ttu-id="23af8-210">Сериализатор, такой как `BinaryFormatter` , используется для десериализации `DataSet` `DataTable` экземпляра или из потока необработанных байтов.</span><span class="sxs-lookup"><span data-stu-id="23af8-210">A serializer such as `BinaryFormatter` is used to deserialize a `DataSet` or `DataTable` instance from a raw byte stream.</span></span>

<span data-ttu-id="23af8-211">В этом документе обсуждаются вопросы безопасности в предыдущих сценариях.</span><span class="sxs-lookup"><span data-stu-id="23af8-211">This document discusses safety considerations for the preceding scenarios.</span></span>

## <a name="use-dataadapterfill-to-populate-a-dataset-from-an-untrusted-data-source"></a><span data-ttu-id="23af8-212">Использование `DataAdapter.Fill` для заполнения `DataSet` из ненадежного источника данных</span><span class="sxs-lookup"><span data-stu-id="23af8-212">Use `DataAdapter.Fill` to populate a `DataSet` from an untrusted data source</span></span>

<span data-ttu-id="23af8-213">`DataSet`Экземпляр можно заполнить с помощью `DataAdapter` [ `DataAdapter.Fill` метода](/dotnet/api/system.data.common.dataadapter.fill), как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="23af8-213">A `DataSet` instance can be populated from a `DataAdapter` by using [the `DataAdapter.Fill` method](/dotnet/api/system.data.common.dataadapter.fill), as shown in the following example.</span></span>

```cs
// Assumes that connection is a valid SqlConnection object.  
string queryString =
  "SELECT CustomerID, CompanyName FROM dbo.Customers";  
SqlDataAdapter adapter = new SqlDataAdapter(queryString, connection);  
  
DataSet customers = new DataSet();  
adapter.Fill(customers, "Customers");
```

<span data-ttu-id="23af8-214">(Приведенный выше пример кода является частью более крупного примера, найденного при [заполнении набора данных из DataAdapter](../populating-a-dataset-from-a-dataadapter.md).)</span><span class="sxs-lookup"><span data-stu-id="23af8-214">(The code sample above is part of a larger sample found at [Populating a DataSet from a DataAdapter](../populating-a-dataset-from-a-dataadapter.md).)</span></span>

> <span data-ttu-id="23af8-215">Большинство приложений могут упростить и предположить, что их уровень базы данных является доверенным.</span><span class="sxs-lookup"><span data-stu-id="23af8-215">Most apps can simplify and assume that their database layer is trusted.</span></span> <span data-ttu-id="23af8-216">Тем не менее, если вы в привычке [моделирования угроз](https://www.microsoft.com/securityengineering/sdl/threatmodeling) для приложений, модель угроз может считать, что между приложением (клиентом) и уровнем базы данных (сервер) есть граница доверия.</span><span class="sxs-lookup"><span data-stu-id="23af8-216">However, if you are in the habit of [threat modeling](https://www.microsoft.com/securityengineering/sdl/threatmodeling) your apps, your threat model may consider there to be a trust boundary between the application (client) and database layer (server).</span></span> <span data-ttu-id="23af8-217">Использование [взаимной проверки подлинности](/sql/relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections) или [проверки подлинности AAD](/azure/azure-sql/database/authentication-aad-overview) между клиентом и сервером является одним из способов помочь в устранении рисков, связанных с этим.</span><span class="sxs-lookup"><span data-stu-id="23af8-217">Using [mutual authentication](/sql/relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections) or [AAD authentication](/azure/azure-sql/database/authentication-aad-overview) between client and server is one way to help address the risks associated with this.</span></span> <span data-ttu-id="23af8-218">Оставшаяся часть этого раздела посвящена возможному результату подключения клиента к серверу, который не является доверенным.</span><span class="sxs-lookup"><span data-stu-id="23af8-218">The remainder of this section discusses the possible result of a client connecting to an untrusted server.</span></span>

<span data-ttu-id="23af8-219">Последствия, указывающие на `DataAdapter` ненадежный источник данных, зависят от реализации `DataAdapter` самого себя.</span><span class="sxs-lookup"><span data-stu-id="23af8-219">The consequences of pointing a `DataAdapter` at an untrusted data source depend on the implementation of the `DataAdapter` itself.</span></span>

### <a name="sqldataadapter"></a><span data-ttu-id="23af8-220">SqlDataAdapter;</span><span class="sxs-lookup"><span data-stu-id="23af8-220">SqlDataAdapter</span></span>

<span data-ttu-id="23af8-221">Для встроенного типа [SqlDataAdapter](/dotnet/api/microsoft.data.sqlclient.sqldataadapter)ссылка на ненадежный источник данных может привести к атаке типа "отказ в обслуживании" (DOS).</span><span class="sxs-lookup"><span data-stu-id="23af8-221">For the built-in type [SqlDataAdapter](/dotnet/api/microsoft.data.sqlclient.sqldataadapter), referencing an untrusted data source could result in a denial of service (DoS) attack.</span></span> <span data-ttu-id="23af8-222">Атака с помощью DoS может привести к тому, что приложение перестанет отвечать или аварийно завершить работу.</span><span class="sxs-lookup"><span data-stu-id="23af8-222">The DoS attack could result in the app becoming unresponsive or crashing.</span></span> <span data-ttu-id="23af8-223">Если злоумышленник может разместить библиотеку DLL вместе с приложением, он также может обеспечить возможность выполнения локального кода.</span><span class="sxs-lookup"><span data-stu-id="23af8-223">If an attacker can plant a DLL alongside the app, they may also be able to achieve local code execution.</span></span>

### <a name="other-dataadapter-types"></a><span data-ttu-id="23af8-224">Другие типы DataAdapter</span><span class="sxs-lookup"><span data-stu-id="23af8-224">Other DataAdapter types</span></span>

<span data-ttu-id="23af8-225">Сторонние `DataAdapter` реализации должны самостоятельно выполнять оценку того, какие гарантии безопасности они предоставляют в ненадежных входных данных.</span><span class="sxs-lookup"><span data-stu-id="23af8-225">Third-party `DataAdapter` implementations must make their own assessments about what security guarantees they provide in the face of untrusted inputs.</span></span> <span data-ttu-id="23af8-226">.NET не может предоставлять гарантии безопасности в отношении этих реализаций.</span><span class="sxs-lookup"><span data-stu-id="23af8-226">.NET cannot make any safety guarantees regarding these implementations.</span></span>

<a name="dsrdtr"></a>

## <a name="datasetreadxml-and-datatablereadxml"></a><span data-ttu-id="23af8-227">DataSet. ReadXml и DataTable. ReadXml</span><span class="sxs-lookup"><span data-stu-id="23af8-227">DataSet.ReadXml and DataTable.ReadXml</span></span>

<span data-ttu-id="23af8-228">`DataSet.ReadXml`Методы и `DataTable.ReadXml` не являются надежными при использовании с ненадежными входными данными.</span><span class="sxs-lookup"><span data-stu-id="23af8-228">The `DataSet.ReadXml` and `DataTable.ReadXml` methods are not safe when used with untrusted input.</span></span> <span data-ttu-id="23af8-229">Мы настоятельно рекомендуем пользователям использовать один из вариантов, описанных далее в этом документе.</span><span class="sxs-lookup"><span data-stu-id="23af8-229">We strongly recommend that consumers instead consider using one of the alternatives outlined later in this document.</span></span>

<span data-ttu-id="23af8-230">Реализации `DataSet.ReadXml` и `DataTable.ReadXml` изначально были созданы до того, как уязвимые места сериализации были хорошо понятными категориями угроз.</span><span class="sxs-lookup"><span data-stu-id="23af8-230">The implementations of `DataSet.ReadXml` and `DataTable.ReadXml` were originally created before serialization vulnerabilities were a well-understood threat category.</span></span> <span data-ttu-id="23af8-231">В результате код не соответствует текущим рекомендациям по обеспечению безопасности.</span><span class="sxs-lookup"><span data-stu-id="23af8-231">As a result, the code does not follow current security best practices.</span></span> <span data-ttu-id="23af8-232">Эти API-интерфейсы можно использовать в качестве векторов, чтобы злоумышленники могли совершать атаки через DoS в отношении приложений.</span><span class="sxs-lookup"><span data-stu-id="23af8-232">These APIs can be used as vectors for attackers to perform DoS attacks against web apps.</span></span> <span data-ttu-id="23af8-233">Эти атаки могут привести к невозможности отклика веб-службы или вызвать непредвиденное завершение процесса.</span><span class="sxs-lookup"><span data-stu-id="23af8-233">These attacks might render the web service unresponsive or result in unexpected process termination.</span></span> <span data-ttu-id="23af8-234">Платформа не обеспечивает устранение рисков для этих категорий атак, и .NET считает это поведение «по разработке».</span><span class="sxs-lookup"><span data-stu-id="23af8-234">The framework does not provide mitigations for these attack categories and .NET considers this behavior "by design".</span></span>

<span data-ttu-id="23af8-235">.NET выпускает обновления для системы безопасности, чтобы устранить некоторые проблемы, такие как раскрытие информации или удаленное выполнение кода в `DataSet.ReadXml` и `DataTable.ReadXml` .</span><span class="sxs-lookup"><span data-stu-id="23af8-235">.NET has released security updates to mitigate some issues such as information disclosure or remote code execution in `DataSet.ReadXml` and `DataTable.ReadXml`.</span></span> <span data-ttu-id="23af8-236">Обновления для системы безопасности .NET могут не обеспечивать полную защиту от этих категорий угроз.</span><span class="sxs-lookup"><span data-stu-id="23af8-236">The .NET security updates may not provide complete protection against these threat categories.</span></span> <span data-ttu-id="23af8-237">Мы рекомендуем всем потребителям проанализировать особенности конкретных сценариев применения и оценить их уязвимость в отношении этих рисков.</span><span class="sxs-lookup"><span data-stu-id="23af8-237">Consumers should assess their individual scenarios and consider their potential exposure to these risks.</span></span>

<span data-ttu-id="23af8-238">Потребители должны учитывать, что обновления безопасности этих API могут повлиять на совместимость приложений в некоторых ситуациях.</span><span class="sxs-lookup"><span data-stu-id="23af8-238">Consumers should be aware that security updates to these APIs may impact application compatibility in some situations.</span></span> <span data-ttu-id="23af8-239">Кроме того, существует вероятность того, что в этих API будет обнаружена романская уязвимость, для которой .NET не может фактически публиковать обновление для системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="23af8-239">Furthermore, the possibility exists that a novel vulnerability in these APIs will be discovered for which .NET can't practically publish a security update.</span></span>

<span data-ttu-id="23af8-240">Рекомендуется, чтобы потребители этих API были:</span><span class="sxs-lookup"><span data-stu-id="23af8-240">We recommend that consumers of these APIs either:</span></span>

* <span data-ttu-id="23af8-241">Попробуйте использовать один из вариантов, описанных далее в этом документе.</span><span class="sxs-lookup"><span data-stu-id="23af8-241">Consider using one of the alternatives outlined later in this document.</span></span>
* <span data-ttu-id="23af8-242">Выполните оценку отдельных рисков для своих приложений.</span><span class="sxs-lookup"><span data-stu-id="23af8-242">Perform individual risk assessments on their apps.</span></span>

<span data-ttu-id="23af8-243">Это единственная обязанность потребителя, позволяющая определить, следует ли использовать эти API.</span><span class="sxs-lookup"><span data-stu-id="23af8-243">It is the consumer's sole responsibility to determine whether to utilize these APIs.</span></span> <span data-ttu-id="23af8-244">Потребители должны оценивать любые вопросы безопасности, технические и юридические риски, включая нормативные требования, которые могут сопровождаться использованием этих API.</span><span class="sxs-lookup"><span data-stu-id="23af8-244">Consumers should assess any security, technical, and legal risks, including regulatory requirements, that may accompany using these APIs.</span></span>

## <a name="dataset-and-datatable-via-aspnet-web-services-or-wcf"></a><span data-ttu-id="23af8-245">DataSet и DataTable через веб-службы ASP.NET или WCF</span><span class="sxs-lookup"><span data-stu-id="23af8-245">DataSet and DataTable via ASP.NET web services or WCF</span></span>

<span data-ttu-id="23af8-246">Можно принять `DataSet` или `DataTable` экземпляр в веб-службе ASP.NET (SOAP), как показано в следующем коде:</span><span class="sxs-lookup"><span data-stu-id="23af8-246">It is possible to accept a `DataSet` or a `DataTable` instance in an ASP.NET (SOAP) web service, as demonstrated in the following code:</span></span>

```cs
using System.Data;
using System.Web.Services;

[WebService(Namespace = "http://contoso.com/")]
public class MyService : WebService
{
    [WebMethod]
    public string MyWebMethod(DataTable dataTable)
    {
        /* Web method implementation. */
    }
}
```

<span data-ttu-id="23af8-247">Вариация в этом случае не принимает `DataSet` или не `DataTable` напрямую в качестве параметра, а принимает его как часть общего сериализованного графа объектов SOAP, как показано в следующем коде:</span><span class="sxs-lookup"><span data-stu-id="23af8-247">A variation on this is not to accept `DataSet` or `DataTable` directly as a parameter, but instead to accept it as part of the overall SOAP serialized object graph, as shown in the following code:</span></span>

```cs
using System.Data;
using System.Web.Services;

[WebService(Namespace = "http://contoso.com/")]
public class MyService : WebService
{
    [WebMethod]
    public string MyWebMethod(MyClass data)
    {
        /* Web method implementation. */
    }
}

public class MyClass
{
    // Property of type DataTable, automatically serialized and
    // deserialized as part of the overall MyClass payload.
    public DataTable MyDataTable { get; set; }
}
```

<span data-ttu-id="23af8-248">Или используйте WCF вместо веб-служб ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="23af8-248">Or, using WCF instead of ASP.NET web services:</span></span>

```cs
using System.Data;
using System.ServiceModel;

[ServiceContract(Namespace = "http://contoso.com/")]
public interface IMyContract
{
    [OperationContract]
    string MyMethod(DataTable dataTable);
    [OperationContract]
    string MyOtherMethod(MyClass data);
}

public class MyClass
{
    // Property of type DataTable, automatically serialized and
    // deserialized as part of the overall MyClass payload.
    public DataTable MyDataTable { get; set; }
}
```

<span data-ttu-id="23af8-249">Во всех этих случаях модель угроз и гарантии безопасности аналогичны [разделам DataSet. ReadXml и DataTable. ReadXml](#dsrdtr).</span><span class="sxs-lookup"><span data-stu-id="23af8-249">In all of these cases, the threat model and security guarantees are the same as the [DataSet.ReadXml and DataTable.ReadXml section](#dsrdtr).</span></span>

## <a name="deserialize-a-dataset-or-datatable-via-xmlserializer"></a><span data-ttu-id="23af8-250">Десериализация набора данных или DataTable через XmlSerializer</span><span class="sxs-lookup"><span data-stu-id="23af8-250">Deserialize a DataSet or DataTable via XmlSerializer</span></span>

<span data-ttu-id="23af8-251">Разработчики могут использовать `XmlSerializer` для десериализации `DataSet` и `DataTable` экземпляров, как показано в следующем коде:</span><span class="sxs-lookup"><span data-stu-id="23af8-251">Developers can use `XmlSerializer` to deserialize `DataSet` and `DataTable` instances, as shown in the following code:</span></span>

```cs
using System.Data;
using System.IO;
using System.Xml.Serialization;

public DataSet PerformDeserialization1(Stream stream) {
    XmlSerializer serializer = new XmlSerializer(typeof(DataSet));
    return (DataSet)serializer.Deserialize(stream);
}

public MyClass PerformDeserialization2(Stream stream) {
    XmlSerializer serializer = new XmlSerializer(typeof(MyClass));
    return (MyClass)serializer.Deserialize(stream);
}

public class MyClass
{
    // Property of type DataTable, automatically serialized and
    // deserialized as part of the overall MyClass payload.
    public DataTable MyDataTable { get; set; }
}
```

<span data-ttu-id="23af8-252">В таких случаях модель угроз и гарантии безопасности совпадают с [разделом DataSet. ReadXml и DataTable. ReadXml.](#dsrdtr)</span><span class="sxs-lookup"><span data-stu-id="23af8-252">In these cases, the threat model and security guarantees are the same as the [DataSet.ReadXml and DataTable.ReadXml section](#dsrdtr)</span></span>

## <a name="deserialize-a-dataset-or-datatable-via-jsonconvert"></a><span data-ttu-id="23af8-253">Десериализация набора данных или DataTable через JsonConvert</span><span class="sxs-lookup"><span data-stu-id="23af8-253">Deserialize a DataSet or DataTable via JsonConvert</span></span>

<span data-ttu-id="23af8-254">Популярную библиотеку [JSON.NET](https://www.newtonsoft.com/json) сторонних производителей Newtonsoft можно использовать для десериализации `DataSet` и `DataTable` экземпляров, как показано в следующем коде:</span><span class="sxs-lookup"><span data-stu-id="23af8-254">The popular third-party Newtonsoft library [JSON.NET](https://www.newtonsoft.com/json) can be used to deserialize `DataSet` and `DataTable` instances, as shown in the following code:</span></span>

```cs
using System.Data;
using Newtonsoft.Json;

public DataSet PerformDeserialization1(string json) {
    return JsonConvert.DeserializeObect<DataSet>(data);
}

public MyClass PerformDeserialization2(string json) {
    return JsonConvert.DeserializeObect<MyClass>(data);
}

public class MyClass
{
    // Property of type DataTable, automatically serialized and
    // deserialized as part of the overall MyClass payload.
    public DataTable MyDataTable { get; set; }
}
```

<span data-ttu-id="23af8-255">Десериализация `DataSet` или `DataTable` таким образом из ненадежного BLOB-объекта JSON небезопасно.</span><span class="sxs-lookup"><span data-stu-id="23af8-255">Deserializing a `DataSet` or `DataTable` in this manner from an untrusted JSON blob is not safe.</span></span> <span data-ttu-id="23af8-256">Этот шаблон уязвим для атак типа "отказ в обслуживании".</span><span class="sxs-lookup"><span data-stu-id="23af8-256">This pattern is vulnerable to a denial of service attack.</span></span> <span data-ttu-id="23af8-257">Такая атака может привести к сбою приложения или отрисовывать его, не реагируя на запросы.</span><span class="sxs-lookup"><span data-stu-id="23af8-257">Such an attack could crash the app or render it unresponsive.</span></span>

> [!NOTE]
> <span data-ttu-id="23af8-258">Корпорация Майкрософт не гарантирует или не поддерживает реализацию сторонних библиотек, таких как _Newtonsoft.Js_.</span><span class="sxs-lookup"><span data-stu-id="23af8-258">Microsoft does not warrant or support the implementation of third-party libraries like _Newtonsoft.Json_.</span></span> <span data-ttu-id="23af8-259">Эти сведения предоставляются для полноты и являются точными на момент написания этой статьи.</span><span class="sxs-lookup"><span data-stu-id="23af8-259">This information is provided for completeness and is accurate as of the time of this writing.</span></span>

## <a name="deserialize-a-dataset-or-datatable-via-binaryformatter"></a><span data-ttu-id="23af8-260">Десериализация набора данных или DataTable через BinaryFormatter</span><span class="sxs-lookup"><span data-stu-id="23af8-260">Deserialize a DataSet or DataTable via BinaryFormatter</span></span>

<span data-ttu-id="23af8-261">Разработчики никогда не должны использовать `BinaryFormatter` , `NetDataContractSerializer` , `SoapFormatter` или связанные ***ненадежные*** модули форматирования для десериализации `DataSet` `DataTable` экземпляра или из ненадежных полезных данных:</span><span class="sxs-lookup"><span data-stu-id="23af8-261">Developers must never use `BinaryFormatter`, `NetDataContractSerializer`, `SoapFormatter`, or related ***unsafe*** formatters to deserialize a `DataSet` or `DataTable` instance from an untrusted payload:</span></span>

* <span data-ttu-id="23af8-262">Это является уязвимым для полной атаки удаленного выполнения кода.</span><span class="sxs-lookup"><span data-stu-id="23af8-262">This is susceptible to a full remote code execution attack.</span></span>
* <span data-ttu-id="23af8-263">Использование пользовательской функции недостаточно `SerializationBinder` для предотвращения такой атаки.</span><span class="sxs-lookup"><span data-stu-id="23af8-263">Using a custom `SerializationBinder` is not sufficient to prevent such an attack.</span></span>

## <a name="safe-replacements"></a><span data-ttu-id="23af8-264">Защищенные замены</span><span class="sxs-lookup"><span data-stu-id="23af8-264">Safe replacements</span></span>

<span data-ttu-id="23af8-265">Для приложений, которые:</span><span class="sxs-lookup"><span data-stu-id="23af8-265">For apps that either:</span></span>

* <span data-ttu-id="23af8-266">Принимают или променяйте `DataSet` `DataTable` конечную точку SOAP. asmx или конечную точку WCF.</span><span class="sxs-lookup"><span data-stu-id="23af8-266">Accept `DataSet` or `DataTable` through an .asmx SOAP endpoint or a WCF endpoint.</span></span>
* <span data-ttu-id="23af8-267">Десериализация непроверенных данных в экземпляр `DataSet` или `DataTable` .</span><span class="sxs-lookup"><span data-stu-id="23af8-267">Deserialize untrusted data into an instance of `DataSet` or `DataTable`.</span></span>

<span data-ttu-id="23af8-268">Рассмотрите возможность замены объектной модели для использования [Entity Framework](/ef).</span><span class="sxs-lookup"><span data-stu-id="23af8-268">Consider replacing the object model to use [Entity Framework](/ef).</span></span> <span data-ttu-id="23af8-269">Entity Framework:</span><span class="sxs-lookup"><span data-stu-id="23af8-269">Entity Framework:</span></span>

* <span data-ttu-id="23af8-270">— Это полнофункциональная, современная, объектно-ориентированная платформа, которая может представлять реляционные данные.</span><span class="sxs-lookup"><span data-stu-id="23af8-270">Is a rich, modern, object-oriented framework that can represent relational data.</span></span>
* <span data-ttu-id="23af8-271">Предоставляет [обширную экосистему](/ef/core/providers/) поставщиков баз данных, облегчающих проецирование запросов к базам данных с помощью объектных моделей Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="23af8-271">Brings [a diverse ecosystem](/ef/core/providers/) of database providers to make it easy to project database queries via your Entity Framework object models.</span></span>
* <span data-ttu-id="23af8-272">Предлагает встроенные средства защиты при десериализации данных из ненадежных источников.</span><span class="sxs-lookup"><span data-stu-id="23af8-272">Offers built-in protections when deserializing data from untrusted sources.</span></span>

<span data-ttu-id="23af8-273">Для приложений, использующих `.aspx` конечные точки SOAP, рассмотрите возможность изменения этих конечных точек для использования [WCF](/dotnet/framework/wcf/).</span><span class="sxs-lookup"><span data-stu-id="23af8-273">For apps that use `.aspx` SOAP endpoints, consider changing those endpoints to use [WCF](/dotnet/framework/wcf/).</span></span> <span data-ttu-id="23af8-274">WCF — это наиболее полнофункциональная замена `.asmx` веб-служб.</span><span class="sxs-lookup"><span data-stu-id="23af8-274">WCF is a more fully featured replacement for `.asmx` web services.</span></span> <span data-ttu-id="23af8-275">Конечные точки WCF [могут быть предоставлены через SOAP](../../../wcf/feature-details/how-to-expose-a-contract-to-soap-and-web-clients.md) для совместимости с существующими вызывающими объектами.</span><span class="sxs-lookup"><span data-stu-id="23af8-275">WCF endpoints [can be exposed via SOAP](../../../wcf/feature-details/how-to-expose-a-contract-to-soap-and-web-clients.md) for compatibility with existing callers.</span></span>

## <a name="code-analyzers"></a><span data-ttu-id="23af8-276">Анализаторы кода</span><span class="sxs-lookup"><span data-stu-id="23af8-276">Code analyzers</span></span>

<span data-ttu-id="23af8-277">Правила безопасности анализатора кода, которые выполняются при компиляции исходного кода, могут помочь найти уязвимости, связанные с этой проблемой безопасности, в C# и Visual Basicном коде.</span><span class="sxs-lookup"><span data-stu-id="23af8-277">Code analyzer security rules, which run when your source code is compiled, can help to find vulnerabilities related to this security issue in C# and Visual Basic code.</span></span> <span data-ttu-id="23af8-278">Microsoft. CodeAnalysis. Фкскопанализерс — это пакет NuGet анализаторов кода, который распространяется на [NuGet.org](https://www.nuget.org/).</span><span class="sxs-lookup"><span data-stu-id="23af8-278">Microsoft.CodeAnalysis.FxCopAnalyzers is a NuGet package of code analyzers that's distributed on [nuget.org](https://www.nuget.org/).</span></span>

<span data-ttu-id="23af8-279">Обзор анализаторов кода см. в разделе [Обзор анализаторов исходного кода](https://docs.microsoft.com/visualstudio/code-quality/roslyn-analyzers-overview).</span><span class="sxs-lookup"><span data-stu-id="23af8-279">For an overview of code analyzers, see [Overview of source code analyzers](https://docs.microsoft.com/visualstudio/code-quality/roslyn-analyzers-overview).</span></span>

<span data-ttu-id="23af8-280">Включите следующие правила Microsoft. CodeAnalysis. Фкскопанализерс:</span><span class="sxs-lookup"><span data-stu-id="23af8-280">Enable the following Microsoft.CodeAnalysis.FxCopAnalyzers rules:</span></span>

- <span data-ttu-id="23af8-281">[CA2350](https://docs.microsoft.com/visualstudio/code-quality/ca2350): не используйте DataTable. ReadXml () с ненадежными данными</span><span class="sxs-lookup"><span data-stu-id="23af8-281">[CA2350](https://docs.microsoft.com/visualstudio/code-quality/ca2350): Do not use DataTable.ReadXml() with untrusted data</span></span>
- <span data-ttu-id="23af8-282">[CA2351](https://docs.microsoft.com/visualstudio/code-quality/ca2351): не используйте DataSet. ReadXml () с ненадежными данными</span><span class="sxs-lookup"><span data-stu-id="23af8-282">[CA2351](https://docs.microsoft.com/visualstudio/code-quality/ca2351): Do not use DataSet.ReadXml() with untrusted data</span></span>
- <span data-ttu-id="23af8-283">[CA2352](https://docs.microsoft.com/visualstudio/code-quality/ca2352): ненадежный набор данных или DataTable в сериализуемых типах может быть уязвим для атак удаленного выполнения кода</span><span class="sxs-lookup"><span data-stu-id="23af8-283">[CA2352](https://docs.microsoft.com/visualstudio/code-quality/ca2352): Unsafe DataSet or DataTable in serializable type can be vulnerable to remote code execution attacks</span></span>
- <span data-ttu-id="23af8-284">[CA2353](https://docs.microsoft.com/visualstudio/code-quality/ca2353): ненадежный набор данных или DataTable в типе Serializable</span><span class="sxs-lookup"><span data-stu-id="23af8-284">[CA2353](https://docs.microsoft.com/visualstudio/code-quality/ca2353): Unsafe DataSet or DataTable in serializable type</span></span>
- <span data-ttu-id="23af8-285">[CA2354](https://docs.microsoft.com/visualstudio/code-quality/ca2354): ненадежный набор данных или DataTable в графе десериализованных объектов может быть уязвим для атак удаленного выполнения кода</span><span class="sxs-lookup"><span data-stu-id="23af8-285">[CA2354](https://docs.microsoft.com/visualstudio/code-quality/ca2354): Unsafe DataSet or DataTable in deserialized object graph can be vulnerable to remote code execution attacks</span></span>
- <span data-ttu-id="23af8-286">[CA2355](https://docs.microsoft.com/visualstudio/code-quality/ca2355): обнаружен ненадежный набор данных или тип DataTable в графе несериализуемых объектов</span><span class="sxs-lookup"><span data-stu-id="23af8-286">[CA2355](https://docs.microsoft.com/visualstudio/code-quality/ca2355): Unsafe DataSet or DataTable type found in deserializable object graph</span></span>
- <span data-ttu-id="23af8-287">[CA2356](https://docs.microsoft.com/visualstudio/code-quality/ca2356): ненадежный набор данных или тип DataTable в графе веб-десериализуемых объектов</span><span class="sxs-lookup"><span data-stu-id="23af8-287">[CA2356](https://docs.microsoft.com/visualstudio/code-quality/ca2356): Unsafe DataSet or DataTable type in web deserializable object graph</span></span>
- <span data-ttu-id="23af8-288">[CA2361](https://docs.microsoft.com/visualstudio/code-quality/ca2361): Убедитесь, что автоматически сформированный класс содержит DataSet. ReadXml () не используется с ненадежными данными</span><span class="sxs-lookup"><span data-stu-id="23af8-288">[CA2361](https://docs.microsoft.com/visualstudio/code-quality/ca2361): Ensure autogenerated class containing DataSet.ReadXml() is not used with untrusted data</span></span>
- <span data-ttu-id="23af8-289">[CA2362](https://docs.microsoft.com/visualstudio/code-quality/ca2362): ненадежный набор данных или DataTable в автоматически созданном сериализуемым типе может быть уязвим для атак удаленного выполнения кода</span><span class="sxs-lookup"><span data-stu-id="23af8-289">[CA2362](https://docs.microsoft.com/visualstudio/code-quality/ca2362): Unsafe DataSet or DataTable in autogenerated serializable type can be vulnerable to remote code execution attacks</span></span>

<span data-ttu-id="23af8-290">Дополнительные сведения о настройке правил см. в статье [использование анализаторов кода](https://docs.microsoft.com/visualstudio/code-quality/use-roslyn-analyzers).</span><span class="sxs-lookup"><span data-stu-id="23af8-290">For more information about configuring rules, see [Use code analyzers](https://docs.microsoft.com/visualstudio/code-quality/use-roslyn-analyzers).</span></span>

<span data-ttu-id="23af8-291">Новые правила безопасности доступны в следующих пакетах NuGet:</span><span class="sxs-lookup"><span data-stu-id="23af8-291">The new security rules are available in the following NuGet packages:</span></span>

- <span data-ttu-id="23af8-292">Microsoft. CodeAnalysis. Фкскопанализерс 3.3.0: для Visual Studio 2019 версии 16,3 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="23af8-292">Microsoft.CodeAnalysis.FxCopAnalyzers 3.3.0: for Visual Studio 2019 version 16.3 or later</span></span>
- <span data-ttu-id="23af8-293">Microsoft. CodeAnalysis. Фкскопанализерс 2.9.11: для Visual Studio 2017 версии 15,9 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="23af8-293">Microsoft.CodeAnalysis.FxCopAnalyzers 2.9.11: for Visual Studio 2017 version 15.9 or later</span></span>