---
title: Критические изменения ASP.NET Core
titleSuffix: ''
description: В этой статье приведен список критических изменений в ASP.NET Core.
ms.date: 10/06/2020
author: scottaddie
ms.author: scaddie
ms.openlocfilehash: 37a366e30f7dc25a5da430de777755b8c9f6dd38
ms.sourcegitcommit: 636af37170ae75a11c4f7d1ecd770820e7dfe7bd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/07/2020
ms.locfileid: "91804950"
---
# <a name="aspnet-core-breaking-changes"></a>Критические изменения ASP.NET Core

ASP.NET Core предоставляет функции разработки веб-приложений, используемые .NET Core.

Выберите одну из следующих ссылок для критических изменений в определенной версии.

* [ASP.NET Core 5.0](#aspnet-core-50)
* [ASP.NET Core 3.1](#aspnet-core-31)
* [ASP.NET Core 3.0](#aspnet-core-30)

На этой странице описаны следующие критические изменения в ASP.NET Core версий 3.0, 3.1 и 5.0.

- [Удалены устаревшие API в областях борьбы с фальсификацией, CORS, диагностики, MVC и маршрутизации](#obsolete-antiforgery-cors-diagnostics-mvc-and-routing-apis-removed)
- [Проверка подлинности. API-интерфейсы и пакеты AzureAD.UI и AzureADB2C.UI помечены как устаревшие](#authentication-azureadui-and-azureadb2cui-apis-and-packages-marked-obsolete)
- [Проверка подлинности. Использование Google + прекращено](#authentication-google-deprecated-and-replaced)
- [Проверка подлинности. Удалено свойство HttpContext.Authentication](#authentication-httpcontextauthentication-property-removed)
- [Проверка подлинности. Заменены типы Newtonsoft.Json](#authentication-newtonsoftjson-types-replaced)
- [Проверка подлинности. Изменена подпись ExchangeCodeAsync OAuthHandler](#authentication-oauthhandler-exchangecodeasync-signature-changed)
- [Авторизация. Перегрузка AddAuthorization перемещена в другую сборку](#authorization-addauthorization-overload-moved-to-different-assembly)
- [Авторизация. IAllowAnonymous удален из AuthorizationFilterContext.Filters](#authorization-iallowanonymous-removed-from-authorizationfiltercontextfilters)
- [Авторизация. Для реализаций IAuthorizationPolicyProvider требуется новый метод](#authorization-iauthorizationpolicyprovider-implementations-require-new-method)
- [Авторизация. Для маршрутизации конечных точек используется ресурс HttpContext](#authorization-resource-in-endpoint-routing-is-httpcontext)
- [Общие сведения Пакеты интеграции Azure с префиксом Майкрософт удалены](#azure-microsoft-prefixed-azure-integration-packages-removed)
- [Методы сериализации BinaryFormatter устарели и запрещены в приложениях ASP.NET](#binaryformatter-serialization-methods-are-obsolete-and-prohibited-in-aspnet-apps)
- [Blazor. Незначащие пробелы удалены из компонентов во время компиляции](#blazor-insignificant-whitespace-trimmed-from-components-at-compile-time)
- [Blazor. Типы JSObjectReference и JSInProcessObjectReference изменены на internal](#blazor-jsobjectreference-and-jsinprocessobjectreference-types-changed-to-internal)
- [Blazor. Функция ProtectedBrowserStorage перемещена на общую платформу](#blazor-protectedbrowserstorage-feature-moved-to-shared-framework)
- [Blazor. Открытые поля только для чтения RenderTreeFrame стали свойствами](#blazor-rendertreeframe-readonly-public-fields-have-become-properties)
- [Blazor. Изменена целевая платформа для пакетов NuGet](#blazor-target-framework-of-nuget-packages-changed)
- [Blazor. Обновлен список поддерживаемых веб-браузеров](#blazor-updated-browser-support)
- [Кэширование. Удалено свойство CompactOnMemoryPressure](#caching-compactonmemorypressure-property-removed)
- [Кэширование. Microsoft.Extensions.Caching.SqlServer использует новый пакет SqlClient](#caching-microsoftextensionscachingsqlserver-uses-new-sqlclient-package)
- [Кэширование. Типы ResponseCaching pubternal теперь стали внутренними](#caching-responsecaching-pubternal-types-changed-to-internal)
- [Защита данных. DataProtection.AzureStorage использует новые API службы хранилища Azure](#data-protection-dataprotectionazurestorage-uses-new-azure-storage-apis)
- [Расширения. Изменения ссылок на пакеты, затрагивающие некоторые пакеты NuGet](#extensions-package-reference-changes-affecting-some-nuget-packages)
- [Размещение. Модуль AspNetCoreModule версии 1 удален из пакета размещения Windows](#hosting-aspnetcoremodule-v1-removed-from-windows-hosting-bundle)
- [Размещение. Универсальный узел ограничивает внедрение через конструктор Startup](#hosting-generic-host-restricts-startup-constructor-injection)
- [Размещение. Для приложений IIS вне процесса включено перенаправление HTTPS](#hosting-https-redirection-enabled-for-iis-out-of-process-apps)
- [Размещение. Удалены типы IHostingEnvironment и IApplicationLifetime](#hosting-ihostingenvironment-and-iapplicationlifetime-types-marked-obsolete-and-replaced)
- [Размещение. ObjectPoolProvider удален из зависимостей WebHostBuilder](#hosting-objectpoolprovider-removed-from-webhostbuilder-dependencies)
- [HTTP. Типы Kestrel и IIS BadHttpRequestException, помеченные как устаревшие и замененные](#http-kestrel-and-iis-badhttprequestexception-types-marked-obsolete-and-replaced)
- [HTTP. Изменения SameSite в браузере влияют на проверку подлинности](#http-browser-samesite-changes-impact-authentication)
- [HTTP. Удалена расширяемость DefaultHttpContext](#http-defaulthttpcontext-extensibility-removed)
- [HTTP. Поля HeaderNames изменены на статические только для чтения](#http-headernames-constants-changed-to-static-readonly)
- [HTTP. Экземпляры HttpClient, созданные с помощью целочисленных кодов состояния журнала IHttpClientFactory](#http-httpclient-instances-created-by-ihttpclientfactory-log-integer-status-codes)
- [HTTP. Изменения в инфраструктуре текста ответа](#http-response-body-infrastructure-changes)
- [HTTP. Внесены изменения в некоторые значения по умолчанию для параметра SameSite для файлов cookie](#http-some-cookie-samesite-defaults-changed-to-none)
- [HTTP. Синхронный ввод-вывода отключен по умолчанию](#http-synchronous-io-disabled-in-all-servers)
- [HttpSys: Повторное согласование сертификата клиента по умолчанию отключено](#httpsys-client-certificate-renegotiation-disabled-by-default)
- [Удостоверение. Удалена перегрузка метода AddDefaultUI](#identity-adddefaultui-method-overload-removed)
- [Удостоверение. Изменена версия начальной загрузки пользовательского интерфейса](#identity-default-bootstrap-version-of-ui-changed)
- [Удостоверение. SignInAsync создает исключение для удостоверения, не прошедшего проверку подлинности](#identity-signinasync-throws-exception-for-unauthenticated-identity)
- [Удостоверение. Конструктор SignInManager принимает новый параметр](#identity-signinmanager-constructor-accepts-new-parameter)
- [Удостоверение. Пользовательский интерфейс использует функцию статических веб-ресурсов](#identity-ui-uses-static-web-assets-feature)
- [IIS: строки запросов ПО промежуточного слоя UrlRewrite сохраняются](#iis-urlrewrite-middleware-query-strings-are-preserved)
- [Kestrel. Обнаружение изменений конфигурации во время выполнения включено по умолчанию](#kestrel-configuration-changes-at-run-time-detected-by-default)
- [Kestrel. Удалены адаптеры подключений](#kestrel-connection-adapters-removed)
- [Kestrel. Изменены поддерживаемые версии протокола TLS по умолчанию](#kestrel-default-supported-tls-protocol-versions-changed)
- [Kestrel. Удалена пустая сборка HTTPS](#kestrel-empty-https-assembly-removed)
- [Kestrel. HTTP/2 по TLS отключен в несовместимых версиях Windows](#kestrel-http2-disabled-over-tls-on-incompatible-windows-versions)
- [Kestrel. Транспорт Libuv помечен как устаревший](#kestrel-libuv-transport-marked-as-obsolete)
- [Kestrel. Заголовки трейлеров запросов перемещены в новую коллекцию](#kestrel-request-trailer-headers-moved-to-new-collection)
- [Kestrel. Внесены изменения в слой абстракции транспорта](#kestrel-transport-abstractions-removed-and-made-public)
- [Локализация. Интерфейсы API отмечены как устаревшие](#localization-resourcemanagerwithculturestringlocalizer-and-withculture-marked-obsolete)
- [Локализация. Удалены API-интерфейсы Pubternal](#localization-pubternal-apis-removed)
- [Локализация. Из ПО промежуточного слоя локализации запроса удален устаревший конструктор](#localization-obsolete-constructor-removed-in-request-localization-middleware)
- [Локализация. Удален класс ResourceManagerWithCultureStringLocalizer и элемент интерфейса WithCulture](#localization-resourcemanagerwithculturestringlocalizer-class-and-withculture-interface-member-removed)
- [Ведение журнала. Класс DebugLogger стал внутренним](#logging-debuglogger-class-made-internal)
- [ПО промежуточного слоя. Страница ошибок базы данных помечена как устаревшая](#middleware-database-error-page-marked-as-obsolete)
- [ПО промежуточного слоя. ПО промежуточного слоя обработчика исключений создает исходное исключение, если обработчик не найден](#middleware-exception-handler-middleware-throws-original-exception-if-handler-not-found)
- [MVC. Удален асинхронный суффикс действия контроллера](#mvc-async-suffix-trimmed-from-controller-action-names)
- [MVC. JsonResult перемещен в Microsoft.AspNetCore.Mvc.Core](#mvc-jsonresult-moved-to-microsoftaspnetcoremvccore)
- [MVC. ObjectModelValidator вызывает новую перегрузку ValidationVisitor.Validate](#mvc-objectmodelvalidator-calls-a-new-overload-of-validationvisitorvalidate)
- [MVC. Использование средства предварительной компиляции прекращено](#mvc-precompilation-tool-deprecated)
- [MVC. Типы теперь стали внутренними](#mvc-pubternal-types-changed-to-internal)
- [MVC. Удалена оболочка совместимости веб-интерфейса API](#mvc-web-api-compatibility-shim-removed)
- [Razor. Удален API RazorTemplateEngine](#razor-razortemplateengine-api-removed)
- [Razor. Компиляция среды выполнения перемещена в пакет](#razor-runtime-compilation-moved-to-a-package)
- [Безопасность. Удалена кодировка имен файлов cookie](#security-cookie-name-encoding-removed)
- [Безопасность. Обновлены версии пакета NuGet IdentityModel](#security-identitymodel-nuget-package-versions-updated)
- [Состояние сеанса. Удалены устаревшие API](#session-state-obsolete-apis-removed)
- [Общая платформа. Из Microsoft.AspNetCore.App удалена сборка](#shared-framework-assemblies-removed-from-microsoftaspnetcoreapp)
- [Общая платформа. Удален Microsoft.AspNetCore.All](#shared-framework-removed-microsoftaspnetcoreall)
- [SignalR. Заменен HandshakeProtocol.SuccessHandshakeData](#signalr-handshakeprotocolsuccesshandshakedata-replaced)
- [SignalR. Удалены методы HubConnection](#signalr-hubconnection-resetsendping-and-resettimeout-methods-removed)
- [SignalR. Изменены конструкторы HubConnectionContext](#signalr-hubconnectioncontext-constructors-changed)
- [SignalR. Изменено имя пакета клиента JavaScript](#signalr-javascript-client-package-name-changed)
- [SignalR. Протокол MessagePack для концентратора перемещен в пакет MessagePack 2.x](#signalr-messagepack-hub-protocol-moved-to-messagepack-2x-package)
- [SignalR. Тип параметров протокола концентратора MessagePack изменился](#signalr-messagepack-hub-protocol-options-type-changed)
- [SignalR. Устаревшие API](#signalr-usesignalr-and-useconnections-methods-marked-obsolete)
- [SignalR. Методы UseSignalR и UseConnections удалены](#signalr-usesignalr-and-useconnections-methods-removed)
- [Одностраничные приложения. Изменено поведение по умолчанию при переключении на средство ведения журнала консоли SpaServices и NodeServices](#spas-spaservices-and-nodeservices-no-longer-fall-back-to-console-logger)
- [Одностраничные приложения. SpaServices и NodeServices отмечены как устаревшие](#spas-spaservices-and-nodeservices-marked-obsolete)
- [Статические файлы. Тип содержимого CSV изменен на соответствующий стандартам](#static-files-csv-content-type-changed-to-standards-compliant)
- [Blazor WebAssembly не поддерживает интерфейсы API System.Security.Cryptography](#systemsecuritycryptography-apis-not-supported-on-blazor-webassembly)
- [Целевая платформа: прекращена поддержка .NET Framework](#target-framework-net-framework-support-dropped)

## <a name="aspnet-core-50"></a>ASP.NET Core 5.0

[!INCLUDE[Authentication: AzureAD.UI and AzureADB2C.UI APIs and packages marked obsolete](~/includes/core-changes/aspnetcore/5.0/authentication-aad-packages-obsolete.md)]

***

[!INCLUDE[Authorization: Resource in endpoint routing is HttpContext](~/includes/core-changes/aspnetcore/5.0/authorization-resource-in-endpoint-routing.md)]

***

[!INCLUDE[Azure: Microsoft-prefixed Azure integration packages removed](~/includes/core-changes/aspnetcore/5.0/azure-integration-packages-removed.md)]

***

[!INCLUDE[Serialization: BinaryFormatter serialization obsolete](~/includes/core-changes/corefx/5.0/binaryformatter-serialization-obsolete.md)]

***

[!INCLUDE[Blazor: Insignificant whitespace trimmed from components at compile time](~/includes/core-changes/aspnetcore/5.0/blazor-components-trim-insignificant-whitespace.md)]

***

[!INCLUDE[Blazor: JSObjectReference and JSInProcessObjectReference types changed to internal](~/includes/core-changes/aspnetcore/5.0/blazor-jsobjectreference-to-internal.md)]

***

[!INCLUDE[Blazor: ProtectedBrowserStorage feature moved to shared framework](~/includes/core-changes/aspnetcore/5.0/blazor-protectedbrowserstorage-moved.md)]

***

[!INCLUDE[Blazor: RenderTreeFrame readonly public fields have become properties](~/includes/core-changes/aspnetcore/5.0/blazor-rendertreeframe-fields-become-properties.md)]

***

[!INCLUDE[Blazor: Target framework of NuGet packages changed](~/includes/core-changes/aspnetcore/5.0/blazor-packages-target-framework-changed.md)]

***

[!INCLUDE[Blazor: Updated browser support](~/includes/core-changes/aspnetcore/5.0/blazor-browser-support-updated.md)]

***

[!INCLUDE[Extensions: Package reference changes](~/includes/core-changes/aspnetcore/5.0/extensions-package-reference-changes.md)]

***

[!INCLUDE[HTTP: HttpClient instances created by IHttpClientFactory log integer status codes](~/includes/core-changes/aspnetcore/5.0/http-httpclient-instances-log-integer-status-codes.md)]

***

[!INCLUDE[HTTP: Kestrel and IIS BadHttpRequestException types marked obsolete and replaced](~/includes/core-changes/aspnetcore/5.0/http-badhttprequestexception-obsolete.md)]

***

[!INCLUDE[HttpSys: Client certificate renegotiation disabled by default](~/includes/core-changes/aspnetcore/5.0/httpsys-client-certificate-renegotiation-disabled-by-default.md)]

***

[!INCLUDE[IIS: UrlRewrite middleware query strings are preserved](~/includes/core-changes/aspnetcore/5.0/iis-urlrewrite-middleware-query-strings-are-preserved.md)]

***

[!INCLUDE[Kestrel: Configuration changes at run time detected by default](~/includes/core-changes/aspnetcore/5.0/kestrel-configuration-changes-at-run-time-detected-by-default.md)]

***
[!INCLUDE[Kestrel: Default supported TLS protocol versions changed](~/includes/core-changes/aspnetcore/5.0/kestrel-default-supported-tls-protocol-versions-changed.md)]

***

[!INCLUDE[Kestrel: HTTP/2 disabled over TLS on incompatible Windows versions](~/includes/core-changes/aspnetcore/5.0/kestrel-disables-http2-over-tls.md)]

***

[!INCLUDE[Kestrel: Libuv transport marked as obsolete](~/includes/core-changes/aspnetcore/5.0/kestrel-libuv-transport-obsolete.md)]

***

[!INCLUDE[Localization: "Pubternal" APIs removed](~/includes/core-changes/aspnetcore/5.0/localization-pubternal-apis-removed.md)]

***

[!INCLUDE[Localization: Obsolete constructor removed in request localization middleware](~/includes/core-changes/aspnetcore/5.0/localization-requestlocalizationmiddleware-constructor-removed.md)]

***

[!INCLUDE[Localization: ResourceManagerWithCultureStringLocalizer class and WithCulture interface member removed](~/includes/core-changes/aspnetcore/5.0/localization-members-removed.md)]

***

[!INCLUDE[Middleware: Database error page marked as obsolete](~/includes/core-changes/aspnetcore/5.0/middleware-database-error-page-obsolete.md)]

***

[!INCLUDE[Middleware: Exception Handler Middleware throws original exception if handler not found](~/includes/core-changes/aspnetcore/5.0/middleware-exception-handler-throws-original-exception.md)]

***

[!INCLUDE[MVC: ObjectModelValidator calls a new overload of ValidationVisitor.Validate](~/includes/core-changes/aspnetcore/5.0/mvc-objectmodelvalidator-calls-new-overload.md)]

***

[!INCLUDE[Security: Cookie name encoding removed](~/includes/core-changes/aspnetcore/5.0/security-cookie-name-encoding-removed.md)]

***

[!INCLUDE[Security: IdentityModel NuGet package versions updated](~/includes/core-changes/aspnetcore/5.0/security-identitymodel-nuget-package-versions-updated.md)]

***

[!INCLUDE[SignalR: MessagePack Hub Protocol moved to MessagePack 2.x package](~/includes/core-changes/aspnetcore/5.0/signalr-messagepack-package.md)]

***

[!INCLUDE[SignalR: MessagePack Hub Protocol options type changed](~/includes/core-changes/aspnetcore/5.0/signalr-messagepack-hub-protocol-options-changed.md)]

***

[!INCLUDE[SignalR: UseSignalR and UseConnections methods removed](~/includes/core-changes/aspnetcore/5.0/signalr-usesignalr-useconnections-removed.md)]

***

[!INCLUDE[Cryptography APIs not supported on Blazor WebAssembly](~/includes/core-changes/cryptography/5.0/cryptography-apis-not-supported-on-blazor-webassembly.md)]

***

[!INCLUDE[Static files: CSV content type changed to standards-compliant](~/includes/core-changes/aspnetcore/5.0/static-files-csv-content-type-changed.md)]

***

## <a name="aspnet-core-31"></a>ASP.NET Core 3.1

[!INCLUDE[HTTP: Browser SameSite changes impact authentication](~/includes/core-changes/aspnetcore/3.1/http-cookie-samesite-authn-impacts.md)]

***

## <a name="aspnet-core-30"></a>ASP.NET Core 3.0

[!INCLUDE[Obsolete Antiforgery, CORS, Diagnostics, MVC, and Routing APIs removed](~/includes/core-changes/aspnetcore/3.0/obsolete-apis-removed.md)]

***

[!INCLUDE[Authentication: Google+ deprecation](~/includes/core-changes/aspnetcore/3.0/authn-google-plus-authn-changes.md)]

***

[!INCLUDE[Authentication: HttpContext.Authentication property removed](~/includes/core-changes/aspnetcore/3.0/authn-httpcontext-property-removed.md)]

***

[!INCLUDE[Authentication: Newtonsoft.Json types replaced](~/includes/core-changes/aspnetcore/3.0/authn-apis-json-types.md)]

***

[!INCLUDE[Authentication: OAuthHandler ExchangeCodeAsync signature changed](~/includes/core-changes/aspnetcore/3.0/authn-exchangecodeasync-signature-change.md)]

***

[!INCLUDE[Authorization: AddAuthorization overload assembly change](~/includes/core-changes/aspnetcore/3.0/authz-assembly-change.md)]

***

[!INCLUDE[Authorization: IAllowAnonymous removed from AuthorizationFilterContext.Filters](~/includes/core-changes/aspnetcore/3.0/authz-iallowanonymous-removed-from-collection.md)]

***

[!INCLUDE[Authorization: IAuthorizationPolicyProvider implementations require new method](~/includes/core-changes/aspnetcore/3.0/authz-iauthzpolicyprovider-new-method.md)]

***

[!INCLUDE[Caching: CompactOnMemoryPressure property removed](~/includes/core-changes/aspnetcore/3.0/caching-memory-property-removed.md)]

***

[!INCLUDE[Caching: Microsoft.Extensions.Caching.SqlServer uses new SqlClient package](~/includes/core-changes/aspnetcore/3.0/caching-new-sqlclient-package.md)]

***

[!INCLUDE[Caching: ResponseCaching types changed to internal](~/includes/core-changes/aspnetcore/3.0/caching-response-pubternal-to-internal.md)]

***

[!INCLUDE[Data Protection: DataProtection.AzureStorage uses new Azure Storage APIs](~/includes/core-changes/aspnetcore/3.0/dataprotection-azstorage-using-azstorage-apis.md)]

***

[!INCLUDE[Hosting: ANCM version 1 removed from hosting bundle](~/includes/core-changes/aspnetcore/3.0/hosting-ancmv1-hosting-bundle-removal.md)]

***

[!INCLUDE[Hosting: Generic host restriction on Startup constructor injection](~/includes/core-changes/aspnetcore/3.0/hosting-generic-host-startup-ctor-restriction.md)]

***

[!INCLUDE[Hosting: HTTPS redirection enabled for IIS OutOfProcess](~/includes/core-changes/aspnetcore/3.0/hosting-https-redirection-iis-outofprocess.md)]

***

[!INCLUDE[Hosting: IHostingEnvironment and IApplicationLifetime types replaced](~/includes/core-changes/aspnetcore/3.0/hosting-ihostingenv-iapplifetime-types-replaced.md)]

***

[!INCLUDE[Hosting: ObjectPoolProvider removed from WebHostBuilder dependencies](~/includes/core-changes/aspnetcore/3.0/hosting-objectpoolprovider-webhostbuilder-dependencies.md)]

***

[!INCLUDE[HTTP: DefaultHttpContext extensibility removed](~/includes/core-changes/aspnetcore/3.0/http-defaulthttpcontext-extensibility-removed.md)]

***

[!INCLUDE[HTTP: HeaderNames fields changed to static readonly](~/includes/core-changes/aspnetcore/3.0/http-headernames-constants-staticreadonly.md)]

***

[!INCLUDE[HTTP: Response body infrastructure changes](~/includes/core-changes/aspnetcore/3.0/http-response-body-changes.md)]

***

[!INCLUDE[HTTP: Some cookie SameSite default values changed](~/includes/core-changes/aspnetcore/3.0/http-cookie-samesite-defaults-change.md)]

***

[!INCLUDE[HTTP: Synchronous IO disabled by default](~/includes/core-changes/aspnetcore/3.0/http-synchronous-io-disabled.md)]

***

[!INCLUDE[Identity: AddDefaultUI method overload removed](~/includes/core-changes/aspnetcore/3.0/identity-ui-adddefaultui-overload-removed.md)]

***

[!INCLUDE[Identity: UI Bootstrap version change](~/includes/core-changes/aspnetcore/3.0/identity-ui-bootstrap-version.md)]

***

[!INCLUDE[Identity: SignInAsync throws exception for unauthenticated identity](~/includes/core-changes/aspnetcore/3.0/identity-signinasync-throws-exception.md)]

***

[!INCLUDE[Identity: SignInManager constructor accepts new parameter](~/includes/core-changes/aspnetcore/3.0/identity-signinmanager-ctor-parameter.md)]

***

[!INCLUDE[Identity: UI uses static web assets feature](~/includes/core-changes/aspnetcore/3.0/identity-ui-static-web-assets.md)]

***

[!INCLUDE[Kestrel: Connection adapters removed](~/includes/core-changes/aspnetcore/3.0/kestrel-connection-adapters-removed.md)]

***

[!INCLUDE[Kestrel: Empty HTTPS assembly removed](~/includes/core-changes/aspnetcore/3.0/kestrel-empty-assembly-removed.md)]

***

[!INCLUDE[Kestrel: Request trailer headers moved to new collection](~/includes/core-changes/aspnetcore/3.0/kestrel-request-trailer-headers.md)]

***

[!INCLUDE[Kestrel: Transport abstraction layer changes](~/includes/core-changes/aspnetcore/3.0/kestrel-transport-abstractions.md)]

***

[!INCLUDE[Localization: APIs marked obsolete](~/includes/core-changes/aspnetcore/3.0/localization-apis-marked-obsolete.md)]

***

[!INCLUDE[Logging: DebugLogger class made internal](~/includes/core-changes/aspnetcore/3.0/logging-debuglogger-to-internal.md)]

***

[!INCLUDE[MVC: Controller action Async suffix removed](~/includes/core-changes/aspnetcore/3.0/mvc-action-async-suffix-trimmed.md)]

***

[!INCLUDE[MVC: JsonResult moved to Microsoft.AspNetCore.Mvc.Core](~/includes/core-changes/aspnetcore/3.0/mvc-jsonresult-moved.md)]

***

[!INCLUDE[MVC: Precompilation tool deprecated](~/includes/core-changes/aspnetcore/3.0/mvc-precompilation-tool-deprecated.md)]

***

[!INCLUDE[MVC: Types changed to internal](~/includes/core-changes/aspnetcore/3.0/mvc-pubternal-to-internal.md)]

***

[!INCLUDE[MVC: Web API compatibility shim removed](~/includes/core-changes/aspnetcore/3.0/mvc-webapi-compat-shim-removed.md)]

***

[!INCLUDE[Razor: RazorTemplatEengine API removed](~/includes/core-changes/aspnetcore/3.0/razor-razortemplateengine-api-removed.md)]

***

[!INCLUDE[Razor: Runtime compilation moved to a package](~/includes/core-changes/aspnetcore/3.0/razor-runtime-compilation-package.md)]

***

[!INCLUDE[Session state: Obsolete APIs removed](~/includes/core-changes/aspnetcore/3.0/session-obsolete-apis-removed.md)]

***

[!INCLUDE[Shared framework: Assembly removal from Microsoft.AspNetCore.App](~/includes/core-changes/aspnetcore/3.0/sharedfx-app-shared-framework-assemblies.md)]

***

[!INCLUDE[Shared framework: Microsoft.AspNetCore.All removed](~/includes/core-changes/aspnetcore/3.0/sharedfx-all-framework-removed.md)]

***

[!INCLUDE[SignalR: HandshakeProtocol.SuccessHandshakeData replaced](~/includes/core-changes/aspnetcore/3.0/signalr-successhandshakedata-replaced.md)]

***

[!INCLUDE[SignalR: HubConnection methods removed](~/includes/core-changes/aspnetcore/3.0/signalr-hubconnection-methods-removed.md)]

***

[!INCLUDE[SignalR: HubConnectionContext constructors changed](~/includes/core-changes/aspnetcore/3.0/signalr-hubconnectioncontext-ctors.md)]

***

[!INCLUDE[SignalR: JavaScript client package name change](~/includes/core-changes/aspnetcore/3.0/signalr-js-client-package-name.md)]

***

[!INCLUDE[SignalR: Obsolete APIs](~/includes/core-changes/aspnetcore/3.0/signalr-obsolete-apis.md)]

***

[!INCLUDE[SPAs: SpaServices and NodeServices marked obsolete](~/includes/core-changes/aspnetcore/3.0/spas-spaservices-nodeservices-obsolete.md)]

***

[!INCLUDE[SPAs: SpaServices and NodeServices console logger fallback default change](~/includes/core-changes/aspnetcore/3.0/spas-spaservices-nodeservices-fallback.md)]

***

[!INCLUDE[Target framework: .NET Framework not supported](~/includes/core-changes/aspnetcore/3.0/targetfx-netfx-tfm-support.md)]

***
