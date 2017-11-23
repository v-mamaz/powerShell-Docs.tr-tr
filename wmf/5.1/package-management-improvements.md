---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, Kur
contributor: jianyunt, quoctruong
title: "WMF 5.1 içinde paket yönetimi geliştirmeleri"
ms.openlocfilehash: b55a1742530b7cd48d60d79b7d4866ebee80a3b6
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/12/2017
---
# <a name="improvements-to-package-management-in-wmf-51"></a><span data-ttu-id="e6ef0-103">WMF 5.1# içinde paket yönetimi geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="e6ef0-103">Improvements to Package Management in WMF 5.1#</span></span>

## <a name="improvements-in-packagemanagement"></a><span data-ttu-id="e6ef0-104">PackageManagement yenilikleri</span><span class="sxs-lookup"><span data-stu-id="e6ef0-104">Improvements in PackageManagement</span></span> ##
<span data-ttu-id="e6ef0-105">WMF 5.1 yapılan düzeltmeler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e6ef0-105">The following are the fixes made in the WMF 5.1:</span></span> 

### <a name="version-alias"></a><span data-ttu-id="e6ef0-106">Sürüm diğer adı</span><span class="sxs-lookup"><span data-stu-id="e6ef0-106">Version Alias</span></span>

<span data-ttu-id="e6ef0-107">**Senaryo**: sürüm 1.0 ve 2.0, sisteminizde yüklü bir paketin P1, sahip olduğunuz ve sürüm 1.0 kaldırmak istediğiniz, şunu çalıştırırsınız: `Uninstall-Package -Name P1 -Version 1.0` ve sürüm 1.0 cmdlet'ini çalıştırdıktan sonra kaldırılması için bekler.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-107">**Scenario**: If you have version 1.0 and 2.0 of a package, P1, installed on your system, and you want to uninstall version 1.0, you would run `Uninstall-Package -Name P1 -Version 1.0` and expect version 1.0 to be uninstalled after running the cmdlet.</span></span> <span data-ttu-id="e6ef0-108">Ancak sonucu 2.0 sürümünün kaldırılması.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-108">However the result is that version 2.0 gets uninstalled.</span></span>  
    
<span data-ttu-id="e6ef0-109">Bu kaynaklanır `-Version` parametredir bir diğer ad `-MinimumVersion` parametresi.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-109">This occurs because the `-Version` parameter is an alias of the `-MinimumVersion` parameter.</span></span> <span data-ttu-id="e6ef0-110">En düşük sürüm 1.0 olan tam bir paket için PackageManagement bakıldığında, en son sürümünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-110">When PackageManagement is looking for a qualified package with the minimum version of 1.0, it returns the latest version.</span></span> <span data-ttu-id="e6ef0-111">Bu normal durumlarda istenilen sonucu genellikle en yeni sürüm olduğundan bulma için beklenen davranıştır.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-111">This behavior is expected in normal cases because finding the latest version is usually the desired result.</span></span> <span data-ttu-id="e6ef0-112">Ancak, bunun uygulanması gereken değil `Uninstall-Package` durumda.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-112">However, it should not apply to the `Uninstall-Package` case.</span></span>
    
