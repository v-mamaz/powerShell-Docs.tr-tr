---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC, powershell, yapılandırma, Kur"
title: "DSC paket kaynağı"
ms.openlocfilehash: f7bcbd387db422037614feee7c4a00d93b3cec4e
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-package-resource"></a><span data-ttu-id="f4138-103">DSC paket kaynağı</span><span class="sxs-lookup"><span data-stu-id="f4138-103">DSC Package Resource</span></span>

> <span data-ttu-id="f4138-104">İçin geçerlidir: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="f4138-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="f4138-105">**Paket** kaynak olarak Windows PowerShell istenen durum yapılandırması (DSC) yüklemek veya bir hedef düğüm üzerinde Windows Installer ve setup.exe paketleri gibi paketleri kaldırmak için bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="f4138-105">The **Package** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to install or uninstall packages, such as Windows Installer and setup.exe packages, on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="f4138-106">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="f4138-106">Syntax</span></span>

```
Package [string] #ResourceName
{
    Name = [string]
    Path = [string]
    ProductId = [string]
    [ Arguments = [string] ]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    [ ReturnCode = [UInt32[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="f4138-107">Özellikler</span><span class="sxs-lookup"><span data-stu-id="f4138-107">Properties</span></span>
|  <span data-ttu-id="f4138-108">Özellik</span><span class="sxs-lookup"><span data-stu-id="f4138-108">Property</span></span>  |  <span data-ttu-id="f4138-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f4138-109">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="f4138-110">Ad</span><span class="sxs-lookup"><span data-stu-id="f4138-110">Name</span></span>| <span data-ttu-id="f4138-111">Belirli bir durumu sağlamak istediğiniz paketinin adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="f4138-111">Indicates the name of the package for which you want to ensure a specific state.</span></span>| 
| <span data-ttu-id="f4138-112">Yol</span><span class="sxs-lookup"><span data-stu-id="f4138-112">Path</span></span>| <span data-ttu-id="f4138-113">Paketin bulunduğu yolu gösterir.</span><span class="sxs-lookup"><span data-stu-id="f4138-113">Indicates the path where the package resides.</span></span>| 
| <span data-ttu-id="f4138-114">ProductID</span><span class="sxs-lookup"><span data-stu-id="f4138-114">ProductId</span></span>| <span data-ttu-id="f4138-115">Paketi benzersiz olarak tanıtan ürün kimliği gösterir.</span><span class="sxs-lookup"><span data-stu-id="f4138-115">Indicates the product ID that uniquely identifies the package.</span></span>| 
| <span data-ttu-id="f4138-116">Bağımsız değişkenler</span><span class="sxs-lookup"><span data-stu-id="f4138-116">Arguments</span></span>| <span data-ttu-id="f4138-117">Paketi tam olarak sağlanan gibi geçirilen bağımsız değişken bir dize listeler.</span><span class="sxs-lookup"><span data-stu-id="f4138-117">Lists a string of arguments that will be passed to the package exactly as provided.</span></span>| 
| <span data-ttu-id="f4138-118">kimlik bilgisi</span><span class="sxs-lookup"><span data-stu-id="f4138-118">Credential</span></span>| <span data-ttu-id="f4138-119">Uzak bir kaynağı üzerinde paket erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="f4138-119">Provides access to the package on a remote source.</span></span> <span data-ttu-id="f4138-120">Bu özellik paketini yüklemek için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="f4138-120">This property is not used to install the package.</span></span> <span data-ttu-id="f4138-121">Paket yerel sistem üzerindeki her zaman yüklenir.</span><span class="sxs-lookup"><span data-stu-id="f4138-121">The package is always installed on the local system.</span></span>| 
| <span data-ttu-id="f4138-122">Emin olun</span><span class="sxs-lookup"><span data-stu-id="f4138-122">Ensure</span></span>| <span data-ttu-id="f4138-123">Paketin yüklü olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f4138-123">Indicates if the package is installed.</span></span> <span data-ttu-id="f4138-124">Bu özelliği paketi yüklü değil emin olun (veya paket yüklüyse kaldırmak için) "yok" olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f4138-124">Set this property to "Absent" to ensure the package is not installed (or uninstall the package if it is installed).</span></span> <span data-ttu-id="f4138-125">"Paketinin yüklü emin olmak için (varsayılan değer) sunmak için" olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f4138-125">Set it to "Present" (the default value) to ensure the package is installed.</span></span>| 
| <span data-ttu-id="f4138-126">LogPath</span><span class="sxs-lookup"><span data-stu-id="f4138-126">LogPath</span></span>| <span data-ttu-id="f4138-127">Sağlayıcı yüklemek veya paket kaldırmak için bir günlük dosyasını kaydetmek istediğiniz yeri tam yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="f4138-127">Indicates the full path where you want the provider to save a log file to install or uninstall the package.</span></span>| 
| <span data-ttu-id="f4138-128">dependsOn</span><span class="sxs-lookup"><span data-stu-id="f4138-128">DependsOn</span></span> | <span data-ttu-id="f4138-129">Bu kaynak yapılandırılmadan önce başka bir kaynak yapılandırmasını çalıştırmalısınız gösterir.</span><span class="sxs-lookup"><span data-stu-id="f4138-129">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="f4138-130">Örneğin, kaynak yapılandırması Kimliğini komut dosyası çalıştırmak istediğiniz bloğu ilk ise **ResourceName** ve türünü **ResourceType**, bu özelliği kullanmak için sözdizimi ' DependsOn = "[ ResourceType] KaynakAdı"''.</span><span class="sxs-lookup"><span data-stu-id="f4138-130">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`\`.</span></span>| 
| <span data-ttu-id="f4138-131">ReturnCode</span><span class="sxs-lookup"><span data-stu-id="f4138-131">ReturnCode</span></span>| <span data-ttu-id="f4138-132">Beklenen dönüş kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="f4138-132">Indicates the expected return code.</span></span> <span data-ttu-id="f4138-133">Gerçek kodu döndürmesi durumunda yapılandırma bir hata döndürecektir beklenen değer burada sağlanan adla eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="f4138-133">If the actual return code does not match the expected value provided here, the configuration will return an error.</span></span>| 

## <a name="example"></a><span data-ttu-id="f4138-134">Örnek</span><span class="sxs-lookup"><span data-stu-id="f4138-134">Example</span></span>

<span data-ttu-id="f4138-135">Bu örnek belirtilen yolda bulunur ve belirtilen ürün kimliği olan .msi yükleyicisini çalıştırır</span><span class="sxs-lookup"><span data-stu-id="f4138-135">This example runs the .msi installer that is located at the specified path and has the specified product ID.</span></span>

```powershell
Configuration PackageTest
{
    Package PackageExample
    {
        Ensure      = "Present"  # You can also set Ensure to "Absent"
        Path        = "$Env:SystemDrive\TestFolder\TestProject.msi"
        Name        = "TestPackage"
        ProductId   = "ACDDCDAF-80C6-41E6-A1B9-8ABD8A05027E"
    } 
}
```
