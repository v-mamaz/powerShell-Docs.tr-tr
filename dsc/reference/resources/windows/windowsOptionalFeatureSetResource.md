---
ms.date: 06/12/2017
keywords: DSC, powershell, yapılandırma, Kurulum
title: DSC WindowsOptionalFeatureSet kaynağı
ms.openlocfilehash: c27d026e01bbb443a82112e37f1d199fb3482e49
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048668"
---
# <a name="dsc-windowsoptionalfeatureset-resource"></a><span data-ttu-id="beae1-103">DSC WindowsOptionalFeatureSet kaynağı</span><span class="sxs-lookup"><span data-stu-id="beae1-103">DSC WindowsOptionalFeatureSet Resource</span></span>

> <span data-ttu-id="beae1-104">Şunun için geçerlidir: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="beae1-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="beae1-105">**WindowsOptionalFeatureSet** kaynak olarak Windows PowerShell Desired State Configuration (DSC), isteğe bağlı özellikler hedef düğümde etkinleştirildiğinden emin olmak için bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="beae1-105">The **WindowsOptionalFeatureSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that optional features are enabled on a target node.</span></span>
<span data-ttu-id="beae1-106">Bu kaynak bir [bileşik kaynak](../../../resources/authoringResourceComposite.md) çağrılarının [WindowsOptionalFeature kaynağı](windowsOptionalFeatureResource.md) belirtilen her bir özellik `Name` özelliği.</span><span class="sxs-lookup"><span data-stu-id="beae1-106">This resource is a [composite resource](../../../resources/authoringResourceComposite.md) that calls the [WindowsOptionalFeature resource](windowsOptionalFeatureResource.md) for each feature specified in the `Name` property.</span></span>

<span data-ttu-id="beae1-107">Windows isteğe bağlı özellikler aynı duruma yapılandırmak istediğinizde bu kaynağı kullanın.</span><span class="sxs-lookup"><span data-stu-id="beae1-107">Use this resource when you want to configure a number of Windows optional features to the same state.</span></span>

## <a name="syntax"></a><span data-ttu-id="beae1-108">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="beae1-108">Syntax</span></span>

```
WindowsOptionalFeature [string] #ResourceName
{
    Name = [string[]]
    [ Ensure = [string] { Enable | Disable }  ]
    [ Source = [string] ]
    [ RemoveFilesOnDisable = [bool] ]
    [ LogPath = [string] ]
    [ NoWindowsUpdateCheck = [bool] ]
    [ LogLevel = [string] { ErrorsOnly | ErrorsAndWarning | ErrorsAndWarningAndInformation }  ]
    [ DependsOn = [string[]] ]

}
```

## <a name="properties"></a><span data-ttu-id="beae1-109">Özellikler</span><span class="sxs-lookup"><span data-stu-id="beae1-109">Properties</span></span>

