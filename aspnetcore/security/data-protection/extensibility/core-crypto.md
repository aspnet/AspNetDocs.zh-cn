---
title: 在 ASP.NET Core 中的核心加密可扩展性
author: rick-anderson
description: 了解有关 IAuthenticatedEncryptor、 IAuthenticatedEncryptorDescriptor、 IAuthenticatedEncryptorDescriptorDeserializer 和顶级工厂。
ms.author: riande
ms.date: 8/11/2017
uid: security/data-protection/extensibility/core-crypto
ms.openlocfilehash: 47432cfefe0a52c9f815d717f7269ec68fdb6af3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036174"
---
# <a name="core-cryptography-extensibility-in-aspnet-core"></a><span data-ttu-id="11002-103">在 ASP.NET Core 中的核心加密可扩展性</span><span class="sxs-lookup"><span data-stu-id="11002-103">Core cryptography extensibility in ASP.NET Core</span></span>

<a name="data-protection-extensibility-core-crypto"></a>

>[!WARNING]
> <span data-ttu-id="11002-104">实现以下接口的任何类型应该是线程安全的多个调用方。</span><span class="sxs-lookup"><span data-stu-id="11002-104">Types that implement any of the following interfaces should be thread-safe for multiple callers.</span></span>

<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptor"></a>

## <a name="iauthenticatedencryptor"></a><span data-ttu-id="11002-105">IAuthenticatedEncryptor</span><span class="sxs-lookup"><span data-stu-id="11002-105">IAuthenticatedEncryptor</span></span>

<span data-ttu-id="11002-106">**IAuthenticatedEncryptor**接口是加密子系统的基本构建基块。</span><span class="sxs-lookup"><span data-stu-id="11002-106">The **IAuthenticatedEncryptor** interface is the basic building block of the cryptographic subsystem.</span></span> <span data-ttu-id="11002-107">通常是每个密钥，一个 IAuthenticatedEncryptor 和 IAuthenticatedEncryptor 实例将对所有加密密钥材料和算法执行加密操作所需的信息。</span><span class="sxs-lookup"><span data-stu-id="11002-107">There's generally one IAuthenticatedEncryptor per key, and the IAuthenticatedEncryptor instance wraps all cryptographic key material and algorithmic information necessary to perform cryptographic operations.</span></span>

<span data-ttu-id="11002-108">顾名思义，类型为负责提供经过身份验证的加密和解密服务。</span><span class="sxs-lookup"><span data-stu-id="11002-108">As its name suggests, the type is responsible for providing authenticated encryption and decryption services.</span></span> <span data-ttu-id="11002-109">它会公开以下两个 Api。</span><span class="sxs-lookup"><span data-stu-id="11002-109">It exposes the following two APIs.</span></span>

* <span data-ttu-id="11002-110">Decrypt(ArraySegment<byte> ciphertext, ArraySegment<byte> additionalAuthenticatedData) : byte[]</span><span class="sxs-lookup"><span data-stu-id="11002-110">Decrypt(ArraySegment<byte> ciphertext, ArraySegment<byte> additionalAuthenticatedData) : byte[]</span></span>

* <span data-ttu-id="11002-111">Encrypt(ArraySegment<byte> plaintext, ArraySegment<byte> additionalAuthenticatedData) : byte[]</span><span class="sxs-lookup"><span data-stu-id="11002-111">Encrypt(ArraySegment<byte> plaintext, ArraySegment<byte> additionalAuthenticatedData) : byte[]</span></span>

