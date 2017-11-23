---
ms.date: 2017-06-12
author: rpsqrd
ms.topic: conceptual
keywords: "jea, powershell, güvenlik"
title: "JEA önkoşulları"
ms.openlocfilehash: 75d5db2ba446df1d461050d187dc1495a22fef18
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/12/2017
---
# <a name="prerequisites"></a><span data-ttu-id="f46af-103">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="f46af-103">Prerequisites</span></span>

> <span data-ttu-id="f46af-104">Uygulandığı öğe: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="f46af-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="f46af-105">Yalnızca yeterli Yönetimi Windows PowerShell 5.0 ve üzeri bulunan bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="f46af-105">Just Enough Administration is a feature included with Windows PowerShell 5.0 and higher.</span></span>
<span data-ttu-id="f46af-106">Bu konuda JEA kullanmaya başlamak için karşılanması gereken önkoşulları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f46af-106">This topic describes the prerequisites that must be satisfied in order to start using JEA.</span></span>

## <a name="install-jea"></a><span data-ttu-id="f46af-107">JEA yükleyin</span><span class="sxs-lookup"><span data-stu-id="f46af-107">Install JEA</span></span>

<span data-ttu-id="f46af-108">JEA Windows PowerShell 5. 0 ile kullanılabilir ve daha yüksek, ancak tam işlevsellik için sisteminizi PowerShell kullanılabilir en son sürümünü yüklemeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="f46af-108">JEA is available with Windows PowerShell 5.0 and higher, but for full functionality it is recommended that you install the latest version of PowerShell available for your system.</span></span>
<span data-ttu-id="f46af-109">Aşağıdaki tabloda, Windows Server'da JEA'in kullanılabilirlik açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="f46af-109">The following table describes JEA's availability on Windows Server:</span></span>

<span data-ttu-id="f46af-110">Sunucu işletim sistemi</span><span class="sxs-lookup"><span data-stu-id="f46af-110">Server Operating System</span></span>   | <span data-ttu-id="f46af-111">JEA kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="f46af-111">JEA Availability</span></span>
--------------------------|--------------------------------
<span data-ttu-id="f46af-112">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="f46af-112">Windows Server 2016</span></span>       | <span data-ttu-id="f46af-113">Önceden yüklenmiş</span><span class="sxs-lookup"><span data-stu-id="f46af-113">Preinstalled</span></span>
<span data-ttu-id="f46af-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="f46af-114">Windows Server 2012 R2</span></span>    | <span data-ttu-id="f46af-115">WMF 5.1 tam işlevsellikle</span><span class="sxs-lookup"><span data-stu-id="f46af-115">Full functionality with WMF 5.1</span></span>
<span data-ttu-id="f46af-116">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="f46af-116">Windows Server 2012</span></span>       | <span data-ttu-id="f46af-117">WMF 5.1 tam işlevsellikle</span><span class="sxs-lookup"><span data-stu-id="f46af-117">Full functionality with WMF 5.1</span></span>
<span data-ttu-id="f46af-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="f46af-118">Windows Server 2008 R2</span></span>    | <span data-ttu-id="f46af-119">İşlevleri azaltılmış<sup>1</sup> WMF 5.1 ile</span><span class="sxs-lookup"><span data-stu-id="f46af-119">Reduced functionality<sup>1</sup> with WMF 5.1</span></span>

<span data-ttu-id="f46af-120">Ev veya iş bilgisayarınızda JEA de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f46af-120">You can also use JEA on your home or work computer:</span></span>

