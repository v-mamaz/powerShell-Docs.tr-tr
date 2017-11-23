---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: Galeri, powershell, cmdlet, psget
title: modulewithpseditionsupport
ms.openlocfilehash: 8122756b78e18fe55daef5c46dc299b87ddcaf1a
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/12/2017
---
# <a name="modules-with-compatible-powershell-editions"></a><span data-ttu-id="c236f-103">Modüller ile uyumlu PowerShell sürümleri</span><span class="sxs-lookup"><span data-stu-id="c236f-103">Modules with compatible PowerShell Editions</span></span>
<span data-ttu-id="c236f-104">Sürüm 5.1’den başlayarak, PowerShell çeşitli özellik kümelerini ve platform uyumluluğunu belirten farklı sürümler halinde sağlanır.</span><span class="sxs-lookup"><span data-stu-id="c236f-104">Starting with version 5.1, PowerShell is available in different editions which denote varying feature sets and platform compatibility.</span></span>

- <span data-ttu-id="c236f-105">**Masaüstü Sürümü:** .NET Framework üzerine yapılandırılmıştır ve Windows’un Sunucu Çekirdeği ve Windows Masaüstü gibi tam boyutlu sürümlerinde çalışan PowerShell sürümlerinin hedeflendiği betikler ve modüllerle uyumluluk sağlar.</span><span class="sxs-lookup"><span data-stu-id="c236f-105">**Desktop Edition:** Built on .NET Framework and provides compatibility with scripts and modules targeting versions of PowerShell running on full footprint editions of Windows such as Server Core and Windows Desktop.</span></span>
- <span data-ttu-id="c236f-106">**Çekirdek Sürümü:** .NET Core üzerine yapılandırılmıştır ve Windows’un Nano Sunucu ve Windows IoT gibi azaltılmış boyutlu sürümlerinde çalışan PowerShell sürümlerinin hedeflendiği betikler ve modüllerle uyumluluk sağlar.</span><span class="sxs-lookup"><span data-stu-id="c236f-106">**Core Edition:** Built on .NET Core and provides compatibility with scripts and modules targeting versions of PowerShell running on reduced footprint editions of Windows such as Nano Server and Windows IoT.</span></span>

## <a name="the-running-edition-of-powershell-is-shown-in-the-psedition-property-of-psversiontable"></a><span data-ttu-id="c236f-107">PowerShell’in çalışan sürümü, $PSVersionTable’ın PSEdition özelliğinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="c236f-107">The running edition of PowerShell is shown in the PSEdition property of $PSVersionTable.</span></span>
```powershell
$PSVersionTable

Name                           Value
----                           -----
PSVersion                      5.1.14300.1000
PSEdition                      Desktop
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
CLRVersion                     4.0.30319.42000
BuildVersion                   10.0.14300.1000
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
SerializationVersion           1.1.0.1
```

## <a name="module-authors-can-declare-their-modules-to-be-compatible-with-one-or-more-powershell-editions-using-the-compatiblepseditions-module-manifest-key-this-key-is-only-supported-on-powershell-51-or-later"></a><span data-ttu-id="c236f-108">Modül yazarları CompatiblePSEditions modül bildirim anahtarını kullanarak kendi modüllerinin bir veya birden çok PowerShell sürümüyle uyumlu olduğunu bildirebilir.</span><span class="sxs-lookup"><span data-stu-id="c236f-108">Module authors can declare their modules to be compatible with one or more PowerShell editions using the CompatiblePSEditions module manifest key.</span></span> <span data-ttu-id="c236f-109">Bu anahtar yalnızca PowerShell 5.1 veya üstünde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c236f-109">This key is only supported on PowerShell 5.1 or later.</span></span>
<span data-ttu-id="c236f-110">*Not* bir modül bildirimi CompatiblePSEditions anahtarla belirlendikten sonra alt PowerShell sürümlerinde alınabileceği değil.</span><span class="sxs-lookup"><span data-stu-id="c236f-110">*NOTE* Once a module manifest is specified with the CompatiblePSEditions key, it can not be imported on lower versions of PowerShell.</span></span>

