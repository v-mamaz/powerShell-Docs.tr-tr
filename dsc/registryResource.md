---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC, powershell, yapılandırma, Kur"
title: "DSC kayıt kaynağı"
ms.openlocfilehash: 649cb60578c053c04a7fcc7446881fb76daee26a
ms.sourcegitcommit: 79e8f03afb8d0b0bb0a167e56464929b27f51990
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/26/2017
---
# <a name="dsc-registry-resource"></a><span data-ttu-id="4ffcf-103">DSC kayıt kaynağı</span><span class="sxs-lookup"><span data-stu-id="4ffcf-103">DSC Registry Resource</span></span>

> <span data-ttu-id="4ffcf-104">İçin geçerlidir: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="4ffcf-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="4ffcf-105">**Kayıt defteri** kaynağı içinde Windows PowerShell istenen durum yapılandırması (DSC), kayıt defteri anahtarları ve değerleri bir hedef düğümdeki yönetmek için bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="4ffcf-105">The **Registry** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage registry keys and values on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="4ffcf-106">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="4ffcf-106">Syntax</span></span>

```
Registry [string] #ResourceName
{
    Key = [string]
    ValueName = [string]
    [ Ensure = [string] { Enable | Disable }  ]
    [ Force =  [bool]   ]
    [ Hex = [bool] ]
    [ DependsOn = [string[]] ]
    [ ValueData = [string[]] ]
    [ ValueType = [string] { Binary | Dword | ExpandString | MultiString | Qword | String }  ]
}
```

