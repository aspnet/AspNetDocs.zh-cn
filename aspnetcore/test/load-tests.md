---
title: ASP.NET Core 负载/压力测试
author: Jeremy-Meng
description: 介绍了几个值得注意的工具和方法可用于负载测试和压力测试 ASP.NET Core 应用。
ms.author: riande
ms.custom: mvc
ms.date: 01/04/2019
uid: test/loadtests
ms.openlocfilehash: d989bc841a372bed7ebf2c84c6abe1a57762ad04
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57061404"
---
# <a name="load-and-stress-testing-aspnet-core"></a><span data-ttu-id="a61c9-103">负载测试和压力测试 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="a61c9-103">Load and stress testing ASP.NET Core</span></span>

<span data-ttu-id="a61c9-104">负载测试和压力测试是非常重要的 web 应用的性能和可缩放。</span><span class="sxs-lookup"><span data-stu-id="a61c9-104">Load testing and stress testing are important to ensure a web app is performant and scalable.</span></span> <span data-ttu-id="a61c9-105">其目标是不同甚至它们通常共享类似测试。</span><span class="sxs-lookup"><span data-stu-id="a61c9-105">Their goals are different even they often share similar tests.</span></span>

<span data-ttu-id="a61c9-106">**负载测试**:测试是否应用可以处理表示特定的场景中的用户指定的负载，同时仍能满足响应目标。</span><span class="sxs-lookup"><span data-stu-id="a61c9-106">**Load tests**: Tests whether the app can handle a specified load of users for a certain scenario while still satisfying the response goal.</span></span> <span data-ttu-id="a61c9-107">在正常情况下运行该应用。</span><span class="sxs-lookup"><span data-stu-id="a61c9-107">The app is run under normal conditions.</span></span>

<span data-ttu-id="a61c9-108">**压力测试**:测试应用程序稳定性下极端条件和通常长时间运行时：</span><span class="sxs-lookup"><span data-stu-id="a61c9-108">**Stress tests**: Tests app stability when running under extreme conditions and often a long period of time:</span></span>

* <span data-ttu-id="a61c9-109">较高用户负载 – 峰值或逐渐增加。</span><span class="sxs-lookup"><span data-stu-id="a61c9-109">High user load – either spikes or gradually increasing.</span></span>
* <span data-ttu-id="a61c9-110">有限的计算资源。</span><span class="sxs-lookup"><span data-stu-id="a61c9-110">Limited computing resources.</span></span>  

<span data-ttu-id="a61c9-111">在负载下，可以应用从故障中恢复并适当地返回到预期的行为？</span><span class="sxs-lookup"><span data-stu-id="a61c9-111">Under stress, can the app recover from failure and gracefully return to expected behavior?</span></span> <span data-ttu-id="a61c9-112">应用程序是在压力下*不*在正常情况下运行。</span><span class="sxs-lookup"><span data-stu-id="a61c9-112">Under stress, the app is *not* run under normal conditions.</span></span>

## <a name="visual-studio-tools"></a><span data-ttu-id="a61c9-113">Visual Studio Tools</span><span class="sxs-lookup"><span data-stu-id="a61c9-113">Visual Studio Tools</span></span>

<span data-ttu-id="a61c9-114">Visual Studio 允许用户创建、 开发和调试 web 性能和负载测试。</span><span class="sxs-lookup"><span data-stu-id="a61c9-114">Visual Studio allows users to create, develop, and debug web performance and load tests.</span></span> <span data-ttu-id="a61c9-115">一个选项，可通过 web 浏览器中录制操作创建测试。</span><span class="sxs-lookup"><span data-stu-id="a61c9-115">An option is available to create tests by recording actions in web browser.</span></span>

<span data-ttu-id="a61c9-116">[快速入门：创建负载测试项目](/visualstudio/test/quickstart-create-a-load-test-project?view=vs-2017)演示如何创建、 配置和运行负载测试项目使用 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="a61c9-116">[Quickstart: Create a load test project](/visualstudio/test/quickstart-create-a-load-test-project?view=vs-2017) shows how to create, configure, and run a load test projects using Visual Studio 2017.</span></span>

