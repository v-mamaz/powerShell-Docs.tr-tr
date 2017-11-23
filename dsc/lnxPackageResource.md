---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC, powershell, yapılandırma, Kur"
title: "DSC Linux nxPackage kaynak için"
ms.openlocfilehash: 11019b1cd12f23b0b498b7cb9a06e02c46c3c279
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-for-linux-nxpackage-resource"></a><span data-ttu-id="d802f-103">DSC Linux nxPackage kaynak için</span><span class="sxs-lookup"><span data-stu-id="d802f-103">DSC for Linux nxPackage Resource</span></span>

<span data-ttu-id="d802f-104">**NxPackage** kaynağı içinde PowerShell istenen durum yapılandırması (DSC), bir Linux düğümünde paketlerini yönetmek için bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="d802f-104">The **nxPackage** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage packages on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="d802f-105">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="d802f-105">Syntax</span></span>

```
nxPackage <string> #ResourceName
{
    Name = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ PackageManager = <string> { Yum | Apt | Zypper } ]
    [ PackageGroup = <bool>]
    [ Arguments = <string> ]
    [ ReturnCode = <uint32> ]
    [ LogPath = <string> ]
    [ DependsOn = <string[]> ]
    
}
```

## <a name="properties"></a><span data-ttu-id="d802f-106">Özellikler</span><span class="sxs-lookup"><span data-stu-id="d802f-106">Properties</span></span>

