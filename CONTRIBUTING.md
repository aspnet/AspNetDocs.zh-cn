# <a name="contribute-to-the-aspnet-documentation"></a>参与 ASP.NET 文档

本文档介绍了参与到 [ASP.NET 文档站点](https://docs.microsoft.com/aspnet/)上托管的文章和代码示例中的过程。 欢迎更正拼写错误以及撰写新文章。

## <a name="how-to-make-a-simple-correction-or-suggestion"></a>如何提出简单的更正或建议

文章作为 Markdown 文件存储在存储库中。 通过选择浏览器窗口右上角的“编辑”链接，可以在浏览器中对 Markdown 文件的内容进行简单更改。 （在窄浏览器窗口中，展开“选项”栏，以查看“编辑”链接 。）按照说明创建拉取请求 (PR)。 我们将对拉取请求进行评审并接受相关请求或提出更改建议。

## <a name="how-to-make-a-more-complex-submission"></a>如何提出更复杂的提交

需要对 [Git 和 GitHub.com](https://guides.github.com/activities/hello-world/) 有基本的理解。

* 创建一个[问题](https://github.com/dotnet/AspNetDocs/issues/new)，描述你想要执行的操作，例如更改现有项目或创建一个新项目。 我们经常要求提供新主题建议的大纲。 请等待团队批准后再投入时间参与进来。
* 将 [dotnet/AspNetDocs](https://github.com/dotnet/AspNetDocs/) 存储库分叉，并为更改创建分支。
* 使用所做的更改向 *主* 分支提交 PR。
* 如果拉取请求分配的标签为 “cla-required”，则[完成贡献许可协议 (CLA)](https://cla.dotnetfoundation.org/)。
* 对 PR 请求反馈进行响应。

有关此过程引导发布新文章的示例，请参阅 .NET Docs 存储库中的[问题&num; 67 ](https://github.com/dotnet/docs/issues/67)和[拉取请求&num; 798](https://github.com/dotnet/docs/pull/798)。 新文章为[编写代码](https://docs.microsoft.com/dotnet/articles/csharp/codedoc)。

## <a name="docs-authoring-pack-extension-in-visual-studio-code"></a>Visual Studio Code 中的 Docs 创作包扩展

如果使用 Visual Studio Code 参与到 ASP.NET 文档中，可以通过安装 [Docs 创作包](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack)扩展来提高工作效率。 该扩展提供各种有助于 Markdown 语法检查、代码拼写检查和项目模板的工具。

## <a name="markdown-syntax"></a>Markdown 语法

文章采用 [DocFx 风格的 Markdown](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html) 编写，它是 [GitHub 风格的 Markdown (GFM)](https://guides.github.com/features/mastering-markdown/) 的超集。 有关 ASP.NET 文档中常用的 UI 功能的 DFM 语法示例，请参阅 .NET 文档存储库样式指南中的 [元数据和 Markdown 模板](https://github.com/dotnet/docs/blob/main/styleguide/template.md) 。

## <a name="folder-structure-conventions"></a>文件夹结构约定

对于每个Markdown 文件，可能存在图像文件夹和示例代码文件夹。 如果项目是 [signalr/概述/高级/依赖关系-注入](https://github.com/dotnet/AspNetDocs/blob/main/aspnet/signalr/overview/advanced/dependency-injection.md)，则图像处于 [signalr/概述/高级/依赖关系注入/ \_ 静态](https://github.com/dotnet/AspNetDocs/tree/main/aspnet/signalr/overview/advanced/dependency-injection/_static) ，示例应用项目文件位于 [signalr/概述/高级/依赖关系注入/示例](https://github.com/dotnet/AspNetDocs/tree/main/aspnet/signalr/overview/advanced/dependency-injection/samples)中。 *Signalr/概述/advanced/依赖关系注入* 文件中的图像由以下 Markdown 呈现：

```md
![description of image for alt attribute](dependency-injection/_static/image1.png)
```

所有图像都应具有[替代 (alt) 文本](https://wikipedia.org/wiki/Alt_attribute)。 有关指定替代文本的建议，请参阅在线资源，例如 [WebAIM：替代文本](https://webaim.org/techniques/alttext/)。

Markdown 文件名称和图像文件名称使用小写。

## <a name="internal-links"></a>内部链接

内部链接应使用目标文件的 `uid` 和外部参照链接（链接文本设置为链接内容的标题）：

```md
<xref:uid_of_the_topic>
```

如果文章标题不适合用于链接文本（例如，句子中的单词或短语是链接文本），请使用以下内容指定外部参照链接和链接文本：

```md
[link text](xref:uid_of_the_topic)
```

有关详细信息，请参阅 [DocFX 交叉引用](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html#cross-reference).

## <a name="images-and-screenshots"></a>图像和屏幕截图

请勿在文章中包含图像，除非：

* 在基本的入门（初级）教程中。
* 需要图像辅助说明。

这些限制可缩小存储库的大小。

作为可选步骤，请确保文档中使用的任何图像和屏幕截图都已压缩，这有助于缩小文件大小和提高页面加载性能。 几个常用工具包括 TinyPNG （使用 [TinyPNG 网站](https://tinypng.com/)或 [TinyPNG API](https://tinypng.com/developers)）或[图像优化器](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.ImageOptimizer) Visual Studio 扩展。

## <a name="code-snippets"></a>代码片段

文章经常使用代码片段来说明要点。 DFM 允许将代码复制到 Markdown 文件或引用单独的代码文件。 请尽可能使用单独的代码文件，以最大限度地减少代码中出错的可能性。 使用前面所述的示例项目的文件夹结构将代码文件存储在存储库中。

以下示例说明了用于 configuration/index.md 文件的 [DFM 代码片段语法](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html#code-snippet)。

将整个代码文件呈现为代码片段：

```md
[!code-csharp[](configuration/index/sample/Program.cs)]
```

使用行号将文件的一部分呈现为代码片段：

```md
[!code-csharp[](configuration/index/sample/Program.cs?range=1-10,20,30,40-50]
[!code-html[](configuration/index/sample/Views/Home/Index.cshtml?range=1-10,20,30,40-50]
```

有关 C# 代码段，请参阅 [C# 区域](https://docs.microsoft.com/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-region)。 请尽可能使用区域而不是行号，因为代码文件中的行号往往会更改，并与 Markdown 中引用的行号不同步。 可嵌套 C# 区域。 如果要引用外部区域，内部 `#region` 和 `#endregion` 指令不会呈现在代码段中。

呈现名为 “snippet_Example” 的 C# 区域：

```md
[!code-csharp[](configuration/index/sample/Program.cs?name=snippet_Example)]
```

突出显示呈现的代码段中选定的行（通常呈现为黄色背景）：

```md
[!code-csharp[](configuration/index/sample/Program.cs?name=snippet_Example&highlight=1-3,10,20-25)]
[!code-csharp[](configuration/index/sample/Program.cs?range=10-20&highlight=1-3]
[!code-html[](configuration/index/sample/Views/Home/Index.cshtml?range=10-20&highlight=1-3]
[!code-javascript[](configuration/index/sample/UsingOptionsSample.csproj?range=10-20&highlight=1-3]
```

## <a name="test-changes-with-docfx"></a>使用 DocFX 测试更改

使用 [DocFX 命令行工具](https://dotnet.github.io/docfx/tutorial/docfx_getting_started.html#2-use-docfx-as-a-command-line-tool)测试更改，这将创建站点的本地托管版本。 DocFX 不呈现为 docs.microsoft.com 创建的样式和站点扩展。

DocFX 要求：

* Windows 上的 .NET Framework。
* 适用于 Linux 或 macOS 的 Mono。

### <a name="windows-instructions"></a>Windows 说明

* 从 [DocFX 发布](https://github.com/dotnet/docfx/releases)下载并解压缩 “docfx.zip”。
* 将 DocFX 添加到路径。
* 在命令外壳中，导航到包含文件 *docfx.js* 的 *aspnet* 文件夹，并运行以下命令：

  ```console
  docfx --serve
  ```

* 在浏览器中导航到 `http://localhost:8080/group1-dest/`。

### <a name="mono-instructions"></a>Mono 说明

* 使用 Homebrew 安装 Mono：

  ```console
  brew install mono
  ```

* 下载 [DocFX 的最新版本](https://github.com/dotnet/docfx/releases)。
* 将存档提取到 $HOME/bin/docfx。
* 在 Bash Shell 中为 docfx 创建一对别名。 第一个别名用于生成文档。 第二个别名用于生成和提供文档。

  ```console
  alias docfx='mono $HOME/bin/docfx/docfx.exe'
  alias docfx-serve='mono $HOME/bin/docfx/docfx.exe --serve'
  ```

* 在命令行界面中，导航到包含文件 *docfx.js* 的 *aspnet* 文件夹，并运行以下命令以通过其别名生成并提供文档：

  ```console
  docfx-serve
  ```

* 在浏览器中导航到 `http://localhost:8080/group1-dest/`。

## <a name="voice-and-tone"></a>语音和声调

我们的目标是编写被广泛受众所理解的易懂文档。 为此，我们编写了写作风格指南，请参与者遵守。 有关详细信息，请参阅 .NET 存储库中的 [语音和音调指导原则](https://github.com/dotnet/docs/blob/main/styleguide/voice-tone.md) 。

## <a name="microsoft-writing-style-guide"></a>Microsoft 编写风格指南

[Microsoft 编写风格指南](https://docs.microsoft.com/style-guide/welcome/)提供的编写风格和术语指南适用于所有形式的技术交流（包括 ASP.NET Core 文档）。

## <a name="redirects"></a>重定向

如果删除某篇文章、更改文章的文件名或将其移到另一个文件夹，请创建一个重定向，确保将此项目收藏为书签的人不会收到 404 Not Found 错误。 将重定向添加到 [主重定向文件](https://github.com/dotnet/AspNetDocs/blob/main/.openpublishing.redirection.json)。
