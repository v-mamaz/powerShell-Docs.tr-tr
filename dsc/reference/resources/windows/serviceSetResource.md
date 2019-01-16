---
ms.date: 06/12/2017
keywords: DSC, powershell, yapılandırma, Kurulum
title: DSC ServiceSet kaynağı
ms.openlocfilehash: 5694c2abc5c0caf0098670b629af464b35125583
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048643"
---
# <a name="dsc-serviceset-resource"></a><span data-ttu-id="270d8-103">DSC ServiceSet kaynağı</span><span class="sxs-lookup"><span data-stu-id="270d8-103">DSC ServiceSet Resource</span></span>

> <span data-ttu-id="270d8-104">Şunun için geçerlidir: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="270d8-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="270d8-105">**ServiceSet** kaynak olarak Windows PowerShell Desired State Configuration (DSC), hedef düğümdeki hizmetleri yönetmek için bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="270d8-105">The **ServiceSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage services on the target node.</span></span> <span data-ttu-id="270d8-106">Bu kaynak bir [bileşik kaynak](../../../resources/authoringResourceComposite.md) çağrılarının [hizmet kaynak](serviceResource.md) belirtilen her hizmet için `Name` özelliği.</span><span class="sxs-lookup"><span data-stu-id="270d8-106">This resource is a [composite resource](../../../resources/authoringResourceComposite.md) that calls the [Service resource](serviceResource.md) for each service specified in the `Name` property.</span></span>

<span data-ttu-id="270d8-107">Bu kaynak, bir dizi hizmet için aynı duruma yapılandırmak istediğinizde kullanın.</span><span class="sxs-lookup"><span data-stu-id="270d8-107">Use this resource when you want to configure a number of services to the same state.</span></span>

## <a name="syntax"></a><span data-ttu-id="270d8-108">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="270d8-108">Syntax</span></span>

```
Service [string] #ResourceName
{
    Name = [string[]]
    [ StartupType = [string] { Automatic | Disabled | Manual }  ]
    [ BuiltInAccount = [string] { LocalService | LocalSystem | NetworkService }  ]
    [ State = [string] { Running | Stopped }  ]
    [ Ensure = [string] { Absent | Present }  ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]

}
```

## <a name="properties"></a><span data-ttu-id="270d8-109">Özellikler</span><span class="sxs-lookup"><span data-stu-id="270d8-109">Properties</span></span>