|  <span data-ttu-id="d802f-107">Özellik</span><span class="sxs-lookup"><span data-stu-id="d802f-107">Property</span></span> |  <span data-ttu-id="d802f-108">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d802f-108">Description</span></span> | 
|---|---|
| <span data-ttu-id="d802f-109">Ad</span><span class="sxs-lookup"><span data-stu-id="d802f-109">Name</span></span>| <span data-ttu-id="d802f-110">Belirli bir durumu sağlamak istediğiniz paket adı.</span><span class="sxs-lookup"><span data-stu-id="d802f-110">The name of the package for which you want to ensure a specific state.</span></span>| 
| <span data-ttu-id="d802f-111">Emin olun</span><span class="sxs-lookup"><span data-stu-id="d802f-111">Ensure</span></span>| <span data-ttu-id="d802f-112">Paketin var olup olmadığını denetlemek belirler.</span><span class="sxs-lookup"><span data-stu-id="d802f-112">Determines whether to check if the package exists.</span></span> <span data-ttu-id="d802f-113">Bu özelliği paketin varolduğundan emin olmak için "var" olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d802f-113">Set this property to "Present" to ensure the package exists.</span></span> <span data-ttu-id="d802f-114">"Mevcut için" paketi yok emin olmak için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d802f-114">Set it to "Absent" to ensure the package does not exist.</span></span> <span data-ttu-id="d802f-115">"Var" varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="d802f-115">The default value is "Present".</span></span>|  
| <span data-ttu-id="d802f-116">PackageManager</span><span class="sxs-lookup"><span data-stu-id="d802f-116">PackageManager</span></span>| <span data-ttu-id="d802f-117">"Yum", "apt" ve "zypper" değerleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="d802f-117">Supported values are "yum", "apt", and "zypper".</span></span> <span data-ttu-id="d802f-118">Paket Yöneticisi'ni paketleri yüklerken kullanılacak belirtir.</span><span class="sxs-lookup"><span data-stu-id="d802f-118">Specifies the package manager to use when installing packages.</span></span> <span data-ttu-id="d802f-119">Varsa **FilePath** belirtilirse, sağlanan yol, paketi yüklemek için kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="d802f-119">If **FilePath** is specified, the provided path will be used to install the package.</span></span> <span data-ttu-id="d802f-120">Aksi halde, bir paket Yöneticisi, önceden yapılandırılmış bir depodan paketi yüklemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d802f-120">Otherwise, a Package Manager will be used to install the package from a pre-configured repository.</span></span> <span data-ttu-id="d802f-121">Ne **PackageManager** ya da **FilePath** sağlanır, varsayılan Paket Yöneticisi sistem kullanılacak için.</span><span class="sxs-lookup"><span data-stu-id="d802f-121">If neither **PackageManager** nor **FilePath** are provided, the default package manager for the system will be used.</span></span>| 
| <span data-ttu-id="d802f-122">filePath</span><span class="sxs-lookup"><span data-stu-id="d802f-122">FilePath</span></span>| <span data-ttu-id="d802f-123">Paketin bulunduğu dosya yolu</span><span class="sxs-lookup"><span data-stu-id="d802f-123">The file path where the package resides</span></span>| 
| <span data-ttu-id="d802f-124">PackageGroup</span><span class="sxs-lookup"><span data-stu-id="d802f-124">PackageGroup</span></span>| <span data-ttu-id="d802f-125">Varsa **$true**, **adı** ile kullanmak için bir paket grubunun adını olması beklenen bir **PackageManager**.</span><span class="sxs-lookup"><span data-stu-id="d802f-125">If **$true**, the **Name** is expected to be the name of a package group for use with a **PackageManager**.</span></span> <span data-ttu-id="d802f-126">**PacakgeGroup** sağlanırken geçersiz bir **FilePath**.</span><span class="sxs-lookup"><span data-stu-id="d802f-126">**PacakgeGroup** is not valid when providing a **FilePath**.</span></span>| 
| <span data-ttu-id="d802f-127">Bağımsız değişkenler</span><span class="sxs-lookup"><span data-stu-id="d802f-127">Arguments</span></span>| <span data-ttu-id="d802f-128">Paketi tam olarak sağlanan gibi geçirilen bağımsız değişken bir dize.</span><span class="sxs-lookup"><span data-stu-id="d802f-128">A string of arguments that will be passed to the package exactly as provided.</span></span>| 
| <span data-ttu-id="d802f-129">ReturnCode</span><span class="sxs-lookup"><span data-stu-id="d802f-129">ReturnCode</span></span>| <span data-ttu-id="d802f-130">Beklenen dönüş kodu.</span><span class="sxs-lookup"><span data-stu-id="d802f-130">The expected return code.</span></span> <span data-ttu-id="d802f-131">Gerçek kodu döndürmesi durumunda yapılandırma bir hata döndürecektir beklenen değer burada sağlanan adla eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="d802f-131">If the actual return code does not match the expected value provided here, the configuration will return an error.</span></span>| 
| <span data-ttu-id="d802f-132">dependsOn</span><span class="sxs-lookup"><span data-stu-id="d802f-132">DependsOn</span></span> | <span data-ttu-id="d802f-133">Bu kaynak yapılandırılmadan önce başka bir kaynak yapılandırmasını çalıştırmalısınız gösterir.</span><span class="sxs-lookup"><span data-stu-id="d802f-133">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="d802f-134">Örneğin, varsa **kimliği** çalıştırmak istediğiniz yapılandırma betik bloğu ilk kaynaktır **ResourceName** ve türünü **ResourceType**, bunu kullanarak söz dizimi özellik `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="d802f-134">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 

## <a name="example"></a><span data-ttu-id="d802f-135">Örnek</span><span class="sxs-lookup"><span data-stu-id="d802f-135">Example</span></span>

<span data-ttu-id="d802f-136">Aşağıdaki örnekte, "httpd" adlı paket "Yum" Paket Yöneticisi'ni kullanarak bir Linux bilgisayara yüklendiğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="d802f-136">The following example ensures that the package named "httpd" is installed on a Linux computer, using the “Yum” package manager.</span></span>

```
Import-DSCResource -Module nx 

Node $node {
nxPackage httpd
{
    Name = "httpd"
    Ensure = "Present"
    PackageManager = "Yum"
}
}
```
