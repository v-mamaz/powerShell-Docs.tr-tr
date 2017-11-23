---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: Galeri, powershell, cmdlet, psgallery
title: psgallery_unlist_items
ms.openlocfilehash: 8fa09c77e144f14bf0fd3493dff7650897100715
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/12/2017
---
# <a name="unlisting-items"></a><span data-ttu-id="0f927-103">Unlisting öğeleri</span><span class="sxs-lookup"><span data-stu-id="0f927-103">Unlisting items</span></span>

<span data-ttu-id="0f927-104">**PowerShell Galerisi'nden bir seçenek olarak gösterilmeyen bir öğe kaldırıldığında neden?**</span><span class="sxs-lookup"><span data-stu-id="0f927-104">**Why is removing an item from PowerShell Gallery not exposed as an option?**</span></span>

<span data-ttu-id="0f927-105">PowerShell Galerisi, kullanıcıların kendilerine öğelerini kalıcı olarak silmesini desteklemez.</span><span class="sxs-lookup"><span data-stu-id="0f927-105">The PowerShell Gallery does not support users permanently deleting their items.</span></span> <span data-ttu-id="0f927-106">Bu, diğerleri gelecekteki olası kesmeleri hakkında endişelenmeden bulunan öğelerinizi bağımlılıkları yapılacak sağlar.</span><span class="sxs-lookup"><span data-stu-id="0f927-106">This enables others to take dependencies on your items without worrying about possible breaks in the future.</span></span> <span data-ttu-id="0f927-107">Örneğin, Azure modülünü Pester modül bağlıdır ve sonra da kullanıcı artık Azure modül Galerisi'nden kaldırılır Pester modülü kullanır.</span><span class="sxs-lookup"><span data-stu-id="0f927-107">For example, if the Pester module depends on the Azure module and the Azure module is removed from the gallery, then user can no longer uses the Pester module.</span></span>

<span data-ttu-id="0f927-108">Bir öğeyi kaldırmak yerine ancak, bunu yerine unlist.</span><span class="sxs-lookup"><span data-stu-id="0f927-108">Instead of removing an item, however, you can unlist it instead.</span></span>

<span data-ttu-id="0f927-109">**Ne unlisting PowerShell Galerisi bir öğede musunuz?**</span><span class="sxs-lookup"><span data-stu-id="0f927-109">**What does unlisting an item on PowerShell Gallery do?**</span></span>

<span data-ttu-id="0f927-110">Modül veya PowerShell Galerisi komut gibi bir öğe unlisting öğeleri sekmesinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="0f927-110">Unlisting an item such as module or script on PowerShell Gallery will remove it from the Items tab.</span></span>
<span data-ttu-id="0f927-111">Ayrıca, listede bulunmayan öğeleri arama çubuğunu kullanarak bulunabilirlik olmaz.</span><span class="sxs-lookup"><span data-stu-id="0f927-111">In addition, unlisted items will not be discoverable using the search bar.</span></span>
<span data-ttu-id="0f927-112">Listede bulunmayan bir öğe indirmek için yalnızca tam adı ve sürümü öğenin belirtmek için yoludur.</span><span class="sxs-lookup"><span data-stu-id="0f927-112">The only way to download an unlisted item is to specify the exact name and version of the item.</span></span>
<span data-ttu-id="0f927-113">Bu nedenle, bir öğe unlisting bağımlı komut dosyaları veya diğer modüller kesintiye uğrar değil.</span><span class="sxs-lookup"><span data-stu-id="0f927-113">Because of this, the unlisting of an item will not break other modules or scripts that depend on it.</span></span>

<span data-ttu-id="0f927-114">Öğenizi unlist için öğesi Ayrıntılar sayfasını ziyaret edin ve 'Öğeyi sil' seçin.</span><span class="sxs-lookup"><span data-stu-id="0f927-114">To unlist your item, visit the item details page and select 'Delete Item'.</span></span> <span data-ttu-id="0f927-115">'Listelendi' onay kutusunun işaretini kaldırın ve Kaydet'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="0f927-115">Uncheck the 'Listed' checkbox, and click Save.</span></span>

<span data-ttu-id="0f927-116">**Bir öğe nasıl kaldırabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="0f927-116">**How can I remove an item?**</span></span>

<span data-ttu-id="0f927-117">Öğe silme gerekli olduğu bir senaryo karşılaşırsanız, PowerShell Galerisi yöneticileri ile iletişime geçin.</span><span class="sxs-lookup"><span data-stu-id="0f927-117">If you experience a scenario where item deletion is necessary, contact the PowerShell Gallery Administrators.</span></span>
<span data-ttu-id="0f927-118">Geçerli silme senaryolar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0f927-118">Valid deletion scenarios are:</span></span>
- <span data-ttu-id="0f927-119">Telif hakkı ihlali sorunları.</span><span class="sxs-lookup"><span data-stu-id="0f927-119">Issues of copyright infringement.</span></span>
- <span data-ttu-id="0f927-120">Öğe zararlı içerik içeriyor.</span><span class="sxs-lookup"><span data-stu-id="0f927-120">Item contains potentially harmful content.</span></span>
- <span data-ttu-id="0f927-121">Öğesi hassas verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="0f927-121">Item contains sensitive data.</span></span>

<span data-ttu-id="0f927-122">Bir silme öğesi isteği PowerShell Galerisi yöneticilere göndermek için öğenizin ayrıntı sayfasını ziyaret edin ve Destek birimine başvurun seçin.</span><span class="sxs-lookup"><span data-stu-id="0f927-122">To submit a Delete Item Request to the PowerShell Gallery Administrators, visit your item's detail page and select Contact Support.</span></span>  