<span data-ttu-id="11002-112">加密方法将返回的 blob，包括到加密的纯文本和身份验证的标记。</span><span class="sxs-lookup"><span data-stu-id="11002-112">The Encrypt method returns a blob that includes the enciphered plaintext and an authentication tag.</span></span> <span data-ttu-id="11002-113">尽管 AAD 本身不需要是可恢复最后一个有效负载中域的身份验证标记必须包含的附加经过身份验证的数据 (AAD)。</span><span class="sxs-lookup"><span data-stu-id="11002-113">The authentication tag must encompass the additional authenticated data (AAD), though the AAD itself need not be recoverable from the final payload.</span></span> <span data-ttu-id="11002-114">解密方法验证的身份验证标记，并返回被解码的有效负载。</span><span class="sxs-lookup"><span data-stu-id="11002-114">The Decrypt method validates the authentication tag and returns the deciphered payload.</span></span> <span data-ttu-id="11002-115">应为 CryptographicException homogenized （除 ArgumentNullException 和类似） 的所有失败。</span><span class="sxs-lookup"><span data-stu-id="11002-115">All failures (except ArgumentNullException and similar) should be homogenized to CryptographicException.</span></span>

> [!NOTE]
> <span data-ttu-id="11002-116">实际上，IAuthenticatedEncryptor 实例本身不需要包含密钥材料。</span><span class="sxs-lookup"><span data-stu-id="11002-116">The IAuthenticatedEncryptor instance itself doesn't actually need to contain the key material.</span></span> <span data-ttu-id="11002-117">例如，实现可以将委托到 HSM 中的所有操作。</span><span class="sxs-lookup"><span data-stu-id="11002-117">For example, the implementation could delegate to an HSM for all operations.</span></span>

<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptorfactory"></a>
<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor"></a>

## <a name="how-to-create-an-iauthenticatedencryptor"></a><span data-ttu-id="11002-118">如何创建 IAuthenticatedEncryptor</span><span class="sxs-lookup"><span data-stu-id="11002-118">How to create an IAuthenticatedEncryptor</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="11002-119">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="11002-119">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="11002-120">**IAuthenticatedEncryptorFactory**接口表示一种类型，知道如何创建[IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor)实例。</span><span class="sxs-lookup"><span data-stu-id="11002-120">The **IAuthenticatedEncryptorFactory** interface represents a type that knows how to create an [IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor) instance.</span></span> <span data-ttu-id="11002-121">其 API 是按如下所示。</span><span class="sxs-lookup"><span data-stu-id="11002-121">Its API is as follows.</span></span>

* <span data-ttu-id="11002-122">CreateEncryptorInstance （IKey 密钥）：IAuthenticatedEncryptor</span><span class="sxs-lookup"><span data-stu-id="11002-122">CreateEncryptorInstance(IKey key) : IAuthenticatedEncryptor</span></span>

<span data-ttu-id="11002-123">对于任何给定的 IKey 实例，其 CreateEncryptorInstance 方法创建的任何经过身份验证的加密应被视为等效，如下面的代码示例。</span><span class="sxs-lookup"><span data-stu-id="11002-123">For any given IKey instance, any authenticated encryptors created by its CreateEncryptorInstance method should be considered equivalent, as in the below code sample.</span></span>

