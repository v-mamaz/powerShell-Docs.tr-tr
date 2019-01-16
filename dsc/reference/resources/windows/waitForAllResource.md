---
ms.date: 06/12/2017
keywords: DSC, powershell, yapılandırma, Kurulum
title: DSC WaitForAll kaynak
ms.openlocfilehash: 1e891f1aecbdbe641973669f71f22664ad8ea16c
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048691"
---
# <a name="dsc-waitforall-resource"></a><span data-ttu-id="babdf-103">DSC WaitForAll kaynak</span><span class="sxs-lookup"><span data-stu-id="babdf-103">DSC WaitForAll Resource</span></span>

> <span data-ttu-id="babdf-104">Şunun için geçerlidir: Windows PowerShell 5.0 ve üzeri</span><span class="sxs-lookup"><span data-stu-id="babdf-104">Applies To: Windows PowerShell 5.0 and later</span></span>

<span data-ttu-id="babdf-105">**WaitForAll** Desired State Configuration ' nı (DSC) kaynak, bir düğüm bloğunda içinde kullanılabilir bir [DSC Yapılandırması](../../../configurations/configurations.md) diğer düğümlerde yapılandırmalarında bağımlılıklarını belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="babdf-105">The **WaitForAll** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](../../../configurations/configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="babdf-106">Bu kaynak tarafından belirtilen kaynağı, başarılı **ResourceName** özelliği içinde tanımlanan tüm hedef düğümler üzerinde istenen durumda **NodeName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="babdf-106">This resource succeeds if the resource specified by the **ResourceName** property is in the desired state on all target nodes defined in the **NodeName** property.</span></span>

## <a name="syntax"></a><span data-ttu-id="babdf-107">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="babdf-107">Syntax</span></span>

```
WaitForAll [string] #ResourceName
{
    ResourceName = [string]
    NodeName = [string]
    [ RetryIntervalSec = [Uint64] ]
    [ RetryCount = [Uint32] ]
    [ ThrottleLimit = [Uint32]]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="babdf-108">Özellikler</span><span class="sxs-lookup"><span data-stu-id="babdf-108">Properties</span></span>

|  <span data-ttu-id="babdf-109">Özellik</span><span class="sxs-lookup"><span data-stu-id="babdf-109">Property</span></span>  |  <span data-ttu-id="babdf-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="babdf-110">Description</span></span>   |
|---|---|
| <span data-ttu-id="babdf-111">ResourceName</span><span class="sxs-lookup"><span data-stu-id="babdf-111">ResourceName</span></span>| <span data-ttu-id="babdf-112">Bağımlı kaynak adı.</span><span class="sxs-lookup"><span data-stu-id="babdf-112">The resource name to depend on.</span></span> <span data-ttu-id="babdf-113">Bu kaynak farklı bir yapılandırmaya aitse, adı olarak Biçimlendir "[__ResourceType__]__ResourceName__:: [__ConfigurationName__]:: [ __ConfigurationName__] "</span><span class="sxs-lookup"><span data-stu-id="babdf-113">If this resource belongs to a different configuration, format the name as "[__ResourceType__]__ResourceName__::[__ConfigurationName__]::[__ConfigurationName__]"</span></span>|
| <span data-ttu-id="babdf-114">NodeName</span><span class="sxs-lookup"><span data-stu-id="babdf-114">NodeName</span></span>| <span data-ttu-id="babdf-115">Hedef düğümleri kaynak bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="babdf-115">The target nodes of the resource to depend on.</span></span>|
| <span data-ttu-id="babdf-116">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="babdf-116">RetryIntervalSec</span></span>| <span data-ttu-id="babdf-117">Yeniden denemeden önce saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="babdf-117">The number of seconds before retrying.</span></span> <span data-ttu-id="babdf-118">Minimum is 1.</span><span class="sxs-lookup"><span data-stu-id="babdf-118">Minimum is 1.</span></span>|
| <span data-ttu-id="babdf-119">retryCount</span><span class="sxs-lookup"><span data-stu-id="babdf-119">RetryCount</span></span>| <span data-ttu-id="babdf-120">Yeniden deneme sayısı.</span><span class="sxs-lookup"><span data-stu-id="babdf-120">The maximum number of times to retry.</span></span>|
| <span data-ttu-id="babdf-121">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="babdf-121">ThrottleLimit</span></span>| <span data-ttu-id="babdf-122">Aynı anda bağlanmak makineleri sayısı.</span><span class="sxs-lookup"><span data-stu-id="babdf-122">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="babdf-123">Yeni-cimsession varsayılan varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="babdf-123">Default is new-cimsession default.</span></span>|
| <span data-ttu-id="babdf-124">DependsOn</span><span class="sxs-lookup"><span data-stu-id="babdf-124">DependsOn</span></span> | <span data-ttu-id="babdf-125">Bu kaynağı yapılandırılmadan önce başka bir kaynak yapılandırmasını çalıştırmanız gerektiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="babdf-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="babdf-126">Örneğin, kaynak yapılandırmasının Kimliğini çalıştırmak istediğiniz bir blok betik ilk ise __ResourceName__ ve kendi türünün __ResourceType__, bu özelliği kullanmak için sözdizimi `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="babdf-126">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="babdf-127">Örnek</span><span class="sxs-lookup"><span data-stu-id="babdf-127">Example</span></span>

<span data-ttu-id="babdf-128">Bu kaynağı kullanmaya ilişkin bir örnek için bkz: [çapraz düğüm bağımlılıklarını belirtme](../../../configurations/crossNodeDependencies.md)</span><span class="sxs-lookup"><span data-stu-id="babdf-128">For an example of how to use this resource, see [Specifying cross-node dependencies](../../../configurations/crossNodeDependencies.md)</span></span>