---
title: Действия в рабочем процессе внешнего цикла DevOps для приложения Docker
description: Жизненный цикл контейнерного приложения Docker на основе платформы и средств Майкрософт
ms.date: 02/15/2019
ms.openlocfilehash: 9fdc5acfd375e4f2266859f061ef1c854286b914
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/30/2019
ms.locfileid: "68673781"
---
# <a name="creating-cicd-pipelines-in-azure-devops-services-for-a-net-core-20-application-on-containers-and-deploying-to-a-kubernetes-cluster"></a><span data-ttu-id="2987b-103">Создание конвейеров CI/CD в службах Azure DevOps для приложения .NET Core 2.0 в контейнерах и развертывание в кластер Kubernetes</span><span class="sxs-lookup"><span data-stu-id="2987b-103">Creating CI/CD pipelines in Azure DevOps Services for a .NET Core 2.0 application on Containers and deploying to a Kubernetes cluster</span></span>

<span data-ttu-id="2987b-104">На рисунке 5-12 показан комплексный сценарий DevOps, охватывающий управление кодом, компиляцию кода, создание образов Docker, отправку образы Docker в реестр Docker и, наконец, развертывание в кластере Kubernetes в Azure.</span><span class="sxs-lookup"><span data-stu-id="2987b-104">In Figure 5-12 you can see the end-to-end DevOps scenario covering the code management, code compilation, Docker images build, Docker images push to a Docker registry and finally the deployment to a Kubernetes cluster in Azure.</span></span>

![Рабочий процесс: начинается с компьютера разработки.](media/docker-workflow-ci-cd-aks.png)

<span data-ttu-id="2987b-107">**Рис. 5-12**.</span><span class="sxs-lookup"><span data-stu-id="2987b-107">**Figure 5-12**.</span></span> <span data-ttu-id="2987b-108">Сценарии CI/CD для создания образов Docker и развертывания в кластере Kubernetes в Azure</span><span class="sxs-lookup"><span data-stu-id="2987b-108">CI/CD scenario creating Docker images and deploying to a Kubernetes cluster in Azure</span></span>

<span data-ttu-id="2987b-109">Важно отметить, что два конвейера — сборки/CI и выпуска/CD — подключены через реестр Docker (например, Docker Hub или Реестр контейнеров Azure).</span><span class="sxs-lookup"><span data-stu-id="2987b-109">It is important to highlight that the two pipelines, build/CI, and release/CD, are connected through the Docker Registry (such as Docker Hub or Azure Container Registry).</span></span> <span data-ttu-id="2987b-110">Реестр Docker является одним из основных отличий по сравнению с традиционным процессом CI/CD без Docker.</span><span class="sxs-lookup"><span data-stu-id="2987b-110">The Docker registry is one of the main differences compared to a traditional CI/CD process without Docker.</span></span>

<span data-ttu-id="2987b-111">Как показано на рисунке 5-13, первым этапом является конвейер сборки/CI.</span><span class="sxs-lookup"><span data-stu-id="2987b-111">As shown in Figure 5-13, the first phase is the build/CI pipeline.</span></span> <span data-ttu-id="2987b-112">В Azure DevOps Services можно создать конвейеры сборки/CI, которые будут компилировать код, создавать образы Docker и отправлять их в реестр Docker, например Docker Hub или Реестр контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="2987b-112">In Azure DevOps Services you can create build/CI pipelines that will compile the code, create the Docker images, and push them to a Docker Registry like Docker Hub or Azure Container Registry.</span></span>

![Браузерное представление Azure DevOps с определением задачи создания процесса.](media/build-ci-pipeline-azure-devops-push-to-docker-registry.png)

<span data-ttu-id="2987b-114">**Рис. 5-13**.</span><span class="sxs-lookup"><span data-stu-id="2987b-114">**Figure 5-13**.</span></span> <span data-ttu-id="2987b-115">Конвейер сборки/CI в Azure DevOps, создающий образы Docker и отправляющий их в реестр Docker</span><span class="sxs-lookup"><span data-stu-id="2987b-115">Build/CI pipeline in Azure DevOps building Docker images and pushing images to a Docker registry</span></span>

<span data-ttu-id="2987b-116">Второй этап заключается в создании конвейера развертывания/выпуска.</span><span class="sxs-lookup"><span data-stu-id="2987b-116">The second phase is to create a deployment/release pipeline.</span></span> <span data-ttu-id="2987b-117">В Azure DevOps Services можно легко создать конвейер развертывания, ориентированный на кластер Kubernetes, с помощью задач Kubernetes для Azure DevOps Services, как показано на рисунке 5-14.</span><span class="sxs-lookup"><span data-stu-id="2987b-117">In Azure DevOps Services, you can easily create a deployment pipeline targeting a Kubernetes cluster by using the Kubernetes tasks for Azure DevOps Services, as shown in Figure 5-14.</span></span>

![Браузерное представление Azure DevOps с определением задачи развертывания в Kubernetes.](media/release-cd-pipeline-azure-devops-deploy-to-kubernetes.png)

<span data-ttu-id="2987b-119">**Рис. 5-14**.</span><span class="sxs-lookup"><span data-stu-id="2987b-119">**Figure 5-14**.</span></span> <span data-ttu-id="2987b-120">Конвейер выпуска/CD в Azure DevOps Services, осуществляющий развертывание в кластере Kubernetes</span><span class="sxs-lookup"><span data-stu-id="2987b-120">Release/CD pipeline in Azure DevOps Services deploying to a Kubernetes cluster</span></span>

> [!Пошаговое руководство]<span data-ttu-id="2987b-121"> Развертывание eShopModernized в Kubernetes:</span><span class="sxs-lookup"><span data-stu-id="2987b-121"> Deploying eShopModernized to Kubernetes:</span></span>
>
> <span data-ttu-id="2987b-122">Подробное пошаговое руководство для конвейеров CI/CD Azure DevOps, осуществляющих развертывание в Kubernetes, см. в этой записи: </span><span class="sxs-lookup"><span data-stu-id="2987b-122">For a detailed walkthrough of Azure DevOps CI/CD pipelines deploying to Kubernetes, see this post: </span></span>\
><https://github.com/dotnet-architecture/eShopModernizing/wiki/04.-How-to-deploy-your-Windows-Containers-based-apps-into-Kubernetes-in-Azure-Container-Service-(Including-CI-CD)>

>[!div class="step-by-step"]
><span data-ttu-id="2987b-123">[Назад](docker-application-outer-loop-devops-workflow.md)
>[Вперед](../run-manage-monitor-docker-environments/index.md)</span><span class="sxs-lookup"><span data-stu-id="2987b-123">[Previous](docker-application-outer-loop-devops-workflow.md)
[Next](../run-manage-monitor-docker-environments/index.md)</span></span>