|  <span data-ttu-id="beae1-110">Özellik</span><span class="sxs-lookup"><span data-stu-id="beae1-110">Property</span></span>  |  <span data-ttu-id="beae1-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="beae1-111">Description</span></span>   |
|---|---|
| <span data-ttu-id="beae1-112">Ad</span><span class="sxs-lookup"><span data-stu-id="beae1-112">Name</span></span>| <span data-ttu-id="beae1-113">Sağlamak istediğiniz özelliklerini adını etkin veya devre dışı gösterir.</span><span class="sxs-lookup"><span data-stu-id="beae1-113">Indicates the name of the features that you want to ensure are enabled or disabled.</span></span>|
| <span data-ttu-id="beae1-114">Emin olun</span><span class="sxs-lookup"><span data-stu-id="beae1-114">Ensure</span></span>| <span data-ttu-id="beae1-115">Özelliklerin etkinleştirilip etkinleştirilmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="beae1-115">Specifies whether the features are enabled.</span></span> <span data-ttu-id="beae1-116">Özellikleri olmasını sağlamak için etkin olarak ayarlayın "Etkinleştir" özellikleri devre dışı olduğunu, emin olmak için bu özelliği ayarlayın "Devre dışı bırak" özelliğini.</span><span class="sxs-lookup"><span data-stu-id="beae1-116">To ensure that the features are enabled, set this property to "Enable" To ensure that the features are disabled, set the property to "Disable".</span></span>|
| <span data-ttu-id="beae1-117">Kaynak</span><span class="sxs-lookup"><span data-stu-id="beae1-117">Source</span></span>| <span data-ttu-id="beae1-118">Henüz uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="beae1-118">Not implemented.</span></span>|
| <span data-ttu-id="beae1-119">NoWindowsUpdateCheck</span><span class="sxs-lookup"><span data-stu-id="beae1-119">NoWindowsUpdateCheck</span></span>| <span data-ttu-id="beae1-120">DISM özellikleri etkinleştirmek kaynak dosyalarının aranacağı Windows Update (WU) kişiler olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="beae1-120">Specifies whether DISM contacts Windows Update (WU) when searching for the source files to enable features.</span></span> <span data-ttu-id="beae1-121">$True, DISM WU sizinle iletişime değil.</span><span class="sxs-lookup"><span data-stu-id="beae1-121">If $true, DISM does not contact WU.</span></span>|
| <span data-ttu-id="beae1-122">RemoveFilesOnDisable</span><span class="sxs-lookup"><span data-stu-id="beae1-122">RemoveFilesOnDisable</span></span>| <span data-ttu-id="beae1-123">Kümesine **$true** devre dışı bırakılana özelliklerle ilişkili tüm dosyaları kaldırmak için (diğer bir deyişle, zaman **emin olun** ayarlanır için "Yok").</span><span class="sxs-lookup"><span data-stu-id="beae1-123">Set to **$true** to remove all files associated with the features when they are disabled (that is, when **Ensure** is set to "Absent").</span></span>|
| <span data-ttu-id="beae1-124">GünlükDüzeyi</span><span class="sxs-lookup"><span data-stu-id="beae1-124">LogLevel</span></span>| <span data-ttu-id="beae1-125">Günlüklerde gösterilen maksimum çıktı düzeyini.</span><span class="sxs-lookup"><span data-stu-id="beae1-125">The maximum output level shown in the logs.</span></span> <span data-ttu-id="beae1-126">Kabul edilen değerler şunlardır: "(Yalnızca hatalar kaydedilir) ErrorsOnly", "ErrorsAndWarning" (hatalar ve uyarılar günlüğe kaydedilir) ve "ErrorsAndWarningAndInformation" (hataları, uyarıları ve hata ayıklama bilgileri kaydedilir).</span><span class="sxs-lookup"><span data-stu-id="beae1-126">The accepted values are: "ErrorsOnly" (only errors are logged), "ErrorsAndWarning" (errors and warnings are logged), and "ErrorsAndWarningAndInformation" (errors, warnings, and debug information are logged).</span></span>|
| <span data-ttu-id="beae1-127">LogPath</span><span class="sxs-lookup"><span data-stu-id="beae1-127">LogPath</span></span>| <span data-ttu-id="beae1-128">Kaynak sağlayıcısı işlemi oturum istediğiniz bir günlük dosyası yolu.</span><span class="sxs-lookup"><span data-stu-id="beae1-128">The path to a log file where you want the resource provider to log the operation.</span></span>|
| <span data-ttu-id="beae1-129">DependsOn</span><span class="sxs-lookup"><span data-stu-id="beae1-129">DependsOn</span></span>| <span data-ttu-id="beae1-130">Bu kaynağı yapılandırılmadan önce başka bir kaynak yapılandırmasını çalıştırmanız gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="beae1-130">Specifies that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="beae1-131">Örneğin, kaynak yapılandırmasının Kimliğini çalıştırmak istediğiniz bir blok betik ilk ise __ResourceName__ ve kendi türünün __ResourceType__, bu özelliği kullanmak için sözdizimi `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="beae1-131">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|