|  <span data-ttu-id="270d8-110">Özellik</span><span class="sxs-lookup"><span data-stu-id="270d8-110">Property</span></span>  |  <span data-ttu-id="270d8-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="270d8-111">Description</span></span>   |
|---|---|
| <span data-ttu-id="270d8-112">Ad</span><span class="sxs-lookup"><span data-stu-id="270d8-112">Name</span></span>| <span data-ttu-id="270d8-113">Hizmet adlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="270d8-113">Indicates the service names.</span></span> <span data-ttu-id="270d8-114">Bazen bu görünen adları farklı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="270d8-114">Note that sometimes this is different from the display names.</span></span> <span data-ttu-id="270d8-115">Hizmetler ve bunların geçerli durumunu içeren bir listesini alabilirsiniz [Get-Service](https://technet.microsoft.com/library/hh849804.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="270d8-115">You can get a list of the services and their current state with the [Get-Service](https://technet.microsoft.com/library/hh849804.aspx) cmdlet.</span></span>|
| <span data-ttu-id="270d8-116">Başlangıç türü</span><span class="sxs-lookup"><span data-stu-id="270d8-116">StartupType</span></span>| <span data-ttu-id="270d8-117">Hizmet başlangıç türünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="270d8-117">Indicates the startup type for the service.</span></span> <span data-ttu-id="270d8-118">Bu özellik için izin verilen değerler şunlardır: **Otomatik**, **devre dışı bırakılmış**, ve **el ile**</span><span class="sxs-lookup"><span data-stu-id="270d8-118">The values that are allowed for this property are: **Automatic**, **Disabled**, and **Manual**</span></span>|
| <span data-ttu-id="270d8-119">BuiltInAccount</span><span class="sxs-lookup"><span data-stu-id="270d8-119">BuiltInAccount</span></span>| <span data-ttu-id="270d8-120">Hizmetleri kullanmak için oturum açma hesabını belirtir.</span><span class="sxs-lookup"><span data-stu-id="270d8-120">Indicates the sign-in account to use for the services.</span></span> <span data-ttu-id="270d8-121">Bu özellik için izin verilen değerler şunlardır: **Yerelhizmet**, **LocalSystem**, ve **NetworkService**.</span><span class="sxs-lookup"><span data-stu-id="270d8-121">The values that are allowed for this property are: **LocalService**, **LocalSystem**, and **NetworkService**.</span></span>|
| <span data-ttu-id="270d8-122">Durum</span><span class="sxs-lookup"><span data-stu-id="270d8-122">State</span></span>| <span data-ttu-id="270d8-123">Hizmetler için sağlamak istediğiniz durumunu gösterir: **Durduruldu** veya **çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="270d8-123">Indicates the state you want to ensure for the services: **Stopped** or **Running**.</span></span>|
| <span data-ttu-id="270d8-124">Emin olun</span><span class="sxs-lookup"><span data-stu-id="270d8-124">Ensure</span></span>| <span data-ttu-id="270d8-125">Hizmetleri sisteminde mevcut olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="270d8-125">Indicates whether the services exist on the system.</span></span> <span data-ttu-id="270d8-126">Bu özellik kümesine **devamsızlık** Hizmetleri mevcut emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="270d8-126">Set this property to **Absent** to ensure that the services do not exist.</span></span> <span data-ttu-id="270d8-127">Bu ayarın **mevcut** (varsayılan değer) hedef Hizmetleri mevcut olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="270d8-127">Setting it to **Present** (the default value) ensures that target services exist.</span></span>|
| <span data-ttu-id="270d8-128">Kimlik bilgisi</span><span class="sxs-lookup"><span data-stu-id="270d8-128">Credential</span></span>| <span data-ttu-id="270d8-129">Hizmet kaynağı altında çalışacağı hesabın kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="270d8-129">Indicates credentials for the account that the service resource will run under.</span></span> <span data-ttu-id="270d8-130">Bu özellik ve **BuiltinAccount** özelliği birlikte kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="270d8-130">This property and the **BuiltinAccount** property cannot be used together.</span></span>|
| <span data-ttu-id="270d8-131">DependsOn</span><span class="sxs-lookup"><span data-stu-id="270d8-131">DependsOn</span></span>| <span data-ttu-id="270d8-132">Bu kaynağı yapılandırılmadan önce başka bir kaynak yapılandırmasını çalıştırmanız gerektiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="270d8-132">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="270d8-133">Örneğin, kaynak yapılandırmasının Kimliğini çalıştırmak istediğiniz bir blok betik ilk ise *ResourceName* ve kendi türünün *ResourceType*, bu özelliği kullanmak için sözdizimi `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="270d8-133">For example, if the ID of the resource configuration script block that you want to run first is *ResourceName* and its type is *ResourceType*, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|



## <a name="example"></a><span data-ttu-id="270d8-134">Örnek</span><span class="sxs-lookup"><span data-stu-id="270d8-134">Example</span></span>

<span data-ttu-id="270d8-135">Aşağıdaki yapılandırma, "Windows Ses" ve "Uzak Masaüstü Hizmetleri" Hizmetleri başlatılır.</span><span class="sxs-lookup"><span data-stu-id="270d8-135">The following configuration starts the "Windows Audio" and "Remote Desktop Services" services.</span></span>

```powershell
configuration ServiceSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        ServiceSet ServiceSetExample
        {
            Name        = @("TermService", "Audiosrv")
            StartupType = "Manual"
            State       = "Running"
        }
    }
}
```