```powershell
New-ModuleManifest -Path .\TestModuleWithEdition.psd1 -CompatiblePSEditions Desktop,Core -PowerShellVersion 5.1
$ModuleInfo = Test-ModuleManifest -Path .\TestModuleWithEdition.psd1
$ModuleInfo.CompatiblePSEditions
Desktop
Core

$ModuleInfo | Get-Member CompatiblePSEditions

   TypeName: System.Management.Automation.PSModuleInfo

Name                 MemberType Definition
----                 ---------- ----------
CompatiblePSEditions Property   System.Collections.Generic.IEnumerable[string] CompatiblePSEditions {get;}

```
<span data-ttu-id="c236f-111">Kullanılabilir modüllerin listesini alırken, listeyi PowerShell sürümüne göre filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c236f-111">When getting a list of available modules, you can filter the list by PowerShell edition.</span></span>
```powershell
Get-Module -ListAvailable -PSEdition Desktop

    Directory: C:\Program Files\WindowsPowerShell\Modules


ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Manifest   1.0        ModuleWithPSEditions

Get-Module -ListAvailable -PSEdition Core | % CompatiblePSEditions
Desktop
Core

```

## <a name="module-authors-can-publish-a-single-module-targeting-to-either-or-both-powershell-editions-desktop-and-core"></a><span data-ttu-id="c236f-112">Modül yazarlar tek modülü hedefleme birini veya her ikisini PowerShell sürümleri için (Masaüstü ve çekirdek) yayımlama</span><span class="sxs-lookup"><span data-stu-id="c236f-112">Module authors can publish a single module targeting to either or both PowerShell editions (Desktop and Core)</span></span> 

<span data-ttu-id="c236f-113">Tek bir modül hem Masaüstü hem de çekirdek sürümleri üzerinde çalışabilir, ya da RootModule veya $PSEdition değişkenini kullanarak modül bildirimi gerekli mantığı eklemek bu modülde Yazar yoktur.</span><span class="sxs-lookup"><span data-stu-id="c236f-113">A single module can work on both Desktop and Core editions, in that module author has to add required logic in either RootModule or in the module manifest using $PSEdition variable.</span></span>
<span data-ttu-id="c236f-114">Modülleri CoreCLR ve FullCLR hedefleyen derlenen DLL'leri iki kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="c236f-114">Modules can have two sets of compiled DLLs targeting both CoreCLR and FullCLR.</span></span>
<span data-ttu-id="c236f-115">Burada, birkaç modülünüzün uygun DLL'leri yükleme için mantığı ile paketlemek için seçeneğiniz bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c236f-115">Here are the couple of options to package your module with logic for loading proper dlls.</span></span>

### <a name="option-1-packaging-a-module-for-targeting-multiple-versions-and-multiple-editions-of-powershell"></a><span data-ttu-id="c236f-116">Seçenek 1: birden çok sürümü ve PowerShell birden çok sürümü hedefleme için bir modül paketleme</span><span class="sxs-lookup"><span data-stu-id="c236f-116">Option 1: Packaging a module for targeting multiple versions and multiple editions of PowerShell</span></span>