<span data-ttu-id="f46af-121">İstemci işletim sistemi</span><span class="sxs-lookup"><span data-stu-id="f46af-121">Client Operating System</span></span>   | <span data-ttu-id="f46af-122">JEA kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="f46af-122">JEA Availability</span></span>
--------------------------|-----------------------------------------------------
<span data-ttu-id="f46af-123">Windows 10 1607 +</span><span class="sxs-lookup"><span data-stu-id="f46af-123">Windows 10 1607+</span></span>          | <span data-ttu-id="f46af-124">Önceden yüklenmiş</span><span class="sxs-lookup"><span data-stu-id="f46af-124">Preinstalled</span></span>
<span data-ttu-id="f46af-125">Windows 10 1603 1511</span><span class="sxs-lookup"><span data-stu-id="f46af-125">Windows 10 1603, 1511</span></span>     | <span data-ttu-id="f46af-126">Önceden, azaltılmış işlevsellik ile<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="f46af-126">Preinstalled, with reduced functionality<sup>2</sup></span></span>
<span data-ttu-id="f46af-127">Windows 10 1507</span><span class="sxs-lookup"><span data-stu-id="f46af-127">Windows 10 1507</span></span>           | <span data-ttu-id="f46af-128">Mevcut değil</span><span class="sxs-lookup"><span data-stu-id="f46af-128">Not available</span></span>
<span data-ttu-id="f46af-129">Windows 8, 8.1</span><span class="sxs-lookup"><span data-stu-id="f46af-129">Windows 8, 8.1</span></span>            | <span data-ttu-id="f46af-130">WMF 5.1 tam işlevsellikle</span><span class="sxs-lookup"><span data-stu-id="f46af-130">Full functionality with WMF 5.1</span></span>
<span data-ttu-id="f46af-131">Windows 7</span><span class="sxs-lookup"><span data-stu-id="f46af-131">Windows 7</span></span>                 | <span data-ttu-id="f46af-132">İşlevleri azaltılmış<sup>1</sup> WMF 5.1 ile</span><span class="sxs-lookup"><span data-stu-id="f46af-132">Reduced functionality<sup>1</sup> with WMF 5.1</span></span>

<span data-ttu-id="f46af-133"><sup>1</sup> JEA, Windows Server 2008 R2 veya Windows 7 üzerinde Grup yönetilen hizmet hesapları kullanacak şekilde yapılandırılamaz.</span><span class="sxs-lookup"><span data-stu-id="f46af-133"><sup>1</sup> JEA cannot be configured to use group managed service accounts on Windows Server 2008 R2 or Windows 7.</span></span>
<span data-ttu-id="f46af-134">Sanal hesaplar ve diğer JEA özellikleri *olan* desteklenir.</span><span class="sxs-lookup"><span data-stu-id="f46af-134">Virtual accounts and other JEA features *are* supported.</span></span>

<span data-ttu-id="f46af-135"><sup>2</sup> Windows 10 sürüm 1511 ve 1603 aşağıdaki JEA özellikleri desteklemez: Grup yönetilen hizmet hesabı, oturum yapılandırmaları koşullu erişim kuralları, kullanıcı sürücüsünde ve erişebilmesi için yerel kullanıcı hesapları olarak çalıştırmak.</span><span class="sxs-lookup"><span data-stu-id="f46af-135"><sup>2</sup> Windows 10 versions 1511 and 1603 do not support the following JEA features: running as a group managed service account, conditional access rules in session configurations, the user drive, and granting access to local user accounts.</span></span>
<span data-ttu-id="f46af-136">Bu özellikler için destek almak için Windows 1607 (Yıldönümü güncelleştirmesi) sürümüne güncelleştirin ya da daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="f46af-136">To get support for these features, update Windows to version 1607 (Anniversary Update) or higher.</span></span>

### <a name="check-which-version-of-powershell-is-installed"></a><span data-ttu-id="f46af-137">PowerShell hangi sürümünün yüklü denetleyin</span><span class="sxs-lookup"><span data-stu-id="f46af-137">Check which version of PowerShell is installed</span></span>

<span data-ttu-id="f46af-138">Sisteminizde yüklü PowerShell sürümünü denetlemek için kontrol `$PSVersionTable` bir Windows PowerShell isteminde değişken.</span><span class="sxs-lookup"><span data-stu-id="f46af-138">To check which version of PowerShell is installed on your system, check the `$PSVersionTable` variable in a Windows PowerShell prompt.</span></span>

```powershell
PS C:\> $PSVersionTable.PSVersion

Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      14393  1000
```

<span data-ttu-id="f46af-139">JEA, kullanıma hazır *ana* sürümüdür eşit veya bundan büyük **5**.</span><span class="sxs-lookup"><span data-stu-id="f46af-139">You are ready to use JEA if the *Major* version is equal to or greater than **5**.</span></span>
<span data-ttu-id="f46af-140">En iyi deneyim için ve en son özelliklere erişim sağlamak için PowerShell sürüme yükseltmeniz önerilir **5.1** mümkün olduğunda.</span><span class="sxs-lookup"><span data-stu-id="f46af-140">For the best experience, and to have access to all the latest features, it is recommended that you upgrade to PowerShell version **5.1** when possible.</span></span>

