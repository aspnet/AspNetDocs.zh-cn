---
uid: web-pages/overview/api-reference/asp-net-web-pages-api-reference
title: ASP.NET 网页 (Razor) API 快速参考 |Microsoft Docs
author: Rick-Anderson
description: 此页包含一个列表，其中列出了使用 Razor 语法编程 ASP.NET 网页的最常用对象、属性和方法。
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 4001cb9b-3bfd-4ace-8a89-1561d8421e2c
msc.legacyurl: /web-pages/overview/api-reference/asp-net-web-pages-api-reference
msc.type: authoredcontent
ms.openlocfilehash: e010307fc0576e8b003fbfe665cae77618d9c9a5
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345245"
---
# <a name="aspnet-web-pages-razor-api-quick-reference"></a>ASP.NET 网页 (Razor) API 快速参考

 作者 [Tom FitzMacken](https://github.com/tfitzmac)

> 此页包含一个列表，其中列出了使用 Razor 语法编程 ASP.NET 网页的最常用对象、属性和方法。
> 
> ASP.NET 网页版本2中引入了标记为 " (v2) " 的说明。
> 
> 有关 API 参考文档，请参阅 MSDN 上的 [ASP.NET 网页参考文档](https://go.microsoft.com/fwlink/?LinkId=208659) 。
> 
> ## <a name="software-versions"></a>软件版本
> 
> 
> -  (Razor) ASP.NET 网页
>   
> 
> 本教程还适用于 ASP.NET 网页2和 ASP.NET 网页 1.0 (（标记为 v2) 的功能除外）。

本页包含以下内容的参考信息：

- [Classes](#Classes)
- [数据](#Data)
- [帮助程序](#Helpers)
- [验证](#Validation)

<a id="Classes"></a>
## <a name="classes"></a>类

### `AppState[key], AppState[index],App`

包含应用程序中的任何页可以共享的数据。 可以使用动态 `App` 属性访问相同的数据，如以下示例中所示：

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

将字符串值转换为布尔值 (true/false) 。 如果字符串不表示 true/false，则返回 false 或指定值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

将字符串值转换为日期/时间。 `DateTime.MinValue`如果字符串不表示日期/时间，则返回或指定值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

将字符串值转换为十进制值。 如果字符串不表示十进制值，则返回0.0 或指定值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

将字符串值转换为 float。 如果字符串不表示十进制值，则返回0.0 或指定值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

将字符串值转换为整数。 如果字符串不表示整数，则返回0或指定值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

使用可选的附加路径部分，从本地文件路径创建与浏览器兼容的 URL。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

将 *值* 呈现为 html 标记，而不是将其呈现为 html 编码的输出。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

如果可以将值从字符串转换为指定类型，则返回 true。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

如果对象或变量没有值，则返回 true。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

如果请求是 POST，则返回 true。  (初始请求通常是 GET。 ) 

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

指定要应用于此页的布局页的路径。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

包含当前请求中的页面、布局页和部分页面之间共享的数据。 可以使用动态 `Page` 属性访问相同的数据，如以下示例中所示：

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

 (布局页) 呈现不在任何命名节中的内容页的内容。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

使用指定的路径和可选的额外数据呈现内容页。 可以按位置获取额外参数的值 `PageData` (示例 1) 或 (example 2) 的键。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

 (布局页) 呈现包含名称的内容节。 如果 *设置为* false，则将节设置为可选。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

获取或设置 HTTP cookie 的值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

获取在当前请求中上载的文件。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

以) 形式 (形式获取作为字符串发布的窗体中的数据。 `Request[key]` 检查 `Request.Form` 和 `Request.QueryString` 集合。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

获取在 URL 查询字符串中指定的数据。 `Request[key]` 检查 `Request.Form` 和 `Request.QueryString` 集合。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

有选择地禁用对窗体元素、查询字符串值、cookie 或标头值的请求验证。 默认情况下，请求验证处于启用状态，并阻止用户发布标记或其他可能危险的内容。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

将 HTTP 服务器标头添加到响应。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

在指定的时间缓存页面输出。 （可选）将 *滑动* 设置为在每个页面访问时重置超时值，并为页面请求中的每个不同的查询字符串 *varyByParams* 缓存不同版本的页面。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

将浏览器请求重定向到新位置。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

设置发送到浏览器的 HTTP 状态代码。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

使用可选的 MIME 类型将 *数据* 的内容写入响应。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

将文件的内容写入响应。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

 (布局页) 定义具有名称的内容节。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

对 HTML 编码的字符串进行解码。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

对字符串进行编码以便在 HTML 标记中呈现。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

返回指定虚拟路径的服务器物理路径。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

解码 URL 中的文本。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

对要置于 URL 中的文本进行编码。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

获取或设置一个值，该值在用户关闭浏览器之前一直存在。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

显示对象值的字符串表示形式。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

从 URL (获取其他数据，例如 */MyPage/ExtraData*) 。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

更改指定用户的密码。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

使用帐户确认令牌确认帐户。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

使用指定的用户名和密码创建新的用户帐户。 若要要求确认令牌，请为 RequireConfirmationToken 传递 true *。*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

获取当前已登录用户的整数标识符。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

获取当前已登录用户的名称。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

生成可通过电子邮件发送给用户的密码重置令牌，以便用户可以重置密码。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

返回用户名中的用户 ID。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

如果当前用户已登录，则返回 true。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

如果用户已被确认 (例如，通过确认电子邮件) ，则返回 true。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

如果当前用户的名称与指定的用户名相匹配，则返回 true。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

通过在 cookie 中设置身份验证令牌，在中记录用户。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

通过删除身份验证令牌 cookie 来注销用户。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

如果用户未经过身份验证，请将 HTTP 状态设置为 401（未经授权）。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

如果当前用户不是指定角色之一的成员，则会将 HTTP 状态设置为 401 (未授权) 。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

如果当前用户不是 *用户名*指定的用户，则会将 HTTP 状态设置为 401 (未授权) 。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

如果密码重置令牌有效，则将用户的密码更改为新密码。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a>数据

### `Database.Execute(SQLstatement [,parameters]`

使用可选参数执行 *SQLstatement* () 例如 INSERT、DELETE 或 UPDATE，并返回受影响的记录的计数。

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

返回最近插入的行中的标识列。

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

使用 *Web.config* 文件中的命名连接字符串打开指定的数据库文件或指定的数据库。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

使用连接字符串打开数据库。  (这与进行比较 `Database.Open` ，后者使用连接字符串名称。 ) 

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

使用 *SQLstatement* 查询数据库 (可以选择传递参数) 并以集合的形式返回结果。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

使用可选参数) 执行 *SQLstatement* (并返回单个记录。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

使用可选参数) 执行 *SQLstatement* (并返回单个值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a>帮助程序

### `Analytics.GetGoogleHtml(webPropertyId)`

呈现指定 ID 的 Google Analytics JavaScript 代码。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

呈现指定项目的 StatCounter 分析 JavaScript 代码。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

为指定的帐户呈现 Yahoo Analytics JavaScript 代码。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

将搜索传递到必应。 若要指定要搜索的站点以及搜索框的标题，可以设置 `Bing.SiteUrl` 和 `Bing.SiteTitle` 属性。 通常在* \_ AppStart*页中设置这些属性。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

初始化图表。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

将图例添加到图表中。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

向图表中添加一系列值。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

返回指定数据的哈希值。 默认算法为 `sha256` 。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

允许 Facebook 用户连接到页面。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

呈现用于上载文件的 UI。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

呈现指定的 Xbox 游戏玩家标记。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

呈现指定电子邮件地址的 Gravatar 图像。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

将数据对象转换为 JavaScript 对象表示法 (JSON) 格式的字符串。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

将 JSON 编码的输入字符串转换为数据对象，您可以循环访问该数据对象或将其插入到数据库中。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

使用指定的标题和可选 URL 呈现社交网络链接。

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

将错误消息与表单域相关联。 使用 `ModelState` 帮助器来访问此成员。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

将错误消息与窗体相关联。 使用 `ModelState` 帮助器来访问此成员。

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

如果没有验证错误，则返回 true。 使用 `ModelState` 帮助器来访问此成员。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

呈现对象和任何子对象的属性和值。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

呈现 reCAPTCHA 验证测试。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

为 reCAPTCHA 服务设置公钥和私钥。 通常在* \_ AppStart*页中设置这些属性。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

返回 reCAPTCHA 测试的结果。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

呈现有关 ASP.NET 网页的状态信息。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

呈现指定用户的 Twitter 流。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

为指定的搜索文本呈现 Twitter 流。

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

为具有可选宽度和高度的指定文件呈现 Flash 视频播放器。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

为具有可选宽度和高度的指定文件呈现 Windows Media player。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

使用所需的宽度和高度为指定的 *.xap* 文件呈现 Silverlight 播放机。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

返回由 *键*指定的对象; 如果未找到该对象，则返回 null。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

从缓存中移除由 *键* 指定的对象。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

将 *值* 放入缓存中由 *键*指定的名称下。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

`WebGrid`使用查询中的数据创建新的对象。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

呈现标记以显示 HTML 表中的数据。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

呈现对象的页导航 `WebGrid` 。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

从指定的路径加载图像。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

将指定的图像作为水印添加。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

向图像添加指定的文本。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

水平或垂直翻转图像。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

在文件上传过程中将图像发布到页面时，将加载图像。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

调整图像大小。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

向左或向右旋转图像。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

将图像保存到指定的路径。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

设置 SMTP 服务器的密码。 通常，在 " * \_ AppStart* " 页中设置此属性。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

发送电子邮件。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

设置 SMTP 服务器名称。 通常，在 " * \_ AppStart* " 页中设置此属性。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

设置 SMTP 服务器的用户名。 通常应在* \_ AppStart*页中设置此属性。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a>验证

### `Html.ValidationMessage(field)`

 (v2) 呈现指定字段的验证错误消息。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

 (v2) 显示所有验证错误的列表。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

 (v2) 将用户输入元素注册到指定的验证类型。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

 (v2) 动态呈现客户端验证的 CSS 类属性，以便您可以设置验证错误消息的格式。  (要求你引用适当的客户端脚本库，并定义 CSS 类。 ) 

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

 (v2) 启用用户输入字段的客户端验证。  (要求你引用适当的客户端脚本库。 ) 

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

如果 registred 验证的所有用户输入元素都包含有效值，则 (v2) 返回 true。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

 (v2) 指定用户必须为用户输入元素提供一个值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

 (v2) 指定用户必须提供每个用户输入元素的值。 此方法不允许您指定自定义错误消息。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample114.html)]

### `Validator.DateTime ([error message])`  
`Validator.Decimal([error message])`  
`Validator.EqualsTo(otherField,[error message])`  
`Validator.Float([error message])`  
`Validator.Integer([error message])`  
`Validator.Range(min,max [, error message])`  
`Validator.RegEx(pattern[, error message])`  
`Validator.Required([error message])`  
`Validator.StringLength(length)`  
`Validator.Url([error message])`

 (v2) 在使用方法时指定验证测试 `Validation.Add` 。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
