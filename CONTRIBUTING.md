# <a name="contribute-to-the-aspnet-documentation"></a><span data-ttu-id="937fd-101">参与 ASP.NET 文档</span><span class="sxs-lookup"><span data-stu-id="937fd-101">Contribute to the ASP.NET documentation</span></span>

<span data-ttu-id="937fd-102">本文档介绍了参与到 [ASP.NET 文档站点](https://docs.microsoft.com/aspnet/)上托管的文章和代码示例中的过程。</span><span class="sxs-lookup"><span data-stu-id="937fd-102">This document covers the process for contributing to the articles and code samples that are hosted on the [ASP.NET documentation site](https://docs.microsoft.com/aspnet/).</span></span> <span data-ttu-id="937fd-103">欢迎更正拼写错误以及撰写新文章。</span><span class="sxs-lookup"><span data-stu-id="937fd-103">Typo corrections and new articles are welcome contributions.</span></span>

## <a name="how-to-make-a-simple-correction-or-suggestion"></a><span data-ttu-id="937fd-104">如何提出简单的更正或建议</span><span class="sxs-lookup"><span data-stu-id="937fd-104">How to make a simple correction or suggestion</span></span>

<span data-ttu-id="937fd-105">文章作为 Markdown 文件存储在存储库中。</span><span class="sxs-lookup"><span data-stu-id="937fd-105">Articles are stored in the repository as Markdown files.</span></span> <span data-ttu-id="937fd-106">通过选择浏览器窗口右上角的“编辑”链接，可以在浏览器中对 Markdown 文件的内容进行简单更改。</span><span class="sxs-lookup"><span data-stu-id="937fd-106">Simple changes to the content of a Markdown file are made in the browser by selecting the **Edit** link in the upper-right corner of the browser window.</span></span> <span data-ttu-id="937fd-107">（在窄浏览器窗口中，展开“选项”栏，以查看“编辑”链接 。）按照说明创建拉取请求 (PR)。</span><span class="sxs-lookup"><span data-stu-id="937fd-107">(In a narrow browser window, expand the **options** bar to see the **Edit** link.) Follow the directions to create a pull request (PR).</span></span> <span data-ttu-id="937fd-108">我们将对拉取请求进行评审并接受相关请求或提出更改建议。</span><span class="sxs-lookup"><span data-stu-id="937fd-108">We will review the PR and accept it or suggest changes.</span></span>

## <a name="how-to-make-a-more-complex-submission"></a><span data-ttu-id="937fd-109">如何提出更复杂的提交</span><span class="sxs-lookup"><span data-stu-id="937fd-109">How to make a more complex submission</span></span>

<span data-ttu-id="937fd-110">需要对 [Git 和 GitHub.com](https://guides.github.com/activities/hello-world/) 有基本的理解。</span><span class="sxs-lookup"><span data-stu-id="937fd-110">You need a basic understanding of [Git and GitHub.com](https://guides.github.com/activities/hello-world/).</span></span>

* <span data-ttu-id="937fd-111">创建一个[问题](https://github.com/dotnet/AspNetDocs/issues/new)，描述你想要执行的操作，例如更改现有项目或创建一个新项目。</span><span class="sxs-lookup"><span data-stu-id="937fd-111">Open an [issue](https://github.com/dotnet/AspNetDocs/issues/new) describing what you want to do, such as changing an existing article or creating a new one.</span></span> <span data-ttu-id="937fd-112">我们经常要求提供新主题建议的大纲。</span><span class="sxs-lookup"><span data-stu-id="937fd-112">We often request an outline for a new topic suggestion.</span></span> <span data-ttu-id="937fd-113">请等待团队批准后再投入时间参与进来。</span><span class="sxs-lookup"><span data-stu-id="937fd-113">Wait for approval from the team before you invest much time.</span></span>
* <span data-ttu-id="937fd-114">将 [dotnet/AspNetDocs](https://github.com/dotnet/AspNetDocs/) 存储库分叉，并为更改创建分支。</span><span class="sxs-lookup"><span data-stu-id="937fd-114">Fork the [dotnet/AspNetDocs](https://github.com/dotnet/AspNetDocs/) repository and create a branch for your changes.</span></span>
* <span data-ttu-id="937fd-115">使用所做的更改向 *主* 分支提交 PR。</span><span class="sxs-lookup"><span data-stu-id="937fd-115">Submit a PR to the *main* branch with your changes.</span></span>
* <span data-ttu-id="937fd-116">如果拉取请求分配的标签为 “cla-required”，则[完成贡献许可协议 (CLA)](https://cla.dotnetfoundation.org/)。</span><span class="sxs-lookup"><span data-stu-id="937fd-116">If your PR has the label 'cla-required' assigned, [complete the Contribution License Agreement (CLA)](https://cla.dotnetfoundation.org/).</span></span>
* <span data-ttu-id="937fd-117">对 PR 请求反馈进行响应。</span><span class="sxs-lookup"><span data-stu-id="937fd-117">Respond to PR feedback.</span></span>

<span data-ttu-id="937fd-118">有关此过程引导发布新文章的示例，请参阅 .NET Docs 存储库中的[问题&num; 67 ](https://github.com/dotnet/docs/issues/67)和[拉取请求&num; 798](https://github.com/dotnet/docs/pull/798)。</span><span class="sxs-lookup"><span data-stu-id="937fd-118">For an example where this process led to publication of a new article, see [Issue &num;67](https://github.com/dotnet/docs/issues/67) and [Pull Request &num;798](https://github.com/dotnet/docs/pull/798) in the .NET Docs repository.</span></span> <span data-ttu-id="937fd-119">新文章为[编写代码](https://docs.microsoft.com/dotnet/articles/csharp/codedoc)。</span><span class="sxs-lookup"><span data-stu-id="937fd-119">The new article is [Documenting your code](https://docs.microsoft.com/dotnet/articles/csharp/codedoc).</span></span>

## <a name="docs-authoring-pack-extension-in-visual-studio-code"></a><span data-ttu-id="937fd-120">Visual Studio Code 中的 Docs 创作包扩展</span><span class="sxs-lookup"><span data-stu-id="937fd-120">Docs Authoring Pack extension in Visual Studio Code</span></span>

<span data-ttu-id="937fd-121">如果使用 Visual Studio Code 参与到 ASP.NET 文档中，可以通过安装 [Docs 创作包](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack)扩展来提高工作效率。</span><span class="sxs-lookup"><span data-stu-id="937fd-121">If you use Visual Studio Code to contribute to the ASP.NET documentation, you can boost your productivity by installing the [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) extension.</span></span> <span data-ttu-id="937fd-122">该扩展提供各种有助于 Markdown 语法检查、代码拼写检查和项目模板的工具。</span><span class="sxs-lookup"><span data-stu-id="937fd-122">The extension provides a variety of tools that helps with Markdown linting, code spell checking, and article templates.</span></span>

## <a name="markdown-syntax"></a><span data-ttu-id="937fd-123">Markdown 语法</span><span class="sxs-lookup"><span data-stu-id="937fd-123">Markdown syntax</span></span>

<span data-ttu-id="937fd-124">文章采用 [DocFx 风格的 Markdown](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html) 编写，它是 [GitHub 风格的 Markdown (GFM)](https://guides.github.com/features/mastering-markdown/) 的超集。</span><span class="sxs-lookup"><span data-stu-id="937fd-124">Articles are written in [DocFx-flavored Markdown](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html), which is a superset of [GitHub-flavored Markdown (GFM)](https://guides.github.com/features/mastering-markdown/).</span></span> <span data-ttu-id="937fd-125">有关 ASP.NET 文档中常用的 UI 功能的 DFM 语法示例，请参阅 .NET 文档存储库样式指南中的 [元数据和 Markdown 模板](https://github.com/dotnet/docs/blob/main/styleguide/template.md) 。</span><span class="sxs-lookup"><span data-stu-id="937fd-125">For examples of DFM syntax for UI features commonly used in the ASP.NET documentation, see [Metadata and Markdown Template](https://github.com/dotnet/docs/blob/main/styleguide/template.md) in the .NET Docs repository style guide.</span></span>

## <a name="folder-structure-conventions"></a><span data-ttu-id="937fd-126">文件夹结构约定</span><span class="sxs-lookup"><span data-stu-id="937fd-126">Folder structure conventions</span></span>

<span data-ttu-id="937fd-127">对于每个Markdown 文件，可能存在图像文件夹和示例代码文件夹。</span><span class="sxs-lookup"><span data-stu-id="937fd-127">For each Markdown file, a folder for images and a folder for sample code may exist.</span></span> <span data-ttu-id="937fd-128">如果项目是 [signalr/概述/高级/依赖关系-注入](https://github.com/dotnet/AspNetDocs/blob/main/aspnet/signalr/overview/advanced/dependency-injection.md)，则图像处于 [signalr/概述/高级/依赖关系注入/ \_ 静态](https://github.com/dotnet/AspNetDocs/tree/main/aspnet/signalr/overview/advanced/dependency-injection/_static) ，示例应用项目文件位于 [signalr/概述/高级/依赖关系注入/示例](https://github.com/dotnet/AspNetDocs/tree/main/aspnet/signalr/overview/advanced/dependency-injection/samples)中。</span><span class="sxs-lookup"><span data-stu-id="937fd-128">If the article is [signalr/overview/advanced/dependency-injection.md](https://github.com/dotnet/AspNetDocs/blob/main/aspnet/signalr/overview/advanced/dependency-injection.md), the images are in [signalr/overview/advanced/dependency-injection/\_static](https://github.com/dotnet/AspNetDocs/tree/main/aspnet/signalr/overview/advanced/dependency-injection/_static) and the sample app project files are in [signalr/overview/advanced/dependency-injection/samples](https://github.com/dotnet/AspNetDocs/tree/main/aspnet/signalr/overview/advanced/dependency-injection/samples).</span></span> <span data-ttu-id="937fd-129">*Signalr/概述/advanced/依赖关系注入* 文件中的图像由以下 Markdown 呈现：</span><span class="sxs-lookup"><span data-stu-id="937fd-129">An image in the *signalr/overview/advanced/dependency-injection.md* file is rendered by the following Markdown:</span></span>

```md
![description of image for alt attribute](dependency-injection/_static/image1.png)
```

<span data-ttu-id="937fd-130">所有图像都应具有[替代 (alt) 文本](https://wikipedia.org/wiki/Alt_attribute)。</span><span class="sxs-lookup"><span data-stu-id="937fd-130">All images should have [alternative (alt) text](https://wikipedia.org/wiki/Alt_attribute).</span></span> <span data-ttu-id="937fd-131">有关指定替代文本的建议，请参阅在线资源，例如 [WebAIM：替代文本](https://webaim.org/techniques/alttext/)。</span><span class="sxs-lookup"><span data-stu-id="937fd-131">For advice on specifying alt text, see online resources, such as [WebAIM: Alternative Text](https://webaim.org/techniques/alttext/).</span></span>

<span data-ttu-id="937fd-132">Markdown 文件名称和图像文件名称使用小写。</span><span class="sxs-lookup"><span data-stu-id="937fd-132">Use lowercase for Markdown file names and image file names.</span></span>

## <a name="internal-links"></a><span data-ttu-id="937fd-133">内部链接</span><span class="sxs-lookup"><span data-stu-id="937fd-133">Internal links</span></span>

<span data-ttu-id="937fd-134">内部链接应使用目标文件的 `uid` 和外部参照链接（链接文本设置为链接内容的标题）：</span><span class="sxs-lookup"><span data-stu-id="937fd-134">Internal links should use the `uid` of the target article with an xref link (link text is set to the linked content's title):</span></span>

```md
<xref:uid_of_the_topic>
```

<span data-ttu-id="937fd-135">如果文章标题不适合用于链接文本（例如，句子中的单词或短语是链接文本），请使用以下内容指定外部参照链接和链接文本：</span><span class="sxs-lookup"><span data-stu-id="937fd-135">If the title of the article is unsuitable for link text (for example, a word or phrase in a sentence is the link text), specify the xref link and link text with the following:</span></span>

```md
[link text](xref:uid_of_the_topic)
```

<span data-ttu-id="937fd-136">有关详细信息，请参阅 [DocFX 交叉引用](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html#cross-reference).</span><span class="sxs-lookup"><span data-stu-id="937fd-136">For more information, see the [DocFX Cross Reference](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html#cross-reference).</span></span>

## <a name="images-and-screenshots"></a><span data-ttu-id="937fd-137">图像和屏幕截图</span><span class="sxs-lookup"><span data-stu-id="937fd-137">Images and screenshots</span></span>

<span data-ttu-id="937fd-138">请勿在文章中包含图像，除非：</span><span class="sxs-lookup"><span data-stu-id="937fd-138">Don't include images with articles, except:</span></span>

* <span data-ttu-id="937fd-139">在基本的入门（初级）教程中。</span><span class="sxs-lookup"><span data-stu-id="937fd-139">In basic onboarding (beginner) tutorials.</span></span>
* <span data-ttu-id="937fd-140">需要图像辅助说明。</span><span class="sxs-lookup"><span data-stu-id="937fd-140">When an image is needed for clarity.</span></span>

<span data-ttu-id="937fd-141">这些限制可缩小存储库的大小。</span><span class="sxs-lookup"><span data-stu-id="937fd-141">These restrictions reduce the size of the repository.</span></span>

<span data-ttu-id="937fd-142">作为可选步骤，请确保文档中使用的任何图像和屏幕截图都已压缩，这有助于缩小文件大小和提高页面加载性能。</span><span class="sxs-lookup"><span data-stu-id="937fd-142">As an optional step, ensure that any images and screenshots used in the documentation are compressed, which helps with file size and page load performance.</span></span> <span data-ttu-id="937fd-143">几个常用工具包括 TinyPNG （使用 [TinyPNG 网站](https://tinypng.com/)或 [TinyPNG API](https://tinypng.com/developers)）或[图像优化器](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.ImageOptimizer) Visual Studio 扩展。</span><span class="sxs-lookup"><span data-stu-id="937fd-143">A few popular tools include TinyPNG (using the [TinyPNG website](https://tinypng.com/) or the [TinyPNG API](https://tinypng.com/developers)) or the [Image Optimizer](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.ImageOptimizer) Visual Studio extension.</span></span>

## <a name="code-snippets"></a><span data-ttu-id="937fd-144">代码片段</span><span class="sxs-lookup"><span data-stu-id="937fd-144">Code snippets</span></span>

<span data-ttu-id="937fd-145">文章经常使用代码片段来说明要点。</span><span class="sxs-lookup"><span data-stu-id="937fd-145">Articles frequently contain code snippets to illustrate points.</span></span> <span data-ttu-id="937fd-146">DFM 允许将代码复制到 Markdown 文件或引用单独的代码文件。</span><span class="sxs-lookup"><span data-stu-id="937fd-146">DFM allows you to copy code into the Markdown file or refer to a separate code file.</span></span> <span data-ttu-id="937fd-147">请尽可能使用单独的代码文件，以最大限度地减少代码中出错的可能性。</span><span class="sxs-lookup"><span data-stu-id="937fd-147">We prefer to use separate code files whenever possible to minimize the chance of errors in the code.</span></span> <span data-ttu-id="937fd-148">使用前面所述的示例项目的文件夹结构将代码文件存储在存储库中。</span><span class="sxs-lookup"><span data-stu-id="937fd-148">The code files are stored in the repository using the folder structure described earlier for sample projects.</span></span>

<span data-ttu-id="937fd-149">以下示例说明了用于 configuration/index.md 文件的 [DFM 代码片段语法](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html#code-snippet)。</span><span class="sxs-lookup"><span data-stu-id="937fd-149">The following examples illustrate [DFM code snippet syntax](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html#code-snippet) for use in a *configuration/index.md* file.</span></span>

<span data-ttu-id="937fd-150">将整个代码文件呈现为代码片段：</span><span class="sxs-lookup"><span data-stu-id="937fd-150">To render an entire code file as a snippet:</span></span>

```md
[!code-csharp[](configuration/index/sample/Program.cs)]
```

<span data-ttu-id="937fd-151">使用行号将文件的一部分呈现为代码片段：</span><span class="sxs-lookup"><span data-stu-id="937fd-151">To render a portion of a file as a snippet by using line numbers:</span></span>

```md
[!code-csharp[](configuration/index/sample/Program.cs?range=1-10,20,30,40-50]
[!code-html[](configuration/index/sample/Views/Home/Index.cshtml?range=1-10,20,30,40-50]
```

<span data-ttu-id="937fd-152">有关 C# 代码段，请参阅 [C# 区域](https://docs.microsoft.com/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-region)。</span><span class="sxs-lookup"><span data-stu-id="937fd-152">For C# snippets, reference a [C# region](https://docs.microsoft.com/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-region).</span></span> <span data-ttu-id="937fd-153">请尽可能使用区域而不是行号，因为代码文件中的行号往往会更改，并与 Markdown 中引用的行号不同步。</span><span class="sxs-lookup"><span data-stu-id="937fd-153">Whenever possible, use regions rather than line numbers because line numbers in a code file tend to change and become out of sync with line number references in Markdown.</span></span> <span data-ttu-id="937fd-154">可嵌套 C# 区域。</span><span class="sxs-lookup"><span data-stu-id="937fd-154">C# regions can be nested.</span></span> <span data-ttu-id="937fd-155">如果要引用外部区域，内部 `#region` 和 `#endregion` 指令不会呈现在代码段中。</span><span class="sxs-lookup"><span data-stu-id="937fd-155">If referencing the outer region, the inner `#region` and `#endregion` directives aren't rendered in a snippet.</span></span>

<span data-ttu-id="937fd-156">呈现名为 “snippet_Example” 的 C# 区域：</span><span class="sxs-lookup"><span data-stu-id="937fd-156">To render a C# region named "snippet_Example":</span></span>

```md
[!code-csharp[](configuration/index/sample/Program.cs?name=snippet_Example)]
```

<span data-ttu-id="937fd-157">突出显示呈现的代码段中选定的行（通常呈现为黄色背景）：</span><span class="sxs-lookup"><span data-stu-id="937fd-157">To highlight selected lines in a rendered snippet (usually renders as yellow background color):</span></span>

```md
[!code-csharp[](configuration/index/sample/Program.cs?name=snippet_Example&highlight=1-3,10,20-25)]
[!code-csharp[](configuration/index/sample/Program.cs?range=10-20&highlight=1-3]
[!code-html[](configuration/index/sample/Views/Home/Index.cshtml?range=10-20&highlight=1-3]
[!code-javascript[](configuration/index/sample/UsingOptionsSample.csproj?range=10-20&highlight=1-3]
```

## <a name="test-changes-with-docfx"></a><span data-ttu-id="937fd-158">使用 DocFX 测试更改</span><span class="sxs-lookup"><span data-stu-id="937fd-158">Test changes with DocFX</span></span>

<span data-ttu-id="937fd-159">使用 [DocFX 命令行工具](https://dotnet.github.io/docfx/tutorial/docfx_getting_started.html#2-use-docfx-as-a-command-line-tool)测试更改，这将创建站点的本地托管版本。</span><span class="sxs-lookup"><span data-stu-id="937fd-159">Test your changes with the [DocFX command-line tool](https://dotnet.github.io/docfx/tutorial/docfx_getting_started.html#2-use-docfx-as-a-command-line-tool), which creates a locally hosted version of the site.</span></span> <span data-ttu-id="937fd-160">DocFX 不呈现为 docs.microsoft.com 创建的样式和站点扩展。</span><span class="sxs-lookup"><span data-stu-id="937fd-160">DocFX doesn't render style and site extensions created for docs.microsoft.com.</span></span>

<span data-ttu-id="937fd-161">DocFX 要求：</span><span class="sxs-lookup"><span data-stu-id="937fd-161">DocFX requires:</span></span>

* <span data-ttu-id="937fd-162">Windows 上的 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="937fd-162">.NET Framework on Windows.</span></span>
* <span data-ttu-id="937fd-163">适用于 Linux 或 macOS 的 Mono。</span><span class="sxs-lookup"><span data-stu-id="937fd-163">Mono for Linux or macOS.</span></span>

### <a name="windows-instructions"></a><span data-ttu-id="937fd-164">Windows 说明</span><span class="sxs-lookup"><span data-stu-id="937fd-164">Windows instructions</span></span>

* <span data-ttu-id="937fd-165">从 [DocFX 发布](https://github.com/dotnet/docfx/releases)下载并解压缩 “docfx.zip”。</span><span class="sxs-lookup"><span data-stu-id="937fd-165">Download and unzip *docfx.zip* from [DocFX releases](https://github.com/dotnet/docfx/releases).</span></span>
* <span data-ttu-id="937fd-166">将 DocFX 添加到路径。</span><span class="sxs-lookup"><span data-stu-id="937fd-166">Add DocFX to your PATH.</span></span>
* <span data-ttu-id="937fd-167">在命令外壳中，导航到包含文件 *docfx.js* 的 *aspnet* 文件夹，并运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="937fd-167">In a command shell, navigate to the *aspnet* folder that contains the *docfx.json* file and run the following command:</span></span>

  ```console
  docfx --serve
  ```

* <span data-ttu-id="937fd-168">在浏览器中导航到 `http://localhost:8080/group1-dest/`。</span><span class="sxs-lookup"><span data-stu-id="937fd-168">In a browser, navigate to `http://localhost:8080/group1-dest/`.</span></span>

### <a name="mono-instructions"></a><span data-ttu-id="937fd-169">Mono 说明</span><span class="sxs-lookup"><span data-stu-id="937fd-169">Mono instructions</span></span>

* <span data-ttu-id="937fd-170">使用 Homebrew 安装 Mono：</span><span class="sxs-lookup"><span data-stu-id="937fd-170">Install Mono via Homebrew:</span></span>

  ```console
  brew install mono
  ```

* <span data-ttu-id="937fd-171">下载 [DocFX 的最新版本](https://github.com/dotnet/docfx/releases)。</span><span class="sxs-lookup"><span data-stu-id="937fd-171">Download the [latest version of DocFX](https://github.com/dotnet/docfx/releases).</span></span>
* <span data-ttu-id="937fd-172">将存档提取到 $HOME/bin/docfx。</span><span class="sxs-lookup"><span data-stu-id="937fd-172">Extract the archive to *$HOME/bin/docfx*.</span></span>
* <span data-ttu-id="937fd-173">在 Bash Shell 中为 docfx 创建一对别名。</span><span class="sxs-lookup"><span data-stu-id="937fd-173">Create a pair of aliases for **docfx** in a bash shell.</span></span> <span data-ttu-id="937fd-174">第一个别名用于生成文档。</span><span class="sxs-lookup"><span data-stu-id="937fd-174">The first alias is used to build the documentation.</span></span> <span data-ttu-id="937fd-175">第二个别名用于生成和提供文档。</span><span class="sxs-lookup"><span data-stu-id="937fd-175">The second alias is used to build and serve the documentation.</span></span>

  ```console
  alias docfx='mono $HOME/bin/docfx/docfx.exe'
  alias docfx-serve='mono $HOME/bin/docfx/docfx.exe --serve'
  ```

* <span data-ttu-id="937fd-176">在命令行界面中，导航到包含文件 *docfx.js* 的 *aspnet* 文件夹，并运行以下命令以通过其别名生成并提供文档：</span><span class="sxs-lookup"><span data-stu-id="937fd-176">In a command shell, navigate to the *aspnet* folder that contains the *docfx.json* file  and run the following command to build and serve the docs via its alias:</span></span>

  ```console
  docfx-serve
  ```

* <span data-ttu-id="937fd-177">在浏览器中导航到 `http://localhost:8080/group1-dest/`。</span><span class="sxs-lookup"><span data-stu-id="937fd-177">In a browser, navigate to `http://localhost:8080/group1-dest/`.</span></span>

## <a name="voice-and-tone"></a><span data-ttu-id="937fd-178">语音和声调</span><span class="sxs-lookup"><span data-stu-id="937fd-178">Voice and tone</span></span>

<span data-ttu-id="937fd-179">我们的目标是编写被广泛受众所理解的易懂文档。</span><span class="sxs-lookup"><span data-stu-id="937fd-179">Our goal is to write documentation that is easily understandable by the widest possible audience.</span></span> <span data-ttu-id="937fd-180">为此，我们编写了写作风格指南，请参与者遵守。</span><span class="sxs-lookup"><span data-stu-id="937fd-180">To that end, we established guidelines for writing style that we ask our contributors to follow.</span></span> <span data-ttu-id="937fd-181">有关详细信息，请参阅 .NET 存储库中的 [语音和音调指导原则](https://github.com/dotnet/docs/blob/main/styleguide/voice-tone.md) 。</span><span class="sxs-lookup"><span data-stu-id="937fd-181">For more information, see [Voice and tone guidelines](https://github.com/dotnet/docs/blob/main/styleguide/voice-tone.md) in the .NET repository.</span></span>

## <a name="microsoft-writing-style-guide"></a><span data-ttu-id="937fd-182">Microsoft 编写风格指南</span><span class="sxs-lookup"><span data-stu-id="937fd-182">Microsoft Writing Style Guide</span></span>

<span data-ttu-id="937fd-183">[Microsoft 编写风格指南](https://docs.microsoft.com/style-guide/welcome/)提供的编写风格和术语指南适用于所有形式的技术交流（包括 ASP.NET Core 文档）。</span><span class="sxs-lookup"><span data-stu-id="937fd-183">The [Microsoft Writing Style Guide](https://docs.microsoft.com/style-guide/welcome/) provides writing style and terminology guidance for all forms of technology communication, including the ASP.NET Core documentation.</span></span>

## <a name="redirects"></a><span data-ttu-id="937fd-184">重定向</span><span class="sxs-lookup"><span data-stu-id="937fd-184">Redirects</span></span>

<span data-ttu-id="937fd-185">如果删除某篇文章、更改文章的文件名或将其移到另一个文件夹，请创建一个重定向，确保将此项目收藏为书签的人不会收到 404 Not Found 错误。</span><span class="sxs-lookup"><span data-stu-id="937fd-185">If you delete an article, change its file name, or move it to a different folder, create a redirect so that people who bookmarked the article don't receive a *404 Not Found* error.</span></span> <span data-ttu-id="937fd-186">将重定向添加到 [主重定向文件](https://github.com/dotnet/AspNetDocs/blob/main/.openpublishing.redirection.json)。</span><span class="sxs-lookup"><span data-stu-id="937fd-186">Add redirects to the [main redirect file](https://github.com/dotnet/AspNetDocs/blob/main/.openpublishing.redirection.json).</span></span>
