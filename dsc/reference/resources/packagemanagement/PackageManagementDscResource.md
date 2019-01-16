---
ms.date: 06/20/2018
keywords: DSC, powershell, yapılandırma, Kurulum
title: DSC PackageManagement kaynak
ms.openlocfilehash: 18cbbfe0715c82dcfdf4a5fb6ee36ee814e43d3b
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048720"
---
# <a name="dsc-packagemanagement-resource"></a><span data-ttu-id="38aea-103">DSC PackageManagement kaynak</span><span class="sxs-lookup"><span data-stu-id="38aea-103">DSC PackageManagement Resource</span></span>

<span data-ttu-id="38aea-104">Şunun için geçerlidir: Windows PowerShell 4.0, Windows PowerShell 5.0, 5.1 Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="38aea-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0, Windows PowerShell 5.1</span></span>

<span data-ttu-id="38aea-105">**PackageManagement** kaynak olarak Windows PowerShell Desired State Configuration (DSC) yüklemek veya bir hedef düğümde paket yönetim paketlerini kaldırmak için bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="38aea-105">The **PackageManagement** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to install or uninstall Package Management packages on a target node.</span></span> <span data-ttu-id="38aea-106">Bu kaynak gerektiriyor **PackageManagement** modülü, kullanılabilir [ http://PowerShellGallery.com ](http://PowerShellGallery.com).</span><span class="sxs-lookup"><span data-stu-id="38aea-106">This resource requires the **PackageManagement** module, available from [http://PowerShellGallery.com](http://PowerShellGallery.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="38aea-107">**PackageManagement** modülü olmalıdır en az sürüm 1.1.7.0 doğru olması aşağıdaki özellik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="38aea-107">The **PackageManagement** module should be at least version 1.1.7.0 for the following property information to be correct.</span></span>

## <a name="syntax"></a><span data-ttu-id="38aea-108">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="38aea-108">Syntax</span></span>

```
PackageManagement [string] #ResourceName
{
    Name = [string]
    [AdditionalParameters = [HashTable]]
    [DependsOn = [string[]]]
    [Ensure = [string]{ Absent | Present }]
    [MaximumVersion = [string]]
    [MinimumVersion = [string]]
    [ProviderName = [string]]
    [PsDscRunAsCredential = [PSCredential]]
    [RequiredVersion = [string]]
    [Source = [string]]
    [SourceCredential = [PSCredential]]
}
```

## <a name="properties"></a><span data-ttu-id="38aea-109">Özellikler</span><span class="sxs-lookup"><span data-stu-id="38aea-109">Properties</span></span>

| <span data-ttu-id="38aea-110">Özellik</span><span class="sxs-lookup"><span data-stu-id="38aea-110">Property</span></span> | <span data-ttu-id="38aea-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="38aea-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="38aea-112">Ad</span><span class="sxs-lookup"><span data-stu-id="38aea-112">Name</span></span>| <span data-ttu-id="38aea-113">Yüklenecek veya için paket adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="38aea-113">Specifies the name of the Package to be installed or uninstalled.</span></span>|
| <span data-ttu-id="38aea-114">AdditionalParameters</span><span class="sxs-lookup"><span data-stu-id="38aea-114">AdditionalParameters</span></span>| <span data-ttu-id="38aea-115">Sağlayıcı belirli hashtable için geçirilir parametrelerinin `Get-Package -AdditionalArguments`.</span><span class="sxs-lookup"><span data-stu-id="38aea-115">Provider specific hashtable of parameters that would be passed to `Get-Package -AdditionalArguments`.</span></span> <span data-ttu-id="38aea-116">Örneğin, NuGet sağlayıcısı DestinationPath gibi ek parametreler geçirebilir.</span><span class="sxs-lookup"><span data-stu-id="38aea-116">For example, for NuGet provider you can pass additional parameters like DestinationPath.</span></span>|
| <span data-ttu-id="38aea-117">Emin olun</span><span class="sxs-lookup"><span data-stu-id="38aea-117">Ensure</span></span>| <span data-ttu-id="38aea-118">Paket yüklü veya kaldırılmış olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="38aea-118">Determines whether the package is to be installed or uninstalled.</span></span>|
| <span data-ttu-id="38aea-119">MaximumVersion</span><span class="sxs-lookup"><span data-stu-id="38aea-119">MaximumVersion</span></span>|<span data-ttu-id="38aea-120">Bulmak istediğiniz paketin sürümü izin verilen üst sınırı belirtir.</span><span class="sxs-lookup"><span data-stu-id="38aea-120">Specifies the maximum allowed version of the package that you want to find.</span></span> <span data-ttu-id="38aea-121">Bu parametreyi eklemezseniz, kaynak paketin en yüksek kullanılabilir sürümü bulur.</span><span class="sxs-lookup"><span data-stu-id="38aea-121">If you do not add this parameter, the resource finds the highest available version of the package.</span></span>|
| <span data-ttu-id="38aea-122">MinimumVersion</span><span class="sxs-lookup"><span data-stu-id="38aea-122">MinimumVersion</span></span>|<span data-ttu-id="38aea-123">Bulmak istediğiniz paketin sürümü izin verilen en düşük belirtir.</span><span class="sxs-lookup"><span data-stu-id="38aea-123">Specifies the minimum allowed version of the package that you want to find.</span></span> <span data-ttu-id="38aea-124">Bu parametreyi eklemezseniz, yüksek kullanılabilir sürümü tarafından belirtilen en yüksek herhangi belirtilen sürümü de karşılayan kaynak bulan _MaximumVersion_ parametresi.</span><span class="sxs-lookup"><span data-stu-id="38aea-124">If you do not add this parameter, the resource finds the highest available version of the package that also satisfies any maximum specified version specified by the _MaximumVersion_ parameter.</span></span>|
| <span data-ttu-id="38aea-125">ProviderName</span><span class="sxs-lookup"><span data-stu-id="38aea-125">ProviderName</span></span>| <span data-ttu-id="38aea-126">Paket aramanızın kapsamını yapılacak bir paket sağlayıcı adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="38aea-126">Specifies a package provider name to which to scope your package search.</span></span> <span data-ttu-id="38aea-127">Çalıştırarak paketin sağlayıcısı adlarını alabilirsiniz `Get-PackageProvider` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="38aea-127">You can get package provider names by running the `Get-PackageProvider` cmdlet.</span></span>|
| <span data-ttu-id="38aea-128">RequiredVersion</span><span class="sxs-lookup"><span data-stu-id="38aea-128">RequiredVersion</span></span>| <span data-ttu-id="38aea-129">Yüklemek istediğiniz paketin'ün tam sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="38aea-129">Specifies the exact version of the package that you want to install.</span></span> <span data-ttu-id="38aea-130">Bu parametreyi belirtmezseniz, bu DSC kaynağı tarafından belirtilen herhangi bir en yüksek sürümü de karşılayan paket kullanılabilir en yeni sürümü yükler _MaximumVersion_ parametresi.</span><span class="sxs-lookup"><span data-stu-id="38aea-130">If you do not specify this parameter, this DSC resource installs the newest available version of the package that also satisfies any maximum version specified by the _MaximumVersion_ parameter.</span></span>|
| <span data-ttu-id="38aea-131">Kaynak</span><span class="sxs-lookup"><span data-stu-id="38aea-131">Source</span></span>| <span data-ttu-id="38aea-132">Paket bulunabileceği paket kaynağının adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="38aea-132">Specifies the name of the package source where the package can be found.</span></span> <span data-ttu-id="38aea-133">Bu bir URI olabilir veya bir kaynak kayıtlı `Register-PackageSource` veya PackageManagementSource DSC kaynağı.</span><span class="sxs-lookup"><span data-stu-id="38aea-133">This can either be a URI or a source registered with `Register-PackageSource` or PackageManagementSource DSC resource.</span></span>|
| <span data-ttu-id="38aea-134">SourceCredential</span><span class="sxs-lookup"><span data-stu-id="38aea-134">SourceCredential</span></span> | <span data-ttu-id="38aea-135">Belirtilen paket sağlayıcısı veya kaynak için bir paket yüklemek için haklarına sahip bir kullanıcı hesabı belirtir.</span><span class="sxs-lookup"><span data-stu-id="38aea-135">Specifies a user account that has rights to install a package for a specified package provider or source.</span></span>|

## <a name="additional-parameters"></a><span data-ttu-id="38aea-136">Ek parametreler</span><span class="sxs-lookup"><span data-stu-id="38aea-136">Additional Parameters</span></span>

<span data-ttu-id="38aea-137">Aşağıdaki tabloda, AdditionalParameters özelliği için seçenekleri listeler.</span><span class="sxs-lookup"><span data-stu-id="38aea-137">The following table lists options for the AdditionalParameters property.</span></span>

| <span data-ttu-id="38aea-138">Parametre</span><span class="sxs-lookup"><span data-stu-id="38aea-138">Parameter</span></span> | <span data-ttu-id="38aea-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="38aea-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="38aea-140">DestinationPath</span><span class="sxs-lookup"><span data-stu-id="38aea-140">DestinationPath</span></span>| <span data-ttu-id="38aea-141">Yerleşik Nuget sağlayıcısı gibi sağlayıcıları tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="38aea-141">Used by providers such as the built-in Nuget Provider.</span></span> <span data-ttu-id="38aea-142">Yüklenecek paket istediğiniz bir dosya konumu belirtir.</span><span class="sxs-lookup"><span data-stu-id="38aea-142">Specifies a file location where you want the package to be installed.</span></span>|
| <span data-ttu-id="38aea-143">InstallationPolicy</span><span class="sxs-lookup"><span data-stu-id="38aea-143">InstallationPolicy</span></span>| <span data-ttu-id="38aea-144">Yerleşik Nuget sağlayıcısı gibi sağlayıcıları tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="38aea-144">Used by providers such as the built-in Nuget Provider.</span></span> <span data-ttu-id="38aea-145">Kaynak paketin güvendiğiniz olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="38aea-145">Determines whether you trust the package's source.</span></span> <span data-ttu-id="38aea-146">Şunlardan biri: `Untrusted`, `Trusted`.</span><span class="sxs-lookup"><span data-stu-id="38aea-146">One of: `Untrusted`, `Trusted`.</span></span>|

## <a name="example"></a><span data-ttu-id="38aea-147">Örnek</span><span class="sxs-lookup"><span data-stu-id="38aea-147">Example</span></span>

<span data-ttu-id="38aea-148">Bu örnek yükler **JQuery** NuGet paketi ve **GistProvider** PowerShell modülünü kullanarak **PackageManagement** DSC kaynağı.</span><span class="sxs-lookup"><span data-stu-id="38aea-148">This example installs the **JQuery** NuGet package and **GistProvider** PowerShell module using the **PackageManagement** DSC resource.</span></span> <span data-ttu-id="38aea-149">Bu örnekte, önce gerekli paket kaynakları kullanılabilir sonra beklenen durumunu tanımlar sağlar **JQuery** ve **GistProvider** paketleri (NuGet ve PowerShell, sırasıyla).</span><span class="sxs-lookup"><span data-stu-id="38aea-149">This example first ensures the required package sources are available then defines the expected state of the **JQuery** and **GistProvider** packages (NuGet and PowerShell, respectively).</span></span>

```powershell
Configuration PackageTest
{
    PackageManagementSource SourceRepository
    {
        Ensure      = "Present"
        Name        = "MyNuget"
        ProviderName= "Nuget"
        SourceLocation   = "http://nuget.org/api/v2/"
        InstallationPolicy ="Trusted"
    }

    PackageManagementSource PSGallery
    {
        Ensure      = "Present"
        Name        = "psgallery"
        ProviderName= "PowerShellGet"
        SourceLocation   = "https://www.powershellgallery.com/api/v2/"
        InstallationPolicy ="Trusted"
    }

    PackageManagement NugetPackage
    {
        Ensure               = "Present"
        Name                 = "JQuery"
        AdditionalParameters = "$env:HomeDrive\nuget"
        RequiredVersion      = "2.0.1"
        DependsOn            = "[PackageManagementSource]SourceRepository"
    }

    PackageManagement PSModule
    {
        Ensure               = "Present"
        Name                 = "gistprovider"
        Source               = "PSGallery"
        DependsOn            = "[PackageManagementSource]PSGallery"
    }
}
```