<span data-ttu-id="e6ef0-113">**Çözüm**: kaldırılan `-Version` tamamen PackageManagement diğer adı (paketini</span><span class="sxs-lookup"><span data-stu-id="e6ef0-113">**Solution**:removed `-Version` alias entirely in PackageManagement (a.k.a.</span></span> <span data-ttu-id="e6ef0-114">OneGet) ve PowerShellGet.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-114">OneGet) and PowerShellGet.</span></span> 

### <a name="multiple-prompts-for-bootstrapping-the-nuget-provider"></a><span data-ttu-id="e6ef0-115">NuGet sağlayıcısı önyükleme için birden çok komut istemleri</span><span class="sxs-lookup"><span data-stu-id="e6ef0-115">Multiple prompts for bootstrapping the NuGet provider</span></span>

<span data-ttu-id="e6ef0-116">**Senaryo**: çalıştırdığınızda `Find-Module` veya `Install-Module` veya diğer PackageManagement cmdlet'leri PackageManagement ilk kez bilgisayarınızda NuGet sağlayıcı bootstrap dener.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-116">**Scenario**: When you run `Find-Module` or `Install-Module` or other PackageManagement cmdlets on your computer for the first time, PackageManagement tries to bootstrap the NuGet provider.</span></span> <span data-ttu-id="e6ef0-117">PowerShellGet sağlayıcısı NuGet sağlayıcısı ayrıca PowerShell modülleri indirmek için kullandığı için bunu yapar.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-117">It does this because the PowerShellGet provider also uses the NuGet provider to download PowerShell modules.</span></span> <span data-ttu-id="e6ef0-118">PackageManagement ardından kullanıcıdan NuGet Sağlayıcısı'nı yüklemek izin ister.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-118">PackageManagement then prompts the user for permission to install the NuGet provider.</span></span> <span data-ttu-id="e6ef0-119">Kullanıcı önyüklemesi için "Evet" seçtikten sonra NuGet sağlayıcısının son sürümünün yüklenecek.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-119">After the user selects "yes" for the bootstrapping, the latest version of the NuGet provider will be installed.</span></span> 
    
<span data-ttu-id="e6ef0-120">Bilgisayarınızda yüklü NuGet Sağlayıcısı'nın eski bir sürümü varsa, ancak bazı durumlarda, eski sürümü NuGet bazen ilk (yani PackageManagement yarış durumu) PowerShell oturumuna yüklenen.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-120">However, in some cases, when you have an old version of NuGet provider installed on your computer, the older version of NuGet sometimes gets loaded first into the PowerShell session (that's the race condition in PackageManagement).</span></span> <span data-ttu-id="e6ef0-121">Ancak PowerShellGet NuGet sağlayıcısı yeniden bootstrap PackageManagement ister şekilde PowerShellGet çalışmak için NuGet provider'ın sonraki bir sürümünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-121">However PowerShellGet requires the later version of the NuGet provider to work, so PowerShellGet asks PackageManagement to bootstrap the NuGet provider again.</span></span> <span data-ttu-id="e6ef0-122">Bu, NuGet sağlayıcısı önyükleme için birden çok komut istemlerini sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-122">This results in multiple prompts for bootstrapping the NuGet provider.</span></span>

<span data-ttu-id="e6ef0-123">**Çözüm**: WMF5.1 içinde PackageManagement NuGet sağlayıcısı önyükleme için birden çok komut istemlerini önlemek için NuGet Sağlayıcısı'nın en son sürümü yükler.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-123">**Solution**: In WMF5.1, PackageManagement loads the latest version of the NuGet provider to avoid multiple prompts for bootstrapping the NuGet provider.</span></span>

<span data-ttu-id="e6ef0-124">Aynı zamanda bu sorunu çözmek, NuGet sağlayıcı (NuGet-Anycpu.exe) eski sürümü el ile silerek sorunu var. $env: ProgramFiles\PackageManagement\ProviderAssemblies $env: LOCALAPPDATA\PackageManagement\ProviderAssemblies</span><span class="sxs-lookup"><span data-stu-id="e6ef0-124">You could also work around this issue by manually deleting the old version of the NuGet provider (NuGet-Anycpu.exe) if exists from $env:ProgramFiles\PackageManagement\ProviderAssemblies $env:LOCALAPPDATA\PackageManagement\ProviderAssemblies</span></span>


### <a name="support-for-packagemanagement-on-computers-with-intranet-access-only"></a><span data-ttu-id="e6ef0-125">Yalnızca Intranet erişimi olan bilgisayarlarda PackageManagement için destek</span><span class="sxs-lookup"><span data-stu-id="e6ef0-125">Support for PackageManagement on computers with Intranet access only</span></span>

<span data-ttu-id="e6ef0-126">**Senaryo**: Kurumsal senaryo için bir ortamı altında Kişiler çalıştığınız söz konusu olduğunda hiçbir Internet erişimi ancak Intranet yalnızca.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-126">**Scenario**: For the enterprise scenario, people are working under an environment where there is no Internet access but Intranet only.</span></span> <span data-ttu-id="e6ef0-127">PackageManagement bu durumda WMF 5.0 desteklememektedir.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-127">PackageManagement did not support this case in WMF 5.0.</span></span>