#### <a name="module-folder-contents"></a><span data-ttu-id="c236f-117">Modül klasör içeriklerini</span><span class="sxs-lookup"><span data-stu-id="c236f-117">Module folder contents</span></span>
- <span data-ttu-id="c236f-118">Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span><span class="sxs-lookup"><span data-stu-id="c236f-118">Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span></span> 
- <span data-ttu-id="c236f-119">Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span><span class="sxs-lookup"><span data-stu-id="c236f-119">Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span></span> 
- <span data-ttu-id="c236f-120">PSScriptAnalyzer.psd1</span><span class="sxs-lookup"><span data-stu-id="c236f-120">PSScriptAnalyzer.psd1</span></span>
- <span data-ttu-id="c236f-121">PSScriptAnalyzer.psm1</span><span class="sxs-lookup"><span data-stu-id="c236f-121">PSScriptAnalyzer.psm1</span></span>
- <span data-ttu-id="c236f-122">ScriptAnalyzer.format.ps1xml</span><span class="sxs-lookup"><span data-stu-id="c236f-122">ScriptAnalyzer.format.ps1xml</span></span>
- <span data-ttu-id="c236f-123">ScriptAnalyzer.types.ps1xml</span><span class="sxs-lookup"><span data-stu-id="c236f-123">ScriptAnalyzer.types.ps1xml</span></span>
- <span data-ttu-id="c236f-124">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span><span class="sxs-lookup"><span data-stu-id="c236f-124">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span></span> 
- <span data-ttu-id="c236f-125">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span><span class="sxs-lookup"><span data-stu-id="c236f-125">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span></span> 
- <span data-ttu-id="c236f-126">en-US\about_PSScriptAnalyzer.help.txt</span><span class="sxs-lookup"><span data-stu-id="c236f-126">en-US\about_PSScriptAnalyzer.help.txt</span></span>
- <span data-ttu-id="c236f-127">en-US\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll-Help.xml</span><span class="sxs-lookup"><span data-stu-id="c236f-127">en-US\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll-Help.xml</span></span>
- <span data-ttu-id="c236f-128">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span><span class="sxs-lookup"><span data-stu-id="c236f-128">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span></span> 
- <span data-ttu-id="c236f-129">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span><span class="sxs-lookup"><span data-stu-id="c236f-129">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span></span> 
- <span data-ttu-id="c236f-130">Settings\CmdletDesign.psd1</span><span class="sxs-lookup"><span data-stu-id="c236f-130">Settings\CmdletDesign.psd1</span></span>
- <span data-ttu-id="c236f-131">Settings\DSC.psd1</span><span class="sxs-lookup"><span data-stu-id="c236f-131">Settings\DSC.psd1</span></span>
- <span data-ttu-id="c236f-132">Settings\ScriptFunctions.psd1</span><span class="sxs-lookup"><span data-stu-id="c236f-132">Settings\ScriptFunctions.psd1</span></span>
- <span data-ttu-id="c236f-133">Settings\ScriptingStyle.psd1</span><span class="sxs-lookup"><span data-stu-id="c236f-133">Settings\ScriptingStyle.psd1</span></span>
- <span data-ttu-id="c236f-134">Settings\ScriptSecurity.psd1</span><span class="sxs-lookup"><span data-stu-id="c236f-134">Settings\ScriptSecurity.psd1</span></span>

#### <a name="contents-of-psscriptanalyzerpsd1-file"></a><span data-ttu-id="c236f-135">PSScriptAnalyzer.psd1 dosyasının içeriği</span><span class="sxs-lookup"><span data-stu-id="c236f-135">Contents of PSScriptAnalyzer.psd1 file</span></span>

```powershell
@{
 
# Author of this module
Author = 'Microsoft Corporation'

# Script module or binary module file associated with this manifest.
RootModule = 'PSScriptAnalyzer.psm1'

# Version number of this module.
ModuleVersion = '1.6.1'

# ---
}
```

#### <a name="contents-of-psscriptanalyzerpsm1-file"></a><span data-ttu-id="c236f-136">PSScriptAnalyzer.psm1 dosyasının içeriği</span><span class="sxs-lookup"><span data-stu-id="c236f-136">Contents of PSScriptAnalyzer.psm1 file</span></span>
<span data-ttu-id="c236f-137">Mantığı gerekli derlemeleri geçerli sürümü veya bağlı olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="c236f-137">Below logic loads the required assemblies depending on the current edition or version.</span></span>

