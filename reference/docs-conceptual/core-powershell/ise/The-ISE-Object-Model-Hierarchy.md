---
ms.date: 2017-06-05
keywords: PowerShell cmdlet'i
title: "ISE nesne modeli hiyerarşisi"
ms.openlocfilehash: 2df6d40f39dbe14bd3f46a6400cde4a6e91052ef
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/08/2017
---
# <a name="the-ise-object-model-hierarchy"></a><span data-ttu-id="4feac-103">ISE nesne modeli hiyerarşisi</span><span class="sxs-lookup"><span data-stu-id="4feac-103">The ISE Object Model Hierarchy</span></span>
<span data-ttu-id="4feac-104">Bu konu, Windows PowerShell Tümleşik komut dosyası ortamı (ISE) parçası olan nesne gösterir.</span><span class="sxs-lookup"><span data-stu-id="4feac-104">This topic shows the hierarchy of objects that are part of Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="4feac-105">Windows PowerShell ISE Windows PowerShell 3.0 ve Windows PowerShell 4.0 dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="4feac-105">Windows PowerShell ISE is included in Windows PowerShell 3.0 and in Windows PowerShell 4.0.</span></span> <span data-ttu-id="4feac-106">Nesne tanımlayan sınıfının başvuru belgeleri için uygulamanız için bir nesne'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4feac-106">Click an object to take you to the reference documentation for the class that defines the object.</span></span>

## <a name="psise-object"></a><span data-ttu-id="4feac-107">$psISE nesnesi</span><span class="sxs-lookup"><span data-stu-id="4feac-107">$psISE Object</span></span>

<span data-ttu-id="4feac-108">**$PsISE** nesne [kök nesnesi](The-ObjectModelRoot-Object.md) Windows PowerShell ISE nesne hiyerarşisinin.</span><span class="sxs-lookup"><span data-stu-id="4feac-108">The **$psISE** object is the [root object](The-ObjectModelRoot-Object.md) of the Windows PowerShell ISE object hierarchy.</span></span>
<span data-ttu-id="4feac-109">En üst düzeyinde bulunan, aşağıdaki nesneleri kullanılabilir komut dosyası için hale getirir:</span><span class="sxs-lookup"><span data-stu-id="4feac-109">Located at the top level, it makes the following objects available for scripting:</span></span>

## <a name="psisecurrentfilethe-isefile-objectmd"></a>[<span data-ttu-id="4feac-110">$psISE.CurrentFile</span><span class="sxs-lookup"><span data-stu-id="4feac-110">$psISE.CurrentFile</span></span>](The-ISEFile-Object.md)

<span data-ttu-id="4feac-111">**$PsISE.CurrentFile** nesnesidir örneği [ISEFile](The-ISEFile-Object.md) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="4feac-111">The **$psISE.CurrentFile** object is an instance of the [ISEFile](The-ISEFile-Object.md) class.</span></span>

## <a name="psisecurrentpowershelltabthe-powershelltab-objectmd"></a>[<span data-ttu-id="4feac-112">$psISE.CurrentPowerShellTab</span><span class="sxs-lookup"><span data-stu-id="4feac-112">$psISE.CurrentPowerShellTab</span></span>](The-PowerShellTab-Object.md)

<span data-ttu-id="4feac-113">**$PsISE.CurrentPowerShellTab** nesnesidir örneği [PowerShellTab](The-PowerShellTab-Object.md) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="4feac-113">The **$psISE.CurrentPowerShellTab** object is an instance of the [PowerShellTab](The-PowerShellTab-Object.md) class.</span></span>

## <a name="psisecurrentvisiblehorizontaltool"></a><span data-ttu-id="4feac-114">$psISE.CurrentVisibleHorizontalTool</span><span class="sxs-lookup"><span data-stu-id="4feac-114">$psISE.CurrentVisibleHorizontalTool</span></span>

