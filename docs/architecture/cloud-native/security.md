---
title: Безопасность
description: Создание архитектуры облачных приложений .NET для Azure | Бюллетеня
ms.date: 06/30/2019
ms.openlocfilehash: 848255de70038798417a558543d0b1ea8cff1e37
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/23/2019
ms.locfileid: "73840997"
---
# <a name="security"></a><span data-ttu-id="9852f-103">Безопасность</span><span class="sxs-lookup"><span data-stu-id="9852f-103">Security</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="9852f-104">Не в день, когда новости не содержат каких-либо сведений о компании, которую можно взломать или куда потеряют данные клиентов.</span><span class="sxs-lookup"><span data-stu-id="9852f-104">Not a day goes by where the news doesn't contain some story about a company being hacked or somehow losing their customers' data.</span></span> <span data-ttu-id="9852f-105">Даже страны не являются незащищенными от проблем, возникающих при обработке безопасности как игнорировать.</span><span class="sxs-lookup"><span data-stu-id="9852f-105">Even countries aren't immune to the problems created by treating security as an afterthought.</span></span> <span data-ttu-id="9852f-106">В течение многих лет компании обрабатывали безопасность данных клиентов и, по сути, все сети как что-нибудь «приятного».</span><span class="sxs-lookup"><span data-stu-id="9852f-106">For years, companies have treated the security of customer data and, in fact, their entire networks as something of a "nice to have".</span></span> <span data-ttu-id="9852f-107">Серверы Windows остались неисправленными, античногоные версии PHP работают и базы данных MongoDB остаются открытыми в мире.</span><span class="sxs-lookup"><span data-stu-id="9852f-107">Windows servers were left unpatched, ancient versions of PHP kept running and MongoDB databases left wide open to the world.</span></span>

<span data-ttu-id="9852f-108">Однако существуют реальные последствия для того, чтобы не поддерживать безопасность при создании и развертывании приложений.</span><span class="sxs-lookup"><span data-stu-id="9852f-108">However, there are starting to be real-world consequences for not maintaining a security mindset when building and deploying applications.</span></span> <span data-ttu-id="9852f-109">Многие компании изучили, что может произойти, когда серверы и настольные компьютеры не были исправлены в течение 2017 [нотпетя](https://www.wired.com/story/notpetya-cyberattack-ukraine-russia-code-crashed-the-world/).</span><span class="sxs-lookup"><span data-stu-id="9852f-109">Many companies learned the hard way what can happen when servers and desktops aren't patched during the 2017 outbreak of [NotPetya](https://www.wired.com/story/notpetya-cyberattack-ukraine-russia-code-crashed-the-world/).</span></span> <span data-ttu-id="9852f-110">Затраты на эти атаки легко достигают миллиардов, при этом некоторые оценки помещают ущерб от этой атаки на 10 000 000 000 долларов США.</span><span class="sxs-lookup"><span data-stu-id="9852f-110">The cost of these attacks has easily reached into the billions, with some estimates putting the losses from this single attack at 10 billion US dollars.</span></span>

<span data-ttu-id="9852f-111">Даже правительственные учреждения не являются уязвимыми для взлома инцидентов.</span><span class="sxs-lookup"><span data-stu-id="9852f-111">Even governments aren't immune to hacking incidents.</span></span> <span data-ttu-id="9852f-112">Город Baltimore был удержан [злоумышленниками](https://www.vox.com/recode/2019/5/21/18634505/baltimore-ransom-robbinhood-mayor-jack-young-hackers) , что не позволяет граждану платить счета или использовать службы городов.</span><span class="sxs-lookup"><span data-stu-id="9852f-112">The city of Baltimore was held ransom by [criminals](https://www.vox.com/recode/2019/5/21/18634505/baltimore-ransom-robbinhood-mayor-jack-young-hackers) making it impossible for citizens to pay their bills or use city services.</span></span>

<span data-ttu-id="9852f-113">Также было увеличено законодательство, которое требует защиты данных для персональных данных.</span><span class="sxs-lookup"><span data-stu-id="9852f-113">There has also been an increase in legislation that mandates certain data protections for personal data.</span></span> <span data-ttu-id="9852f-114">В Европе GDPR действует в течение более чем года, и в последнее время Калифорния передавал свою собственную версию под названием ККДА, которая вступает в действие 1 января 2020 г.</span><span class="sxs-lookup"><span data-stu-id="9852f-114">In Europe, GDPR has been in effect for more than a year and, more recently, California passed their own version called CCDA, which comes into effect January 1, 2020.</span></span> <span data-ttu-id="9852f-115">В GDPR может быть так, чтобы пунишинг, как и компании.</span><span class="sxs-lookup"><span data-stu-id="9852f-115">The fines under GDPR can be so punishing as to put companies out of business.</span></span> <span data-ttu-id="9852f-116">Google уже мелких 50 000 000 евро на предмет нарушений, но это просто перетаскивание в контейнере по сравнению с потенциальными штрафами.</span><span class="sxs-lookup"><span data-stu-id="9852f-116">Google has already been fined 50 million Euros for violations, but that's just a drop in the bucket compared with the potential fines.</span></span>

<span data-ttu-id="9852f-117">Вкратце, безопасность — серьезный бизнес.</span><span class="sxs-lookup"><span data-stu-id="9852f-117">In short, security is serious business.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="9852f-118">[Назад](identity-server.md)
>[Вперед](azure-security.md)</span><span class="sxs-lookup"><span data-stu-id="9852f-118">[Previous](identity-server.md)
[Next](azure-security.md)</span></span>