```powershell
#
# Script module for module 'PSScriptAnalyzer'
#
Set-StrictMode -Version Latest

# Set up some helper variables to make it easier to work with the module
$PSModule = $ExecutionContext.SessionState.Module
$PSModuleRoot = $PSModule.ModuleBase

# Import the appropriate nested binary module based on the current PowerShell version
$binaryModuleRoot = $PSModuleRoot


if (($PSVersionTable.Keys -contains "PSEdition") -and ($PSVersionTable.PSEdition -ne 'Desktop')) {
    $binaryModuleRoot = Join-Path -Path $PSModuleRoot -ChildPath 'coreclr'
}
else
{
    if ($PSVersionTable.PSVersion -lt [Version]'5.0') {
        $binaryModuleRoot = Join-Path -Path $PSModuleRoot -ChildPath 'PSv3'
    }    
}

$binaryModulePath = Join-Path -Path $binaryModuleRoot -ChildPath 'Microsoft.Windows.PowerShell.ScriptAnalyzer.dll'
$binaryModule = Import-Module -Name $binaryModulePath -PassThru

# When the module is unloaded, remove the nested binary module that was loaded with it
$PSModule.OnRemove = {
    Remove-Module -ModuleInfo $binaryModule
} 

```

### <a name="option-2-use-psedition-variable-in-the-psd1-file-to-load-the-proper-dlls-and-nestedrequired-modules"></a><span data-ttu-id="c236f-138">Seçenek 2: $PSEdition değişkeni uygun DLL'ler ve iç içe ve gerekli modüllerini yüklemek için PSD1 dosyası kullanın</span><span class="sxs-lookup"><span data-stu-id="c236f-138">Option 2: Use $PSEdition variable in the PSD1 file to load the proper DLLs and Nested/Required modules</span></span>

<span data-ttu-id="c236f-139">PS 5.1 veya daha yeni, $PSEdition genel değişkeni modülü bildirim dosyasında izin verilir.</span><span class="sxs-lookup"><span data-stu-id="c236f-139">In PS 5.1 or newer, $PSEdition global variable is allowed in the module manifest file.</span></span>
<span data-ttu-id="c236f-140">Bu değişkeni kullanarak, modül yazarına modülü bildirim dosyasında koşullu değerlerini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c236f-140">Using this variable, module author can specify the conditional values in the module manifest file.</span></span> <span data-ttu-id="c236f-141">$PSEdition değişkeni kısıtlı dil modu veya veri bölümü başvurulabilir.</span><span class="sxs-lookup"><span data-stu-id="c236f-141">$PSEdition variable can be referenced in restricted language mode or a Data section.</span></span> 

<span data-ttu-id="c236f-142">*Not* bir modül bildirimi CompatiblePSEditions anahtarla belirtilen veya $PSEdition değişkenini kullanır sonra daha düşük PowerShell sürümlerinde alınabileceği değil.</span><span class="sxs-lookup"><span data-stu-id="c236f-142">*NOTE* Once a module manifest is specified with the CompatiblePSEditions key or uses $PSEdition variable, it can not be imported on lower versions of PowerShell.</span></span>


#### <a name="sample-module-manifest-file-with-compatiblepseditions-key"></a><span data-ttu-id="c236f-143">Örnek modülü bildirim dosyası CompatiblePSEditions anahtarı</span><span class="sxs-lookup"><span data-stu-id="c236f-143">Sample module manifest file with CompatiblePSEditions key</span></span>

```powershell
@{ 
# - - -
 
# Script module or binary module file associated with this manifest.
RootModule = if($PSEdition -eq 'Core')
{
'coreclr\MyCoreClrRM.dll'
}
else # Desktop
{
'clr\MyFullClrRM.dll'
}
 
# Supported PSEditions
CompatiblePSEditions = 'Desktop', 'Core'
 
# Modules to import as nested modules of the module specified in RootModule/ModuleToProcess
NestedModules = if($PSEdition -eq 'Core')
{
'coreclr\MyCoreClrNM1.dll',
'coreclr\MyCoreClrNM2.dll'
}
else # Desktop
{
'clr\MyFullClrNM1.dll',
'clr\MyFullClrNM2.dll'
}
 
# -- - -
}
```

