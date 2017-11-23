---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, Kur
ms.openlocfilehash: 80852bf750700d549de24e150ffd89ac55b7bf88
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/12/2017
---
# <a name="network-switch-management-with-powershell"></a><span data-ttu-id="fbce2-102">PowerShell ile ağ anahtarı yönetimi</span><span class="sxs-lookup"><span data-stu-id="fbce2-102">Network Switch Management with PowerShell</span></span>

<span data-ttu-id="fbce2-103">**Get-NetworkSwitchEthernetPort** cmdlet'i şimdi örnekleri aşağıdaki ek bilgilerle döndürür:</span><span class="sxs-lookup"><span data-stu-id="fbce2-103">The **Get-NetworkSwitchEthernetPort** cmdlet now returns the following additional information with instances:</span></span>

- <span data-ttu-id="fbce2-104">IPADDRESS – bağlantı noktasıyla ilişkili IP adresi</span><span class="sxs-lookup"><span data-stu-id="fbce2-104">IPAddress – the IP address associated with the port</span></span>
- <span data-ttu-id="fbce2-105">PortMode – bağlantı noktası modu: erişim, yönlendirme veya santral</span><span class="sxs-lookup"><span data-stu-id="fbce2-105">PortMode – the port mode: access, route, or trunk</span></span>
- <span data-ttu-id="fbce2-106">Bu bağlantı noktası erişim modunda VLAN kimliği AccessVLAN – ilişkili</span><span class="sxs-lookup"><span data-stu-id="fbce2-106">AccessVLAN – the ID of the VLAN associated with this port in access mode</span></span>
- <span data-ttu-id="fbce2-107">Bu bağlantı noktası santral modundaki kimlikleri VLAN'ları, listesini TrunkedVLANList – ilişkili</span><span class="sxs-lookup"><span data-stu-id="fbce2-107">TrunkedVLANList – a list of IDs of VLANs associated with this port in trunk mode</span></span>

## <a name="fundamental-network-switch-management-with-windows-powershell"></a><span data-ttu-id="fbce2-108">Windows PowerShell ile temel ağ anahtarı yönetimi</span><span class="sxs-lookup"><span data-stu-id="fbce2-108">Fundamental network switch management with Windows PowerShell</span></span>