<span data-ttu-id="a61c9-117">有关详细信息，请参阅[其他资源](#add)。</span><span class="sxs-lookup"><span data-stu-id="a61c9-117">See [Additional Resources](#add) for more information.</span></span>

<span data-ttu-id="a61c9-118">可以配置负载测试运行中的本地或在云中使用 Azure DevOps 运行。</span><span class="sxs-lookup"><span data-stu-id="a61c9-118">Load tests can be configured to run in on-premise or run in the cloud using Azure DevOps.</span></span>

## <a name="azure-devops"></a><span data-ttu-id="a61c9-119">Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="a61c9-119">Azure DevOps</span></span>

<span data-ttu-id="a61c9-120">可以使用启动负载测试运行[Azure DevOps 测试计划](/azure/devops/test/load-test/index?view=vsts)服务。</span><span class="sxs-lookup"><span data-stu-id="a61c9-120">Load test runs can be started using the [Azure DevOps Test Plans](/azure/devops/test/load-test/index?view=vsts) service.</span></span>

![](./load-tests/_static/azure-devops-load-test.png)

<span data-ttu-id="a61c9-121">该服务支持以下类型的测试格式：</span><span class="sxs-lookup"><span data-stu-id="a61c9-121">The service supports the following types of test format:</span></span>

- <span data-ttu-id="a61c9-122">Visual Studio 测试 – Visual Studio 中创建的 web 测试。</span><span class="sxs-lookup"><span data-stu-id="a61c9-122">Visual Studio test – web test created in Visual Studio.</span></span>
- <span data-ttu-id="a61c9-123">在测试期间重播基于 HTTP 存档的测试 – 存档内捕获的 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="a61c9-123">HTTP Archive-based test – captured HTTP traffic inside archive is replayed during testing.</span></span>
- <span data-ttu-id="a61c9-124">[基于 URL 的测试](/azure/devops/test/load-test/get-started-simple-cloud-load-test?view=vsts)– 允许指定的 Url 来加载测试、 请求类型、 标头和查询字符串。</span><span class="sxs-lookup"><span data-stu-id="a61c9-124">[URL-based test](/azure/devops/test/load-test/get-started-simple-cloud-load-test?view=vsts) – allows specifying URLs to load test, request types, headers, and query strings.</span></span> <span data-ttu-id="a61c9-125">运行设置参数，如持续时间，可以配置负载模式，用户等。</span><span class="sxs-lookup"><span data-stu-id="a61c9-125">Run setting parameters such as duration, load pattern, number of users, etc., can be configured.</span></span>
- <span data-ttu-id="a61c9-126">[Apache JMeter](https://jmeter.apache.org/)测试。</span><span class="sxs-lookup"><span data-stu-id="a61c9-126">[Apache JMeter](https://jmeter.apache.org/) test.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="a61c9-127">Azure 门户</span><span class="sxs-lookup"><span data-stu-id="a61c9-127">Azure portal</span></span>

<span data-ttu-id="a61c9-128">[Azure 门户允许设置和运行负载测试的 Web 应用，](/azure/devops/test/load-test/app-service-web-app-performance-test?view=vsts)直接从 Azure 门户中的应用服务的性能选项卡。</span><span class="sxs-lookup"><span data-stu-id="a61c9-128">[Azure portal allows setting up and running load testing of Web Apps,](/azure/devops/test/load-test/app-service-web-app-performance-test?view=vsts) directly from the Performance tab of the App Service in Azure portal.</span></span>

![](./load-tests/_static/azure-appservice-perf-test.png)

<span data-ttu-id="a61c9-129">测试可以是包含指定的 URL 或可以测试多个 Url 的 Visual Studio Web 测试文件的手动测试。</span><span class="sxs-lookup"><span data-stu-id="a61c9-129">The test can be a manual test with a specified URL, or a Visual Studio Web Test file, which can test multiple URLs.</span></span>

![](./load-tests/_static/azure-appservice-perf-test-config.png)

<span data-ttu-id="a61c9-130">在测试结束时，会生成报表来显示该应用程序的性能特征。</span><span class="sxs-lookup"><span data-stu-id="a61c9-130">At end of the test, reports are generated to show the performance characteristics of the app.</span></span> <span data-ttu-id="a61c9-131">示例统计信息包括：</span><span class="sxs-lookup"><span data-stu-id="a61c9-131">Example statistics include:</span></span>

- <span data-ttu-id="a61c9-132">平均响应时间</span><span class="sxs-lookup"><span data-stu-id="a61c9-132">Average response time</span></span>
- <span data-ttu-id="a61c9-133">最大吞吐量： 每秒请求数</span><span class="sxs-lookup"><span data-stu-id="a61c9-133">Max throughput: requests per second</span></span>
- <span data-ttu-id="a61c9-134">失败百分比</span><span class="sxs-lookup"><span data-stu-id="a61c9-134">Failure percentage</span></span>

## <a name="third-party-tools"></a><span data-ttu-id="a61c9-135">第三方工具</span><span class="sxs-lookup"><span data-stu-id="a61c9-135">Third-party Tools</span></span>

<span data-ttu-id="a61c9-136">以下列表包含各种功能集与第三方 web 性能工具：</span><span class="sxs-lookup"><span data-stu-id="a61c9-136">The following list contains third-party web performance tools with various feature sets:</span></span>

- <span data-ttu-id="a61c9-137">[Apache JMeter](https://jmeter.apache.org/) :负载测试工具的完整特色的套件。</span><span class="sxs-lookup"><span data-stu-id="a61c9-137">[Apache JMeter](https://jmeter.apache.org/) : Full featured suite of load testing tools.</span></span> <span data-ttu-id="a61c9-138">线程绑定： 需要每个用户的一个线程。</span><span class="sxs-lookup"><span data-stu-id="a61c9-138">Thread-bound: need one thread per user.</span></span>
- [<span data-ttu-id="a61c9-139">ab 的基准测试工具的 Apache HTTP 服务器</span><span class="sxs-lookup"><span data-stu-id="a61c9-139">ab - Apache HTTP server benchmarking tool</span></span>](https://httpd.apache.org/docs/2.4/programs/ab.html)
- <span data-ttu-id="a61c9-140">[Gatling](https://gatling.io/) :使用 GUI 和测试的刻录机的桌面工具。</span><span class="sxs-lookup"><span data-stu-id="a61c9-140">[Gatling](https://gatling.io/) : Desktop tool with a GUI and test recorders.</span></span> <span data-ttu-id="a61c9-141">JMeter 性能更强。</span><span class="sxs-lookup"><span data-stu-id="a61c9-141">More performant than JMeter.</span></span>
- <span data-ttu-id="a61c9-142">[Locust.io](https://locust.io/) :不受线程。</span><span class="sxs-lookup"><span data-stu-id="a61c9-142">[Locust.io](https://locust.io/) : Not bounded by threads.</span></span>

<a name="add"></a>
## <a name="additional-resources"></a><span data-ttu-id="a61c9-143">其他资源</span><span class="sxs-lookup"><span data-stu-id="a61c9-143">Additional Resources</span></span>

<span data-ttu-id="a61c9-144">[加载测试博客系列](https://blogs.msdn.microsoft.com/charles_sterling/2015/06/01/load-test-series-part-i-creating-web-performance-tests-for-a-load-test/)作者： Charles Sterling。</span><span class="sxs-lookup"><span data-stu-id="a61c9-144">[Load Test blog series](https://blogs.msdn.microsoft.com/charles_sterling/2015/06/01/load-test-series-part-i-creating-web-performance-tests-for-a-load-test/) by Charles Sterling.</span></span> <span data-ttu-id="a61c9-145">日期，但大多数主题都仍适用。</span><span class="sxs-lookup"><span data-stu-id="a61c9-145">Dated but most of the topics are still relevant.</span></span>