```csharp
// we have an IAuthenticatedEncryptorFactory instance and an IKey instance
IAuthenticatedEncryptorFactory factory = ...;
IKey key = ...;

// get an encryptor instance and perform an authenticated encryption operation
ArraySegment<byte> plaintext = new ArraySegment<byte>(Encoding.UTF8.GetBytes("plaintext"));
ArraySegment<byte> aad = new ArraySegment<byte>(Encoding.UTF8.GetBytes("AAD"));
var encryptor1 = factory.CreateEncryptorInstance(key);
byte[] ciphertext = encryptor1.Encrypt(plaintext, aad);

// get another encryptor instance and perform an authenticated decryption operation
var encryptor2 = factory.CreateEncryptorInstance(key);
byte[] roundTripped = encryptor2.Decrypt(new ArraySegment<byte>(ciphertext), aad);


// the 'roundTripped' and 'plaintext' buffers should be equivalent
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="11002-124">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="11002-124">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="11002-125">**IAuthenticatedEncryptorDescriptor**接口表示一种类型，知道如何创建[IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor)实例。</span><span class="sxs-lookup"><span data-stu-id="11002-125">The **IAuthenticatedEncryptorDescriptor** interface represents a type that knows how to create an [IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor) instance.</span></span> <span data-ttu-id="11002-126">其 API 是按如下所示。</span><span class="sxs-lookup"><span data-stu-id="11002-126">Its API is as follows.</span></span>

* <span data-ttu-id="11002-127">CreateEncryptorInstance():IAuthenticatedEncryptor</span><span class="sxs-lookup"><span data-stu-id="11002-127">CreateEncryptorInstance() : IAuthenticatedEncryptor</span></span>

* <span data-ttu-id="11002-128">ExportToXml():XmlSerializedDescriptorInfo</span><span class="sxs-lookup"><span data-stu-id="11002-128">ExportToXml() : XmlSerializedDescriptorInfo</span></span>

<span data-ttu-id="11002-129">如 IAuthenticatedEncryptor，假定的 IAuthenticatedEncryptorDescriptor 实例包装一个特定键。</span><span class="sxs-lookup"><span data-stu-id="11002-129">Like IAuthenticatedEncryptor, an instance of IAuthenticatedEncryptorDescriptor is assumed to wrap one specific key.</span></span> <span data-ttu-id="11002-130">这意味着，对于任何给定的 IAuthenticatedEncryptorDescriptor 实例，其 CreateEncryptorInstance 方法创建的任何经过身份验证的加密应视为等效的如下面的代码示例。</span><span class="sxs-lookup"><span data-stu-id="11002-130">This means that for any given IAuthenticatedEncryptorDescriptor instance, any authenticated encryptors created by its CreateEncryptorInstance method should be considered equivalent, as in the below code sample.</span></span>

```csharp
// we have an IAuthenticatedEncryptorDescriptor instance
IAuthenticatedEncryptorDescriptor descriptor = ...;

// get an encryptor instance and perform an authenticated encryption operation
ArraySegment<byte> plaintext = new ArraySegment<byte>(Encoding.UTF8.GetBytes("plaintext"));
ArraySegment<byte> aad = new ArraySegment<byte>(Encoding.UTF8.GetBytes("AAD"));
var encryptor1 = descriptor.CreateEncryptorInstance();
byte[] ciphertext = encryptor1.Encrypt(plaintext, aad);

// get another encryptor instance and perform an authenticated decryption operation
var encryptor2 = descriptor.CreateEncryptorInstance();
byte[] roundTripped = encryptor2.Decrypt(new ArraySegment<byte>(ciphertext), aad);