<span data-ttu-id="fbce2-109">WMF 5. 0'da, sunulan ağ geçiş cmdlet'leri anahtarı, sanal LAN (VLAN) ve temel Katman 2 ağ anahtarı bağlantı noktası yapılandırmasını Windows Server 2012 R2 logo sertifikalı ağ anahtarlara uygulamak sağlar.</span><span class="sxs-lookup"><span data-stu-id="fbce2-109">The Network Switch cmdlets, introduced in WMF 5.0, enable you to apply switch, virtual LAN (VLAN), and basic Layer 2 network switch port configuration to Windows Server 2012 R2 logo-certified network switches.</span></span> <span data-ttu-id="fbce2-110">Microsoft destek kaydedilmiş kalır [veri merkezi soyutlama](http://technet.microsoft.com/en-us/cloud/dal.aspx) düzeyi (DAL) görme ve müşterilerimizin ve iş ortakları bu alan için değer göstermek için.</span><span class="sxs-lookup"><span data-stu-id="fbce2-110">Microsoft remains committed to supporting the [Datacenter Abstraction](http://technet.microsoft.com/en-us/cloud/dal.aspx) Layer (DAL) vision, and to show value for our customers and partners in this space.</span></span> <span data-ttu-id="fbce2-111">Bu cmdlet'leri kullanarak şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fbce2-111">Using these cmdlets you can perform:</span></span>

- <span data-ttu-id="fbce2-112">Genel yapılandırma, gibi anahtarı:</span><span class="sxs-lookup"><span data-stu-id="fbce2-112">Global switch configuration, such as:</span></span>
    - <span data-ttu-id="fbce2-113">Küme ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="fbce2-113">Set host name</span></span>
    - <span data-ttu-id="fbce2-114">Set anahtar başlığı</span><span class="sxs-lookup"><span data-stu-id="fbce2-114">Set switch banner</span></span>
    - <span data-ttu-id="fbce2-115">Yapılandırma Sürdür</span><span class="sxs-lookup"><span data-stu-id="fbce2-115">Persist configuration</span></span>
    - <span data-ttu-id="fbce2-116">Etkinleştirmek veya özelliği devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="fbce2-116">Enable or disable feature</span></span>

- <span data-ttu-id="fbce2-117">VLAN yapılandırması:</span><span class="sxs-lookup"><span data-stu-id="fbce2-117">VLAN configuration:</span></span>
    - <span data-ttu-id="fbce2-118">Oluşturma veya VLAN kaldırma</span><span class="sxs-lookup"><span data-stu-id="fbce2-118">Create or remove VLAN</span></span>
    - <span data-ttu-id="fbce2-119">Etkinleştirmek veya VLAN devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="fbce2-119">Enable or disable VLAN</span></span>
    - <span data-ttu-id="fbce2-120">VLAN listeleme</span><span class="sxs-lookup"><span data-stu-id="fbce2-120">Enumerate VLAN</span></span>
    - <span data-ttu-id="fbce2-121">VLAN kolay adını ayarlama</span><span class="sxs-lookup"><span data-stu-id="fbce2-121">Set friendly name to a VLAN</span></span>

- <span data-ttu-id="fbce2-122">Katman 2 bağlantı noktası yapılandırması:</span><span class="sxs-lookup"><span data-stu-id="fbce2-122">Layer 2 port configuration:</span></span>
    - <span data-ttu-id="fbce2-123">Bağlantı noktalarını listeleme</span><span class="sxs-lookup"><span data-stu-id="fbce2-123">Enumerate ports</span></span>
    - <span data-ttu-id="fbce2-124">Etkinleştirmek veya devre dışı bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="fbce2-124">Enable or disable ports</span></span>
    - <span data-ttu-id="fbce2-125">Set bağlantı noktası modları ve özellikleri</span><span class="sxs-lookup"><span data-stu-id="fbce2-125">Set port modes and properties</span></span>
    - <span data-ttu-id="fbce2-126">Ekleme veya VLAN santral veya bağlantı noktası erişimi ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="fbce2-126">Add or associate VLAN to Trunk or Access on the port</span></span>

<span data-ttu-id="fbce2-127">Tüm NetworkSwitch cmdlet'leri için bakarak keşfetmeye başlayın!</span><span class="sxs-lookup"><span data-stu-id="fbce2-127">Start exploring by looking for all of the NetworkSwitch cmdlets!</span></span>

```powershell
PS> Get-Command *-NetworkSwitch*

| CommandType | Name                                      | Source        |
|-------------|-------------------------------------------|---------------|
|             |                                           |               |
| Function    | Disable-NetworkSwitchEthernetPort         | NetworkSwitch |
| Function    | Disable-NetworkSwitchFeature              | NetworkSwitch |
| Function    | Disable-NetworkSwitchVlan                 | NetworkSwitch |
| Function    | Enable-NetworkSwitchEthernetPort          | NetworkSwitch |
| Function    | Enable-NetworkSwitchFeature               | NetworkSwitch |
| Function    | Enable-NetworkSwitchVlan                  | NetworkSwitch |
| Function    | Get-NetworkSwitchEthernetPort             | NetworkSwitch |
| Function    | Get-NetworkSwitchFeature                  | NetworkSwitch |
| Function    | Get-NetworkSwitchGlobalData               | NetworkSwitch |
| Function    | Get-NetworkSwitchVlan                     | NetworkSwitch |
| Function    | New-NetworkSwitchVlan                     | NetworkSwitch |
| Function    | Remove-NetworkSwitchEthernetPortIPAddress | NetworkSwitch |
| Function    | Remove-NetworkSwitchVlan                  | NetworkSwitch |
| Function    | Restore-NetworkSwitchConfiguration        | NetworkSwitch |
| Function    | Save-NetworkSwitchConfiguration           | NetworkSwitch |
| Function    | Set-NetworkSwitchEthernetPortIPAddress    | NetworkSwitch |
| Function    | Set-NetworkSwitchPortMode                 | NetworkSwitch |
| Function    | Set-NetworkSwitchPortProperty             | NetworkSwitch |
| Function    | Set-NetworkSwitchVlanProperty             | NetworkSwitch |
```

<span data-ttu-id="fbce2-128">Daha fazla bilgi Gamze Snover'ın WMF 5.0 Önizleme Duyurusu blog postasına mevcuttur: <http://blogs.technet.com/b/windowsserver/archive/2014/04/03/windows-management-framework-v5-preview.aspx></span><span class="sxs-lookup"><span data-stu-id="fbce2-128">More information is available in Jeffrey Snover’s WMF 5.0 Preview announcement blog post: <http://blogs.technet.com/b/windowsserver/archive/2014/04/03/windows-management-framework-v5-preview.aspx></span></span>
