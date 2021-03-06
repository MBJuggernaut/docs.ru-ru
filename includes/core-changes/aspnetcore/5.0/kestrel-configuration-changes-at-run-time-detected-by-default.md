---
ms.openlocfilehash: d00b8ecaa61b358e062d85a2b68ca8a95cada442
ms.sourcegitcommit: 1eae045421d9ea2bfc82aaccfa5b1ff1b8c9e0e4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/16/2020
ms.locfileid: "84803239"
---
### <a name="kestrel-configuration-changes-at-run-time-detected-by-default"></a>Kestrel. Обнаружение изменений конфигурации во время выполнения включено по умолчанию

Kestrel теперь реагирует на изменения, внесенные в раздел `Kestrel` экземпляра `IConfiguration` проекта (например, *appsettings.json*) во время выполнения. Дополнительные сведения о настройке Kestrel с помощью *appsettings.json* см. в примере *appsettings.json* в [конфигурации конечной точки](/aspnet/core/fundamentals/servers/kestrel#endpoint-configuration).

Kestrel привязывает, отменяет привязку и повторно привязывает конечные точки при необходимости для реагирования на соответствующие изменения в конфигурации.

Обсуждение этого вопроса см. на странице [dotnet/aspnetcore#22807](https://github.com/dotnet/aspnetcore/issues/22807).

#### <a name="version-introduced"></a>Представленная версия

5.0 (предварительная версия 7)

#### <a name="old-behavior"></a>Старое поведение

До ASP.NET Core 5.0 (предварительная версия 6) Kestrel не поддерживал изменение конфигурации во время выполнения.

В ASP.NET Core 5.0 (предварительная версия 6) можно было выбрать поведение по умолчанию для действий, выполняемых в настоящее время, для реагирования на изменения в конфигурации во время выполнения. Включение в конфигурацию требуемой привязки Kestrel вручную:

```csharp
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Hosting;

public class Program
{
    public static void Main(string[] args) =>
        CreateHostBuilder(args).Build().Run();

    public static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureWebHostDefaults(webBuilder =>
            {
                webBuilder.UseKestrel((builderContext, kestrelOptions) =>
                {
                    kestrelOptions.Configure(
                        builderContext.Configuration.GetSection("Kestrel"), reloadOnChange: true);
                });

                webBuilder.UseStartup<Startup>();
            });
}
```

#### <a name="new-behavior"></a>Новое поведение

По умолчанию Kestrel реагирует на изменения конфигурации во время выполнения. Для поддержки этого изменения <xref:Microsoft.Extensions.Hosting.GenericHostBuilderExtensions.ConfigureWebHostDefaults%2A> по умолчанию вызывает `KestrelServerOptions.Configure(IConfiguration, bool)` с `reloadOnChange: true`.

#### <a name="reason-for-change"></a>Причина изменения

Было внесено изменение для поддержки перенастройки конечной точки во время выполнения без полного перезапуска сервера. В отличие от полного перезапуска сервера, привязка неизмененных конечных точек не отменяется даже временно.

#### <a name="recommended-action"></a>Рекомендованное действие

* В большинстве сценариев, в которых раздел конфигурации Kestrel по умолчанию не изменяется во время выполнения, это изменение не оказывает влияния и никаких действий не требуется.
* Для сценариев, в которых раздел конфигурации Kestrel по умолчанию изменяется во время выполнения и Kestrel должен реагировать на него, это поведение по умолчанию.
* Для сценариев, в которых раздел конфигурации Kestrel по умолчанию изменяется во время выполнения и Kestrel не должен реагировать на него, можно отказаться от приведенных ниже действий.

    ```csharp
    using Microsoft.AspNetCore.Hosting;
    using Microsoft.Extensions.Hosting;

    public class Program
    {
        public static void Main(string[] args) =>
            CreateHostBuilder(args).Build().Run();

        public static IHostBuilder CreateHostBuilder(string[] args) =>
            Host.CreateDefaultBuilder(args)
                .ConfigureWebHostDefaults(webBuilder =>
                {
                    webBuilder.UseKestrel((builderContext, kestrelOptions) =>
                    {
                        kestrelOptions.Configure(
                            builderContext.Configuration.GetSection("Kestrel"), reloadOnChange: false);
                    });

                    webBuilder.UseStartup<Startup>();
                });
    }
    ```

**Примечания.**

Это изменение не изменяет поведение перегрузки `KestrelServerOptions.Configure(IConfiguration)`, которое по умолчанию по-прежнему `reloadOnChange: false`.

Также важно убедиться, что источник конфигурации поддерживает перезагрузку. Для источников JSON перезагрузка настраивается путем вызова `AddJsonFile(path, reloadOnChange: true)`. Для *appsettings.json* и *appsettings.{Environment}.json* повторная загрузка уже настроена по умолчанию.

#### <a name="category"></a>Категория

ASP.NET Core

#### <a name="affected-apis"></a>Затронутые API

<xref:Microsoft.Extensions.Hosting.GenericHostBuilderExtensions.ConfigureWebHostDefaults%2A?displayProperty=nameWithType>

<!-- 

#### Affected APIs

`Overload:Microsoft.Extensions.Hosting.GenericHostBuilderExtensions.ConfigureWebHostDefaults`

-->