<span data-ttu-id="4feac-115">**$PsISE.CurrentVisibleHorizontalTool** nesnesidir örneği [ISEAddOnTool](The-ISEAddOnTool-Object.md) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="4feac-115">The **$psISE.CurrentVisibleHorizontalTool** object is an instance of the [ISEAddOnTool](The-ISEAddOnTool-Object.md) class.</span></span>
<span data-ttu-id="4feac-116">Şu anda yerleşik yüklü eklenti aracı Windows PowerShell ISE penceresi üst kenarına temsil eder.</span><span class="sxs-lookup"><span data-stu-id="4feac-116">It represents the installed add-on tool that is currently docked to the top edge of the Windows PowerShell ISE window.</span></span>

## <a name="psisecurrentvisibleverticaltool"></a><span data-ttu-id="4feac-117">$psISE.CurrentVisibleVerticalTool</span><span class="sxs-lookup"><span data-stu-id="4feac-117">$psISE.CurrentVisibleVerticalTool</span></span>

<span data-ttu-id="4feac-118">**$PsISE.CurrentVisibleHorizontalTool** nesnesidir örneği [ISEAddOnTool](The-ISEAddOnTool-Object.md) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="4feac-118">The **$psISE.CurrentVisibleHorizontalTool** object is an instance of the [ISEAddOnTool](The-ISEAddOnTool-Object.md) class.</span></span>
<span data-ttu-id="4feac-119">Şu anda yerleşik yüklü eklenti aracı Windows PowerShell ISE penceresi sağ kenarı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="4feac-119">It represents the installed add-on tool that is currently docked to the right-hand edge of the Windows PowerShell ISE window.</span></span>

## <a name="psiseoptionsthe-iseoptions-objectmd"></a>[<span data-ttu-id="4feac-120">$psISE.Options</span><span class="sxs-lookup"><span data-stu-id="4feac-120">$psISE.Options</span></span>](The-ISEOptions-Object.md)

<span data-ttu-id="4feac-121">**$PsISE.Options** nesnesidir örneği [ISEOptions](The-ISEOptions-Object.md) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="4feac-121">The **$psISE.Options** object is an instance of the [ISEOptions](The-ISEOptions-Object.md) class.</span></span>
<span data-ttu-id="4feac-122">ISEOptions nesne çeşitli Windows PowerShell ISE ayarlarını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="4feac-122">The ISEOptions object represents various settings for Windows PowerShell ISE.</span></span>
<span data-ttu-id="4feac-123">Microsoft.PowerShell.Host.ISE.ISEOptions sınıfının bir örneğidir.</span><span class="sxs-lookup"><span data-stu-id="4feac-123">It is an instance of the Microsoft.PowerShell.Host.ISE.ISEOptions class.</span></span>

## <a name="psisepowershelltabsthe-powershelltabcollection-objectmd"></a>[<span data-ttu-id="4feac-124">$psISE.PowerShellTabs</span><span class="sxs-lookup"><span data-stu-id="4feac-124">$psISE.PowerShellTabs</span></span>](The-PowerShellTabCollection-Object.md)

<span data-ttu-id="4feac-125">**$PsISE.PowerShellTabs** nesnesidir örneği [PowerShellTabCollection](The-PowerShellTabCollection-Object.md) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="4feac-125">The **$psISE.PowerShellTabs** object is an instance of the [PowerShellTabCollection](The-PowerShellTabCollection-Object.md) class.</span></span>
<span data-ttu-id="4feac-126">Yerel bilgisayarda veya uzak bilgisayarlarda bağlı ortamları çalıştırmak kullanılabilir Windows PowerShell temsil eden tüm açık PowerShell sekmeleri koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="4feac-126">It is a collection of all the currently open PowerShell tabs that represent the available Windows PowerShell run environments on the local computer or on connected remote computers.</span></span> <span data-ttu-id="4feac-127">Koleksiyonda her üye bir örneğidir [PowerShellTab](The-PowerShellTab-Object.md) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="4feac-127">Each member in the collection is an instance of the [PowerShellTab](The-PowerShellTab-Object.md) class.</span></span>

## <a name="see-also"></a><span data-ttu-id="4feac-128">Ayrıca bkz:</span><span class="sxs-lookup"><span data-stu-id="4feac-128">See Also</span></span>
- [<span data-ttu-id="4feac-129">Windows PowerShell ISE nesne modeli komut dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="4feac-129">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="4feac-130">Windows PowerShell ISE nesne modeli başvurusu</span><span class="sxs-lookup"><span data-stu-id="4feac-130">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md)