<span data-ttu-id="e6ef0-128">**Senaryo**: içinde WMF 5.0, PackageManagement desteği yalnızca Intranet (ancak Internet'değil) sahip bilgisayarların erişim.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-128">**Scenario**: In WMF 5.0, PackageManagement did not support computers that have only Intranet (but not Internet) access.</span></span>

<span data-ttu-id="e6ef0-129">**Çözüm**: WMF 5.1'nde, Intranet bilgisayarların PackageManagement kullanmasına izin vermek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="e6ef0-129">**Solution**: In WMF 5.1, you can follow these steps to allow Intranet computers to use PackageManagement:</span></span>

1. <span data-ttu-id="e6ef0-130">NuGet sağlayıcıyı kullanarak bir Internet bağlantısı olan başka bir bilgisayara kullanarak karşıdan `Install-PackageProvider -Name NuGet`.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-130">Download the NuGet provider using another computer that has an Internet connection by using `Install-PackageProvider -Name NuGet`.</span></span>

2. <span data-ttu-id="e6ef0-131">NuGet sağlayıcısı ya da altında Bul `$env:ProgramFiles\PackageManagement\ProviderAssemblies\nuget` veya `$env:LOCALAPPDATA\PackageManagement\ProviderAssemblies\nuget`.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-131">Find the NuGet provider under either `$env:ProgramFiles\PackageManagement\ProviderAssemblies\nuget`  or  `$env:LOCALAPPDATA\PackageManagement\ProviderAssemblies\nuget`.</span></span>

3. <span data-ttu-id="e6ef0-132">Intranet bilgisayarına erişmek ve NuGet sağlayıcısıyla yüklemek bir klasör veya ağ paylaşımı konumu ikili dosyaları kopyalamak `Install-PackageProvider -Name NuGet -Source <Path to folder>`.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-132">Copy the binaries to a folder or network share location that the Intranet computer can access, and then install the NuGet provider with `Install-PackageProvider -Name NuGet -Source <Path to folder>`.</span></span>


### <a name="event-logging-improvements"></a><span data-ttu-id="e6ef0-133">Olay günlüğü geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="e6ef0-133">Event logging improvements</span></span>

<span data-ttu-id="e6ef0-134">Paketleri yüklediğinizde, bilgisayarın durumunu değiştiriyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-134">When you install packages, you are changing the state of the computer.</span></span> <span data-ttu-id="e6ef0-135">WMF 5.1 PackageManagement şimdi olayları için Windows olay günlüğüne kaydeder `Install-Package`, `Uninstall-Package`, ve `Save-Package` etkinlikler.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-135">In WMF 5.1, PackageManagement now logs events to the Windows event log for `Install-Package`, `Uninstall-Package`, and `Save-Package` activities.</span></span> <span data-ttu-id="e6ef0-136">Olay günlüğü PowerShell, diğer bir deyişle, aynıdır `Microsoft-Windows-PowerShell, Operational`.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-136">The Event log  is the same as for PowerShell, that is, `Microsoft-Windows-PowerShell, Operational`.</span></span>

### <a name="support-for-basic-authentication"></a><span data-ttu-id="e6ef0-137">Temel kimlik doğrulaması için destek</span><span class="sxs-lookup"><span data-stu-id="e6ef0-137">Support for basic authentication</span></span>

<span data-ttu-id="e6ef0-138">WMF 5.1, bulma ve temel kimlik doğrulaması gerektiren bir depodan paketler yükleme PackageManagement destekler.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-138">In WMF 5.1, PackageManagement supports finding and installing packages from a repository that requires basic authentication.</span></span> <span data-ttu-id="e6ef0-139">Kimlik bilgilerinizi sağlamanız `Find-Package` ve `Install-Package` cmdlet'leri.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-139">You can supply your credentials to the `Find-Package` and `Install-Package` cmdlets.</span></span> <span data-ttu-id="e6ef0-140">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="e6ef0-140">For example:</span></span>

``` PowerShell
Find-Package -Source <SourceWithCredential> -Credential (Get-Credential)
```
### <a name="support-for-using-packagemanagement-behind-a-proxy"></a><span data-ttu-id="e6ef0-141">Bir proxy'nin arkasında PackageManagement kullanma desteği</span><span class="sxs-lookup"><span data-stu-id="e6ef0-141">Support for using PackageManagement behind a proxy</span></span>

<span data-ttu-id="e6ef0-142">WMF 5.1 PackageManagement şimdi yeni proxy kullandığı parametreler `-ProxyCredential` ve `-Proxy`.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-142">In WMF 5.1, PackageManagement now takes new proxy parameters `-ProxyCredential` and `-Proxy`.</span></span> <span data-ttu-id="e6ef0-143">Bu parametreleri kullanarak proxy URL'si ve PackageManagement cmdlet'leri için kimlik bilgileri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-143">Using these parameters, you can specify the proxy URL and credentials to PackageManagement cmdlets.</span></span> <span data-ttu-id="e6ef0-144">Varsayılan olarak, sistem proxy ayarları kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e6ef0-144">By default, system proxy settings are used.</span></span> <span data-ttu-id="e6ef0-145">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="e6ef0-145">For example:</span></span>

``` PowerShell
Find-Package -Source http://www.nuget.org/api/v2/ -Proxy http://www.myproxyserver.com -ProxyCredential (Get-Credential)
```
