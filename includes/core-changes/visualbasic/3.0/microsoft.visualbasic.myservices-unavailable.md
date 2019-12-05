---
ms.openlocfilehash: 58e65bae1593f23945a971b896a1db4a929b4587
ms.sourcegitcommit: 79a2d6a07ba4ed08979819666a0ee6927bbf1b01
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74567425"
---
### <a name="types-in-microsoftvisualbasicmyservices-namespace-not-available"></a><span data-ttu-id="5ff8c-101">Типы из пространства имен Microsoft.VisualBasic.MyServices недоступны</span><span class="sxs-lookup"><span data-stu-id="5ff8c-101">Types in Microsoft.VisualBasic.MyServices namespace not available</span></span>

<span data-ttu-id="5ff8c-102">Типы в пространстве имен <xref:Microsoft.VisualBasic.MyServices?displayProperty=fullName> недоступны.</span><span class="sxs-lookup"><span data-stu-id="5ff8c-102">The types in the <xref:Microsoft.VisualBasic.MyServices?displayProperty=fullName> namespace are not available.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="5ff8c-103">Представленная версия</span><span class="sxs-lookup"><span data-stu-id="5ff8c-103">Version introduced</span></span>

<span data-ttu-id="5ff8c-104">.NET Core 3.0 (предварительная версия 8)</span><span class="sxs-lookup"><span data-stu-id="5ff8c-104">.NET Core 3.0 Preview 8</span></span>

#### <a name="change-description"></a><span data-ttu-id="5ff8c-105">Описание изменений</span><span class="sxs-lookup"><span data-stu-id="5ff8c-105">Change description</span></span>

<span data-ttu-id="5ff8c-106">Типы из пространства имен <xref:Microsoft.VisualBasic.MyServices?displayProperty=fullName> были доступны в некоторых предварительных выпусках .NET Core 3.0.</span><span class="sxs-lookup"><span data-stu-id="5ff8c-106">The types in the <xref:Microsoft.VisualBasic.MyServices?displayProperty=fullName> namespace were available in some .NET Core 3.0 Preview releases.</span></span> <span data-ttu-id="5ff8c-107">Начиная с предварительной версии 9 .NET Core 3.0, они больше не доступны.</span><span class="sxs-lookup"><span data-stu-id="5ff8c-107">They are no longer available starting with .NET Core 3.0 Preview 9.</span></span>

<span data-ttu-id="5ff8c-108">Типы были удалены во избежание ненужных зависимостей сборок или критических изменений в последующих выпусках.</span><span class="sxs-lookup"><span data-stu-id="5ff8c-108">The types were removed to avoid unnecessary assembly dependencies or breaking changes in subsequent releases.</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="5ff8c-109">Рекомендуемое действие</span><span class="sxs-lookup"><span data-stu-id="5ff8c-109">Recommended action</span></span>

<span data-ttu-id="5ff8c-110">Если в вашем коде применяются типы **Microsoft.VisualBasic.MyServices** и их члены, вы можете использовать соответствующие типы и члены из библиотеки классов .NET.</span><span class="sxs-lookup"><span data-stu-id="5ff8c-110">If your code depends on the use of **Microsoft.VisualBasic.MyServices** types and their members, there are corresponding types and members in the .NET class library.</span></span> <span data-ttu-id="5ff8c-111">Ниже представлено сопоставление типов **Microsoft.VisualBasic.MyServices** и эквивалентных типов в библиотеке классов .NET.</span><span class="sxs-lookup"><span data-stu-id="5ff8c-111">The following is a mapping of  **Microsoft.VisualBasic.MyServices** types to their equivalent .NET class library types:</span></span>

|<span data-ttu-id="5ff8c-112">Тип Microsoft.VisualBasic.MyServices</span><span class="sxs-lookup"><span data-stu-id="5ff8c-112">Microsoft.VisualBasic.MyServices type</span></span>|<span data-ttu-id="5ff8c-113">Тип в библиотеке классов .NET</span><span class="sxs-lookup"><span data-stu-id="5ff8c-113">.NET class library type</span></span>|
|--|--|
|<xref:Microsoft.VisualBasic.MyServices.ClipboardProxy>|<span data-ttu-id="5ff8c-114"><xref:System.Windows.Clipboard?displayProperty=nameWithType> для приложений WPF, <xref:System.Windows.Forms.Clipboard?displayProperty=nameWithType> для приложений Windows Forms</span><span class="sxs-lookup"><span data-stu-id="5ff8c-114"><xref:System.Windows.Clipboard?displayProperty=nameWithType> for WPF applications, <xref:System.Windows.Forms.Clipboard?displayProperty=nameWithType> for Windows Forms applications</span></span>|
|<xref:Microsoft.VisualBasic.MyServices.FileSystemProxy>|<span data-ttu-id="5ff8c-115">Типы в пространстве имен <xref:System.IO></span><span class="sxs-lookup"><span data-stu-id="5ff8c-115">Types in the <xref:System.IO> namespace</span></span>|
|<xref:Microsoft.VisualBasic.MyServices.RegistryProxy>|<span data-ttu-id="5ff8c-116">Связанные с реестром типы в пространстве имен <xref:Microsoft.Win32></span><span class="sxs-lookup"><span data-stu-id="5ff8c-116">Registry-related types in the <xref:Microsoft.Win32> namespace</span></span>|
|<xref:Microsoft.VisualBasic.MyServices.SpecialDirectoriesProxy>|<xref:System.Environment.GetFolderPath%2A?displayProperty=nameWithType>|

#### <a name="category"></a><span data-ttu-id="5ff8c-117">Категория</span><span class="sxs-lookup"><span data-stu-id="5ff8c-117">Category</span></span>

<span data-ttu-id="5ff8c-118">Visual Basic</span><span class="sxs-lookup"><span data-stu-id="5ff8c-118">Visual Basic</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="5ff8c-119">Затронутые API</span><span class="sxs-lookup"><span data-stu-id="5ff8c-119">Affected APIs</span></span>

- <xref:Microsoft.VisualBasic.MyServices?displayProperty=fullName>

<!--

### Affected APIs

- `N:Microsoft.VisualBasic.MyServices`

-- >