### <a name="install-windows-management-framework"></a><span data-ttu-id="f46af-141">Windows Management Framework'ü yükleme</span><span class="sxs-lookup"><span data-stu-id="f46af-141">Install Windows Management Framework</span></span>

<span data-ttu-id="f46af-142">PowerShell daha eski bir sürümü çalıştırıyorsanız, sisteminizi en son Windows Management Framework (WMF) güncelleştirmesi ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f46af-142">If you are running an older version of PowerShell, you will need to update your system with the latest Windows Management Framework (WMF) update.</span></span>
<span data-ttu-id="f46af-143">Güncelleştirme paketleri ve en son WMF sürüm notlarını bağlantı bulunan [Yükleme Merkezi'nden](https://aka.ms/WMF5).</span><span class="sxs-lookup"><span data-stu-id="f46af-143">Update packages and a link to the latest WMF release notes are available in the [Download Center](https://aka.ms/WMF5).</span></span>

<span data-ttu-id="f46af-144">Tüm sunucularınız yükseltmeden önce WMF İş yükünüzün uyumluluğunu test önerilir.</span><span class="sxs-lookup"><span data-stu-id="f46af-144">It is strongly recommended that you test your workload's compatibility with WMF before upgrading all of your servers.</span></span>

<span data-ttu-id="f46af-145">Windows 10 kullanıcıları Windows PowerShell geçerli sürümünü elde etmek için en son özellik güncelleştirmeleri yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f46af-145">Windows 10 users should install the latest feature updates to obtain the current version of Windows PowerShell.</span></span>

## <a name="enable-powershell-remoting"></a><span data-ttu-id="f46af-146">PowerShell uzaktan iletişimini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f46af-146">Enable PowerShell Remoting</span></span>

<span data-ttu-id="f46af-147">PowerShell uzaktan iletişimi JEA yerleşik olan temel sağlar.</span><span class="sxs-lookup"><span data-stu-id="f46af-147">PowerShell Remoting provides the foundation on which JEA is built.</span></span>
<span data-ttu-id="f46af-148">Bu nedenle PowerShell uzaktan iletişimi etkin emin olmak gerekli olan ve [düzgün güvenli](https://msdn.microsoft.com/en-us/powershell/scripting/setup/winrmsecurity) JEA kullanmadan önce sisteminizdeki.</span><span class="sxs-lookup"><span data-stu-id="f46af-148">It is therefore necessary to ensure PowerShell Remoting is enabled and [properly secured](https://msdn.microsoft.com/en-us/powershell/scripting/setup/winrmsecurity) on your system before you can use JEA.</span></span>

<span data-ttu-id="f46af-149">PowerShell uzaktan iletişimi, Windows Server 2012, 2012 R2 ve 2016 varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="f46af-149">PowerShell Remoting is enabled by default on Windows Server 2012, 2012 R2, and 2016.</span></span>
<span data-ttu-id="f46af-150">PowerShell uzaktan iletişimi yükseltilmiş bir PowerShell penceresinde aşağıdaki komutu çalıştırarak etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f46af-150">You can enable PowerShell Remoting by running the following command in an elevated PowerShell window.</span></span>

```powershell
Enable-PSRemoting
```

## <a name="enable-powershell-module-and-script-block-logging-optional"></a><span data-ttu-id="f46af-151">PowerShell modülü ve komut dosyası bloğunun günlüğünü (isteğe bağlı) etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f46af-151">Enable PowerShell module and script block logging (optional)</span></span>

<span data-ttu-id="f46af-152">Aşağıdaki adımlar, sisteminizdeki tüm PowerShell eylemler için günlük kaydını etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f46af-152">The following steps enable logging for all PowerShell actions on your system.</span></span>
<span data-ttu-id="f46af-153">PowerShell günlük modülü için JEA gerekli değildir, ancak bu komutları kullanıcıların çalışmasını sağlamak için açmanız önerilir merkezi bir konumda kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="f46af-153">PowerShell Module Logging is not required for JEA, however it is strongly recommended that you turn it on to ensure the commands users run are logged in a central location.</span></span>

<span data-ttu-id="f46af-154">PowerShell modülü günlüğü ilkesini Grup İlkesi kullanarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f46af-154">You can configure the PowerShell Module Logging policy using Group Policy.</span></span>

1. <span data-ttu-id="f46af-155">Bir iş istasyonunda yerel Grup İlkesi Düzenleyicisi'ni veya bir Grup İlkesi nesnesi bir Active Directory etki alanı denetleyicisinde Grup İlkesi Yönetim Konsolu'nu açın</span><span class="sxs-lookup"><span data-stu-id="f46af-155">Open the Local Group Policy Editor on a workstation or a Group Policy Object in the Group Policy Management Console on an Active Directory Domain Controller</span></span>
2. <span data-ttu-id="f46af-156">Gidin **Bilgisayar Yapılandırması\\Yönetim Şablonları\\Windows bileşenleri\\Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="f46af-156">Navigate to **Computer Configuration\\Administrative Templates\\Windows Components\\Windows PowerShell**</span></span>
3. <span data-ttu-id="f46af-157">Çift tıklatın **modülü günlük özelliğini açın**</span><span class="sxs-lookup"><span data-stu-id="f46af-157">Double click on **Turn on Module Logging**</span></span>
4. <span data-ttu-id="f46af-158">Tıklatın **etkin**</span><span class="sxs-lookup"><span data-stu-id="f46af-158">Click **Enabled**</span></span>
5. <span data-ttu-id="f46af-159">Seçenekler bölümünde tıklayın **Göster** modül adlarını yanındaki</span><span class="sxs-lookup"><span data-stu-id="f46af-159">In the Options section, click on **Show** next to Module Names</span></span>
6. <span data-ttu-id="f46af-160">Türü "**\***" açılır pencerede içinde.</span><span class="sxs-lookup"><span data-stu-id="f46af-160">Type "**\***" in the pop up window.</span></span> <span data-ttu-id="f46af-161">PowerShell komutları tüm modüllerden oturum bildirir.</span><span class="sxs-lookup"><span data-stu-id="f46af-161">This instructs PowerShell to log commands from all modules.</span></span>
7. <span data-ttu-id="f46af-162">Tıklatın **Tamam** ilkesini ayarlamak için</span><span class="sxs-lookup"><span data-stu-id="f46af-162">Click **OK** to set the policy</span></span>
8. <span data-ttu-id="f46af-163">Çift tıklatın **PowerShell betik bloğu günlük özelliğini açın**</span><span class="sxs-lookup"><span data-stu-id="f46af-163">Double click on **Turn on PowerShell Script Block Logging**</span></span>
9. <span data-ttu-id="f46af-164">Tıklatın **etkin**</span><span class="sxs-lookup"><span data-stu-id="f46af-164">Click **Enabled**</span></span>
10. <span data-ttu-id="f46af-165">Tıklatın **Tamam** ilkesini ayarlamak için</span><span class="sxs-lookup"><span data-stu-id="f46af-165">Click **OK** to set the policy</span></span>
11. <span data-ttu-id="f46af-166">(Etki alanına katılmış makinelerde yalnızca) Çalıştırma **gpupdate** veya güncelleştirilmiş ilke işlemek ve ayarları uygulamak Grup İlkesi için bekleyin</span><span class="sxs-lookup"><span data-stu-id="f46af-166">(On domain-joined machines only) Run **gpupdate** or wait for Group Policy to process the updated policy and apply the settings</span></span>

<span data-ttu-id="f46af-167">Grup İlkesi aracılığıyla sistem genelinde PowerShell transcription de etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f46af-167">You can also enable system-wide PowerShell transcription through Group Policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f46af-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f46af-168">Next steps</span></span>

- [<span data-ttu-id="f46af-169">Bir rol özelliği dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="f46af-169">Create a role capability file</span></span>](role-capabilities.md)
- [<span data-ttu-id="f46af-170">Oturum yapılandırma dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="f46af-170">Create a session configuration file</span></span>](session-configurations.md)

## <a name="see-also"></a><span data-ttu-id="f46af-171">Ayrıca bkz:</span><span class="sxs-lookup"><span data-stu-id="f46af-171">See also</span></span>

- [<span data-ttu-id="f46af-172">PowerShell uzaktan iletişimi ve WinRM güvenlik hakkında ek bilgi</span><span class="sxs-lookup"><span data-stu-id="f46af-172">Additional information about PowerShell Remoting and WinRM security</span></span>](https://msdn.microsoft.com/en-us/powershell/scripting/setup/winrmsecurity)
- [<span data-ttu-id="f46af-173">*PowerShell ♥ mavi takım* güvenlik blog gönderisi</span><span class="sxs-lookup"><span data-stu-id="f46af-173">*PowerShell ♥ the Blue Team* blog post on security</span></span>](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)