## <a name="properties"></a><span data-ttu-id="4ffcf-107">Özellikler</span><span class="sxs-lookup"><span data-stu-id="4ffcf-107">Properties</span></span>
|  <span data-ttu-id="4ffcf-108">Özellik</span><span class="sxs-lookup"><span data-stu-id="4ffcf-108">Property</span></span>  |  <span data-ttu-id="4ffcf-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4ffcf-109">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="4ffcf-110">üzerine gelin</span><span class="sxs-lookup"><span data-stu-id="4ffcf-110">Key</span></span>| <span data-ttu-id="4ffcf-111">Belirli bir durumu sağlamak istediğiniz kayıt defteri anahtarının yolunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="4ffcf-111">Indicates the path of the registry key for which you want to ensure a specific state.</span></span> <span data-ttu-id="4ffcf-112">Bu yol hive içermelidir.</span><span class="sxs-lookup"><span data-stu-id="4ffcf-112">This path must include the hive.</span></span>| 
| <span data-ttu-id="4ffcf-113">Değer adı</span><span class="sxs-lookup"><span data-stu-id="4ffcf-113">ValueName</span></span>| <span data-ttu-id="4ffcf-114">Kayıt defteri değerinin adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="4ffcf-114">Indicates the name of the registry value.</span></span> <span data-ttu-id="4ffcf-115">Eklemek veya bir kayıt defteri anahtarı kaldırmak için ValueType veya ValueData belirtmeden bu özellik olarak boş bir dize belirtin.</span><span class="sxs-lookup"><span data-stu-id="4ffcf-115">To add or remove a registry key, specify this property as an empty string without specifying ValueType or ValueData.</span></span> <span data-ttu-id="4ffcf-116">Değiştirmek veya bir kayıt defteri anahtarının varsayılan değeri kaldırmak için ValueType veya ValueData de belirtildiğinde bu özellik olarak boş bir dize belirtin.</span><span class="sxs-lookup"><span data-stu-id="4ffcf-116">To modify or remove the default value of a registry key, specify this property as an empty string while also specifying ValueType or ValueData.</span></span>| 
| <span data-ttu-id="4ffcf-117">Emin olun</span><span class="sxs-lookup"><span data-stu-id="4ffcf-117">Ensure</span></span>| <span data-ttu-id="4ffcf-118">Anahtar ve değer var olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="4ffcf-118">Indicates if the key and value exist.</span></span> <span data-ttu-id="4ffcf-119">"Var" Bu özelliği ayarlayın emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="4ffcf-119">To ensure that they do, set this property to "Present".</span></span> <span data-ttu-id="4ffcf-120">Mevcut olduğundan emin olmak için "Yok" özelliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4ffcf-120">To ensure that they do not exist, set the property to "Absent".</span></span> <span data-ttu-id="4ffcf-121">"Var" varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="4ffcf-121">The default value is "Present".</span></span>| 
| <span data-ttu-id="4ffcf-122">Force</span><span class="sxs-lookup"><span data-stu-id="4ffcf-122">Force</span></span>| <span data-ttu-id="4ffcf-123">Belirtilen kayıt defteri anahtarı varsa, __zorla__ yeni değerle üzerine yazar.</span><span class="sxs-lookup"><span data-stu-id="4ffcf-123">If the specified registry key is present, __Force__ overwrites it with the new value.</span></span> <span data-ttu-id="4ffcf-124">Alt anahtarlar içeren bir kayıt defteri anahtarının silinmesi, bu olması gerekir __$true__</span><span class="sxs-lookup"><span data-stu-id="4ffcf-124">If deleting a registry key with subkeys, this needs to be __$true__</span></span>| 
| <span data-ttu-id="4ffcf-125">Onaltılık</span><span class="sxs-lookup"><span data-stu-id="4ffcf-125">Hex</span></span>| <span data-ttu-id="4ffcf-126">Onaltılık biçimde belirtilecektir veri gösterir.</span><span class="sxs-lookup"><span data-stu-id="4ffcf-126">Indicates if data will be expressed in hexadecimal format.</span></span> <span data-ttu-id="4ffcf-127">Belirtilmişse, onaltılık biçimde DWORD/QWORD değer verisi sunulur.</span><span class="sxs-lookup"><span data-stu-id="4ffcf-127">If specified, the DWORD/QWORD value data is presented in hexadecimal format.</span></span> <span data-ttu-id="4ffcf-128">Diğer türleri için geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="4ffcf-128">Not valid for other types.</span></span> <span data-ttu-id="4ffcf-129">Varsayılan değer __$false__.</span><span class="sxs-lookup"><span data-stu-id="4ffcf-129">The default value is __$false__.</span></span>| 
| <span data-ttu-id="4ffcf-130">dependsOn</span><span class="sxs-lookup"><span data-stu-id="4ffcf-130">DependsOn</span></span>| <span data-ttu-id="4ffcf-131">Bu kaynak yapılandırılmadan önce başka bir kaynak yapılandırmasını çalıştırmalısınız gösterir.</span><span class="sxs-lookup"><span data-stu-id="4ffcf-131">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="4ffcf-132">Örneğin, kaynak yapılandırması Kimliğini komut dosyası çalıştırmak istediğiniz bloğu ilk ise __ResourceName__ ve türünü __ResourceType__, bu özelliği kullanmak için sözdizimi `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="4ffcf-132">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 
| <span data-ttu-id="4ffcf-133">ValueData</span><span class="sxs-lookup"><span data-stu-id="4ffcf-133">ValueData</span></span>| <span data-ttu-id="4ffcf-134">Kayıt defteri değeri verileri.</span><span class="sxs-lookup"><span data-stu-id="4ffcf-134">The data for the registry value.</span></span>| 
| <span data-ttu-id="4ffcf-135">ValueType</span><span class="sxs-lookup"><span data-stu-id="4ffcf-135">ValueType</span></span>| <span data-ttu-id="4ffcf-136">Değerin türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="4ffcf-136">Indicates the type of the value.</span></span> <span data-ttu-id="4ffcf-137">Desteklenen türler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4ffcf-137">The supported types are:</span></span> 
<ul><li><span data-ttu-id="4ffcf-138">Dize (REG_SZ)</span><span class="sxs-lookup"><span data-stu-id="4ffcf-138">String (REG_SZ)</span></span></li>


<li><span data-ttu-id="4ffcf-139">İkili (ikili REG)</span><span class="sxs-lookup"><span data-stu-id="4ffcf-139">Binary (REG-BINARY)</span></span></li>


<li><span data-ttu-id="4ffcf-140">DWORD 32-bit (REG_DWORD)</span><span class="sxs-lookup"><span data-stu-id="4ffcf-140">Dword 32-bit (REG_DWORD)</span></span></li>


<li><span data-ttu-id="4ffcf-141">QWORD 64-bit (REG_QWORD)</span><span class="sxs-lookup"><span data-stu-id="4ffcf-141">Qword 64-bit (REG_QWORD)</span></span></li>


<li><span data-ttu-id="4ffcf-142">Çoklu dize (REG_MULTI_SZ)</span><span class="sxs-lookup"><span data-stu-id="4ffcf-142">Multi-string (REG_MULTI_SZ)</span></span></li>


<li><span data-ttu-id="4ffcf-143">Genişletilebilir dize (REG_EXPAND_SZ)</span><span class="sxs-lookup"><span data-stu-id="4ffcf-143">Expandable string (REG_EXPAND_SZ)</span></span></li></ul>

## <a name="example"></a><span data-ttu-id="4ffcf-144">Örnek</span><span class="sxs-lookup"><span data-stu-id="4ffcf-144">Example</span></span>
<span data-ttu-id="4ffcf-145">Bu örnekte "ExampleKey" adlı bir anahtar mevcut olmasını sağlar **HKEY\_yerel\_makine** hive.</span><span class="sxs-lookup"><span data-stu-id="4ffcf-145">This example ensures that a key named "ExampleKey" is present in the **HKEY\_LOCAL\_MACHINE** hive.</span></span>
```powershell
Configuration RegistryTest
{
    Registry RegistryExample
    {
        Ensure      = "Present"  # You can also set Ensure to "Absent"
        Key         = "HKEY_LOCAL_MACHINE\SOFTWARE\ExampleKey"
        ValueName   = "TestValue"
        ValueData   = "TestData"
    }
}
```

><span data-ttu-id="4ffcf-146">**Not:** bir kayıt defteri ayarını değiştirerek **HKEY\_geçerli\_kullanıcı** hive gerektirir yapılandırma sistemi olarak değil, kullanıcı kimlik bilgileriyle çalışır.</span><span class="sxs-lookup"><span data-stu-id="4ffcf-146">**Note:** Changing a registry setting in the **HKEY\_CURRENT\_USER** hive requires that the configuration runs with user credentials, rather than as the system.</span></span>
><span data-ttu-id="4ffcf-147">Kullanabileceğiniz **PsDscRunAsCredential** özelliği yapılandırma için kullanıcı kimlik bilgilerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="4ffcf-147">You can use the **PsDscRunAsCredential** property to specify user credentials for the configuration.</span></span> <span data-ttu-id="4ffcf-148">Bir örnek için bkz: [çalıştıran DSC kullanıcı kimlik bilgileri](runAsUser.md)</span><span class="sxs-lookup"><span data-stu-id="4ffcf-148">For an example, see [Running DSC with user credentials](runAsUser.md)</span></span>