#### <a name="module-contents"></a><span data-ttu-id="c236f-144">Modül içerikleri</span><span class="sxs-lookup"><span data-stu-id="c236f-144">Module contents</span></span>

```powershell

PS C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions> dir -Recurse
 
    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions
 
Mode                LastWriteTime         Length Name                                                                                
----                -------------         ------ ----                                                                                
d-----         7/5/2016   1:37 PM                clr                                                                                 
d-----         7/5/2016   1:36 PM                coreclr                                                                             
-a----         7/5/2016   1:34 PM           4906 ModuleWithEditions.psd1                                                             
 
    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions\clr
 
Mode                LastWriteTime         Length Name                                                                                
----                -------------         ------ ----                                                                                
-a----         7/5/2016   1:35 PM              0 MyFullClrNM1.dll                                                                    
-a----         7/5/2016   1:35 PM              0 MyFullClrNM2.dll                                                                    
-a----         7/5/2016   1:35 PM              0 MyFullClrRM.dl                                                                      
 
    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions\coreclr
 
Mode                LastWriteTime         Length Name                                                                                
----                -------------         ------ ----                                                                                
-a----         7/5/2016   1:35 PM              0 MyCoreClrNM1.dll                                                                    
-a----         7/5/2016   1:35 PM              0 MyCoreClrNM2.dll                                                                    
-a----         7/5/2016   1:35 PM              0 MyCoreClrRM.dl                                                                      
```

## <a name="powershell-gallery-users-can-find-the-list-of-modules-supported-on-a-specific-powershell-edition-using-tags-pseditiondesktop-and-pseditoncore"></a><span data-ttu-id="c236f-145">PowerShell Galerisi kullanıcılar etiketleri PSEdition_Desktop ve PSEditon_Core kullanarak belirli bir PowerShell sürümünde desteklenen modüllerin listesini bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c236f-145">PowerShell Gallery users can find the list of modules supported on a specific PowerShell Edition using tags PSEdition_Desktop and PSEditon_Core.</span></span>
<span data-ttu-id="c236f-146">Modülleri PSEdition_Desktop ve PSEditon_Core etiketleri olmadan PowerShell Masaüstü sürümlerinde ince çalışmaya olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="c236f-146">Modules without PSEdition_Desktop and PSEditon_Core tags are considered to work fine on PowerShell Desktop editions.</span></span>

```powershell

# Find modules supported on PowerShell Desktop edition
Find-Module -Tag PSEditon_Desktop

# Find modules supported on PowerShell Core editions
Find-Module -Tag PSEditon_Core

```


## <a name="more-details"></a><span data-ttu-id="c236f-147">Daha fazla ayrıntı</span><span class="sxs-lookup"><span data-stu-id="c236f-147">More details</span></span>
### <a name="scripts-with-pseditionsscriptscriptwithpseditionsupportmd"></a>[<span data-ttu-id="c236f-148">PSEditions sahip komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="c236f-148">Scripts with PSEditions</span></span>](../script/scriptwithpseditionsupport.md)
### <a name="pseditions-support-on-powershellgallerypsgallerypsgallerypseditionsmd"></a>[<span data-ttu-id="c236f-149">PowerShellGallery PSEditions desteği</span><span class="sxs-lookup"><span data-stu-id="c236f-149">PSEditions support on PowerShellGallery</span></span>](../../psgallery/psgallery_pseditions.md)
### <a name="update-module-manifest-psgetupdate-modulemanifestmd"></a><span data-ttu-id="c236f-150">[Güncelleştirme modül bildirimi] (./psget_update-modulemanifest.md)</span><span class="sxs-lookup"><span data-stu-id="c236f-150">[Update module manifest] (./psget_update-modulemanifest.md)</span></span>