// the 'roundTripped' and 'plaintext' buffers should be equivalent
```

---

<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor"></a>

## <a name="iauthenticatedencryptordescriptor-aspnet-core-2x-only"></a><span data-ttu-id="11002-131">IAuthenticatedEncryptorDescriptor （ASP.NET Core 2.x 仅）</span><span class="sxs-lookup"><span data-stu-id="11002-131">IAuthenticatedEncryptorDescriptor (ASP.NET Core 2.x only)</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="11002-132">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="11002-132">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="11002-133">**IAuthenticatedEncryptorDescriptor**接口表示知道如何将自身导出到 XML 的类型。</span><span class="sxs-lookup"><span data-stu-id="11002-133">The **IAuthenticatedEncryptorDescriptor** interface represents a type that knows how to export itself to XML.</span></span> <span data-ttu-id="11002-134">其 API 是按如下所示。</span><span class="sxs-lookup"><span data-stu-id="11002-134">Its API is as follows.</span></span>

* <span data-ttu-id="11002-135">ExportToXml():XmlSerializedDescriptorInfo</span><span class="sxs-lookup"><span data-stu-id="11002-135">ExportToXml() : XmlSerializedDescriptorInfo</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="11002-136">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="11002-136">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

---

## <a name="xml-serialization"></a><span data-ttu-id="11002-137">XML 序列化</span><span class="sxs-lookup"><span data-stu-id="11002-137">XML Serialization</span></span>

<span data-ttu-id="11002-138">IAuthenticatedEncryptor 和 IAuthenticatedEncryptorDescriptor 的主要区别是描述符，知道如何创建加密程序并提供有效的参数。</span><span class="sxs-lookup"><span data-stu-id="11002-138">The primary difference between IAuthenticatedEncryptor and IAuthenticatedEncryptorDescriptor is that the descriptor knows how to create the encryptor and supply it with valid arguments.</span></span> <span data-ttu-id="11002-139">请考虑其实现依赖于 SymmetricAlgorithm 和 KeyedHashAlgorithm IAuthenticatedEncryptor。</span><span class="sxs-lookup"><span data-stu-id="11002-139">Consider an IAuthenticatedEncryptor whose implementation relies on SymmetricAlgorithm and KeyedHashAlgorithm.</span></span> <span data-ttu-id="11002-140">加密程序的作业是使用这些类型，但它并不一定知道这些类型原来所在的位置，因此它不能真正写出如何重新创建自身的应用程序重启时的正确描述。</span><span class="sxs-lookup"><span data-stu-id="11002-140">The encryptor's job is to consume these types, but it doesn't necessarily know where these types came from, so it can't really write out a proper description of how to recreate itself if the application restarts.</span></span> <span data-ttu-id="11002-141">描述符可作为在此基础上更高的级别。</span><span class="sxs-lookup"><span data-stu-id="11002-141">The descriptor acts as a higher level on top of this.</span></span> <span data-ttu-id="11002-142">因为描述符知道如何创建加密器实例 （例如，它知道如何创建所需的算法），以便可以重新创建加密程序实例，应用程序重置后，它可以序列化这一知识以 XML 格式。</span><span class="sxs-lookup"><span data-stu-id="11002-142">Since the descriptor knows how to create the encryptor instance (e.g., it knows how to create the required algorithms), it can serialize that knowledge in XML form so that the encryptor instance can be recreated after an application reset.</span></span>

<a name="data-protection-extensibility-core-crypto-exporttoxml"></a>

<span data-ttu-id="11002-143">通过其 ExportToXml 例程，描述符可序列化。</span><span class="sxs-lookup"><span data-stu-id="11002-143">The descriptor can be serialized via its ExportToXml routine.</span></span> <span data-ttu-id="11002-144">此例程返回 XmlSerializedDescriptorInfo 其中包含两个属性： 描述符和表示的类型的 XElement 表示形式[IAuthenticatedEncryptorDescriptorDeserializer](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptordeserializer)可以是用于提供相应的 XElement 此描述符继续研究下去。</span><span class="sxs-lookup"><span data-stu-id="11002-144">This routine returns an XmlSerializedDescriptorInfo which contains two properties: the XElement representation of the descriptor and the Type which represents an [IAuthenticatedEncryptorDescriptorDeserializer](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptordeserializer) which can be used to resurrect this descriptor given the corresponding XElement.</span></span>

<span data-ttu-id="11002-145">序列化的描述符可能包含敏感信息，如加密密钥材料。</span><span class="sxs-lookup"><span data-stu-id="11002-145">The serialized descriptor may contain sensitive information such as cryptographic key material.</span></span> <span data-ttu-id="11002-146">数据保护系统必须对其具有永久保存到存储之前加密信息的内置支持。</span><span class="sxs-lookup"><span data-stu-id="11002-146">The data protection system has built-in support for encrypting information before it's persisted to storage.</span></span> <span data-ttu-id="11002-147">若要这样做的优点，描述符应将标记包含敏感信息的属性名称"requiresEncryption"的元素 (xmlns"<http://schemas.asp.net/2015/03/dataProtection>")，值"true"。</span><span class="sxs-lookup"><span data-stu-id="11002-147">To take advantage of this, the descriptor should mark the element which contains sensitive information with the attribute name "requiresEncryption" (xmlns "<http://schemas.asp.net/2015/03/dataProtection>"), value "true".</span></span>

>[!TIP]
> <span data-ttu-id="11002-148">没有用于将此属性设置的帮助器 API。</span><span class="sxs-lookup"><span data-stu-id="11002-148">There's a helper API for setting this attribute.</span></span> <span data-ttu-id="11002-149">调用 XElement.MarkAsRequiresEncryption() 位于命名空间 Microsoft.AspNetCore.DataProtection.AuthenticatedEncryption.ConfigurationModel 中的扩展方法。</span><span class="sxs-lookup"><span data-stu-id="11002-149">Call the extension method XElement.MarkAsRequiresEncryption() located in namespace Microsoft.AspNetCore.DataProtection.AuthenticatedEncryption.ConfigurationModel.</span></span>

<span data-ttu-id="11002-150">也可以是其中的序列化的描述符不包含敏感信息的情况。</span><span class="sxs-lookup"><span data-stu-id="11002-150">There can also be cases where the serialized descriptor doesn't contain sensitive information.</span></span> <span data-ttu-id="11002-151">再次考虑在 HSM 中存储的加密密钥的大小写。</span><span class="sxs-lookup"><span data-stu-id="11002-151">Consider again the case of a cryptographic key stored in an HSM.</span></span> <span data-ttu-id="11002-152">序列化本身由于 HSM 就不会暴露的材料以纯文本形式时，描述符不能写出的密钥材料。</span><span class="sxs-lookup"><span data-stu-id="11002-152">The descriptor cannot write out the key material when serializing itself since the HSM won't expose the material in plaintext form.</span></span> <span data-ttu-id="11002-153">相反，描述符可能写出的版本密钥包装的密钥 （如果 HSM 允许以这种方式导出） 或密钥的 HSM 的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="11002-153">Instead, the descriptor might write out the key-wrapped version of the key (if the HSM allows export in this fashion) or the HSM's own unique identifier for the key.</span></span>

<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptordeserializer"></a>

## <a name="iauthenticatedencryptordescriptordeserializer"></a><span data-ttu-id="11002-154">IAuthenticatedEncryptorDescriptorDeserializer</span><span class="sxs-lookup"><span data-stu-id="11002-154">IAuthenticatedEncryptorDescriptorDeserializer</span></span>

<span data-ttu-id="11002-155">**IAuthenticatedEncryptorDescriptorDeserializer**接口表示知道如何从 XElement IAuthenticatedEncryptorDescriptor 实例反序列化的类型。</span><span class="sxs-lookup"><span data-stu-id="11002-155">The **IAuthenticatedEncryptorDescriptorDeserializer** interface represents a type that knows how to deserialize an IAuthenticatedEncryptorDescriptor instance from an XElement.</span></span> <span data-ttu-id="11002-156">它公开了一个方法：</span><span class="sxs-lookup"><span data-stu-id="11002-156">It exposes a single method:</span></span>

* <span data-ttu-id="11002-157">ImportFromXml （XElement 元素）：IAuthenticatedEncryptorDescriptor</span><span class="sxs-lookup"><span data-stu-id="11002-157">ImportFromXml(XElement element) : IAuthenticatedEncryptorDescriptor</span></span>

<span data-ttu-id="11002-158">ImportFromXml 方法将返回的 XElement [IAuthenticatedEncryptorDescriptor.ExportToXml](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-exporttoxml)和创建的原始 IAuthenticatedEncryptorDescriptor 等效。</span><span class="sxs-lookup"><span data-stu-id="11002-158">The ImportFromXml method takes the XElement that was returned by [IAuthenticatedEncryptorDescriptor.ExportToXml](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-exporttoxml) and creates an equivalent of the original IAuthenticatedEncryptorDescriptor.</span></span>

<span data-ttu-id="11002-159">类型实现 IAuthenticatedEncryptorDescriptorDeserializer 应具有以下两个公共构造函数之一：</span><span class="sxs-lookup"><span data-stu-id="11002-159">Types which implement IAuthenticatedEncryptorDescriptorDeserializer should have one of the following two public constructors:</span></span>

* <span data-ttu-id="11002-160">.ctor(IServiceProvider)</span><span class="sxs-lookup"><span data-stu-id="11002-160">.ctor(IServiceProvider)</span></span>

* <span data-ttu-id="11002-161">.ctor()</span><span class="sxs-lookup"><span data-stu-id="11002-161">.ctor()</span></span>

> [!NOTE]
> <span data-ttu-id="11002-162">传递给构造函数的 IServiceProvider 可能为 null。</span><span class="sxs-lookup"><span data-stu-id="11002-162">The IServiceProvider passed to the constructor may be null.</span></span>

## <a name="the-top-level-factory"></a><span data-ttu-id="11002-163">顶级工厂</span><span class="sxs-lookup"><span data-stu-id="11002-163">The top-level factory</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="11002-164">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="11002-164">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="11002-165">**AlgorithmConfiguration**类表示的类型： 它知道如何创建[IAuthenticatedEncryptorDescriptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor)实例。</span><span class="sxs-lookup"><span data-stu-id="11002-165">The **AlgorithmConfiguration** class represents a type which knows how to create [IAuthenticatedEncryptorDescriptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor) instances.</span></span> <span data-ttu-id="11002-166">它公开一个 API。</span><span class="sxs-lookup"><span data-stu-id="11002-166">It exposes a single API.</span></span>

* <span data-ttu-id="11002-167">CreateNewDescriptor():IAuthenticatedEncryptorDescriptor</span><span class="sxs-lookup"><span data-stu-id="11002-167">CreateNewDescriptor() : IAuthenticatedEncryptorDescriptor</span></span>

<span data-ttu-id="11002-168">AlgorithmConfiguration 视为顶级工厂。</span><span class="sxs-lookup"><span data-stu-id="11002-168">Think of AlgorithmConfiguration as the top-level factory.</span></span> <span data-ttu-id="11002-169">配置可作为模板。</span><span class="sxs-lookup"><span data-stu-id="11002-169">The configuration serves as a template.</span></span> <span data-ttu-id="11002-170">它包装算法的信息 （例如，此配置生成使用 AES-128-GCM 主密钥描述符），但它尚不支持与特定键相关联。</span><span class="sxs-lookup"><span data-stu-id="11002-170">It wraps algorithmic information (e.g., this configuration produces descriptors with an AES-128-GCM master key), but it's not yet associated with a specific key.</span></span>

<span data-ttu-id="11002-171">当调用 CreateNewDescriptor、 仅用于此调用中，创建新的密钥材料，并且生成新 IAuthenticatedEncryptorDescriptor 其包装此密钥材料和所需使用材料的算法信息。</span><span class="sxs-lookup"><span data-stu-id="11002-171">When CreateNewDescriptor is called, fresh key material is created solely for this call, and a new IAuthenticatedEncryptorDescriptor is produced which wraps this key material and the algorithmic information required to consume the material.</span></span> <span data-ttu-id="11002-172">无法在软件中创建 （和保存在内存中） 的密钥材料，它可以创建并保留在 HSM 中，依次类推。</span><span class="sxs-lookup"><span data-stu-id="11002-172">The key material could be created in software (and held in memory), it could be created and held within an HSM, and so on.</span></span> <span data-ttu-id="11002-173">关键点是到 CreateNewDescriptor 任何两个调用应永远不会创建等效 IAuthenticatedEncryptorDescriptor 实例。</span><span class="sxs-lookup"><span data-stu-id="11002-173">The crucial point is that any two calls to CreateNewDescriptor should never create equivalent IAuthenticatedEncryptorDescriptor instances.</span></span>

<span data-ttu-id="11002-174">AlgorithmConfiguration 类型如充当密钥创建例程的入口点[自动密钥滚动](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling)。</span><span class="sxs-lookup"><span data-stu-id="11002-174">The AlgorithmConfiguration type serves as the entry point for key creation routines such as [automatic key rolling](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling).</span></span> <span data-ttu-id="11002-175">若要更改所有将来密钥的实现，设置在 KeyManagementOptions AuthenticatedEncryptorConfiguration 属性。</span><span class="sxs-lookup"><span data-stu-id="11002-175">To change the implementation for all future keys, set the AuthenticatedEncryptorConfiguration property in KeyManagementOptions.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="11002-176">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="11002-176">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="11002-177">**IAuthenticatedEncryptorConfiguration**接口表示的类型： 它知道如何创建[IAuthenticatedEncryptorDescriptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor)实例。</span><span class="sxs-lookup"><span data-stu-id="11002-177">The **IAuthenticatedEncryptorConfiguration** interface represents a type which knows how to create [IAuthenticatedEncryptorDescriptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor) instances.</span></span> <span data-ttu-id="11002-178">它公开一个 API。</span><span class="sxs-lookup"><span data-stu-id="11002-178">It exposes a single API.</span></span>

* <span data-ttu-id="11002-179">CreateNewDescriptor():IAuthenticatedEncryptorDescriptor</span><span class="sxs-lookup"><span data-stu-id="11002-179">CreateNewDescriptor() : IAuthenticatedEncryptorDescriptor</span></span>

<span data-ttu-id="11002-180">IAuthenticatedEncryptorConfiguration 视为顶级工厂。</span><span class="sxs-lookup"><span data-stu-id="11002-180">Think of IAuthenticatedEncryptorConfiguration as the top-level factory.</span></span> <span data-ttu-id="11002-181">配置可作为模板。</span><span class="sxs-lookup"><span data-stu-id="11002-181">The configuration serves as a template.</span></span> <span data-ttu-id="11002-182">它包装算法的信息 （例如，此配置生成使用 AES-128-GCM 主密钥描述符），但它尚不支持与特定键相关联。</span><span class="sxs-lookup"><span data-stu-id="11002-182">It wraps algorithmic information (e.g., this configuration produces descriptors with an AES-128-GCM master key), but it's not yet associated with a specific key.</span></span>

<span data-ttu-id="11002-183">当调用 CreateNewDescriptor、 仅用于此调用中，创建新的密钥材料，并且生成新 IAuthenticatedEncryptorDescriptor 其包装此密钥材料和所需使用材料的算法信息。</span><span class="sxs-lookup"><span data-stu-id="11002-183">When CreateNewDescriptor is called, fresh key material is created solely for this call, and a new IAuthenticatedEncryptorDescriptor is produced which wraps this key material and the algorithmic information required to consume the material.</span></span> <span data-ttu-id="11002-184">无法在软件中创建 （和保存在内存中） 的密钥材料，它可以创建并保留在 HSM 中，依次类推。</span><span class="sxs-lookup"><span data-stu-id="11002-184">The key material could be created in software (and held in memory), it could be created and held within an HSM, and so on.</span></span> <span data-ttu-id="11002-185">关键点是到 CreateNewDescriptor 任何两个调用应永远不会创建等效 IAuthenticatedEncryptorDescriptor 实例。</span><span class="sxs-lookup"><span data-stu-id="11002-185">The crucial point is that any two calls to CreateNewDescriptor should never create equivalent IAuthenticatedEncryptorDescriptor instances.</span></span>

<span data-ttu-id="11002-186">IAuthenticatedEncryptorConfiguration 类型如充当密钥创建例程的入口点[自动密钥滚动](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling)。</span><span class="sxs-lookup"><span data-stu-id="11002-186">The IAuthenticatedEncryptorConfiguration type serves as the entry point for key creation routines such as [automatic key rolling](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling).</span></span> <span data-ttu-id="11002-187">若要更改所有将来密钥的实现，请在服务容器中注册的单一实例 IAuthenticatedEncryptorConfiguration。</span><span class="sxs-lookup"><span data-stu-id="11002-187">To change the implementation for all future keys, register a singleton IAuthenticatedEncryptorConfiguration in the service container.</span></span>

---
