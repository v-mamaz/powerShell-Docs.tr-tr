---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, Kur
ms.openlocfilehash: 2c3cc6d5d226daf22c7ee83a1b7068d6a08b7f45
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/12/2017
---
# <a name="script-tracing-and-logging"></a><span data-ttu-id="ae93e-102">Komut dosyası izleme ve kaydetme</span><span class="sxs-lookup"><span data-stu-id="ae93e-102">Script Tracing and Logging</span></span>

<span data-ttu-id="ae93e-103">Windows PowerShell zaten varken **LogPipelineExecutionDetails** Grup İlkesi cmdlet'leri çağırma oturum ayarlama, PowerShell'in komut dosyası dili oturum ve/veya denetim isteyebilirsiniz özellikleri Eskinin sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ae93e-103">While Windows PowerShell already has the **LogPipelineExecutionDetails** Group Policy setting to log the invocation of cmdlets, PowerShell’s scripting language has plenty of features that you might want to log and/or audit.</span></span> <span data-ttu-id="ae93e-104">Yeni betik ayrıntılı izleme özelliği, ayrıntılı izleme ve çözümleme sisteminde Windows PowerShell komut dosyası kullanımı olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="ae93e-104">The new Detailed Script Tracing feature lets you enable detailed tracking and analysis of Windows PowerShell scripting use on a system.</span></span> <span data-ttu-id="ae93e-105">Ayrıntılı betik izleme etkinleştirdikten sonra Windows PowerShell tüm komut dosyası blokları ETW olay günlüğüne kaydeder. **Microsoft-Windows-PowerShell/Operational**.</span><span class="sxs-lookup"><span data-stu-id="ae93e-105">After you enable detailed script tracing, Windows PowerShell logs all script blocks to the ETW event log, **Microsoft-Windows-PowerShell/Operational**.</span></span> <span data-ttu-id="ae93e-106">Bir betik bloğu başka bir betik bloğu (örneğin, bir dizesine Invoke-Expression cmdlet'ini çağıran bir betik) oluşturursa, sonuçta elde edilen bu betik bloğu da günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="ae93e-106">If a script block creates another script block (for example, a script that calls the Invoke-Expression cmdlet on a string), that resulting script block is logged as well.</span></span>

<span data-ttu-id="ae93e-107">Bu olayların günlüğe kaydedilmesi, aracılığıyla etkinleştirilebilir **PowerShell betik bloğu günlük özelliğini açın** Grup İlkesi ayarı (Yönetim Şablonları -> Windows bileşenlerini Windows PowerShell ->).</span><span class="sxs-lookup"><span data-stu-id="ae93e-107">Logging of these events can be enabled through the **Turn on PowerShell Script Block Logging** Group Policy setting (in Administrative Templates -> Windows Components -> Windows PowerShell).</span></span>

<span data-ttu-id="ae93e-108">Olaylar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ae93e-108">The events are:</span></span>

| <span data-ttu-id="ae93e-109">Kanal</span><span class="sxs-lookup"><span data-stu-id="ae93e-109">Channel</span></span> | <span data-ttu-id="ae93e-110">İşletimsel</span><span class="sxs-lookup"><span data-stu-id="ae93e-110">Operational</span></span>                                 |
|---------|---------------------------------------------|
| <span data-ttu-id="ae93e-111">Düzey</span><span class="sxs-lookup"><span data-stu-id="ae93e-111">Level</span></span>   | <span data-ttu-id="ae93e-112">Verbose</span><span class="sxs-lookup"><span data-stu-id="ae93e-112">Verbose</span></span>                                     |
| <span data-ttu-id="ae93e-113">İşlem kodu</span><span class="sxs-lookup"><span data-stu-id="ae93e-113">Opcode</span></span>  | <span data-ttu-id="ae93e-114">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="ae93e-114">Create</span></span>                                      |
| <span data-ttu-id="ae93e-115">Görev</span><span class="sxs-lookup"><span data-stu-id="ae93e-115">Task</span></span>    | <span data-ttu-id="ae93e-116">CommandStart</span><span class="sxs-lookup"><span data-stu-id="ae93e-116">CommandStart</span></span>                                |
| <span data-ttu-id="ae93e-117">Anahtar sözcüğü</span><span class="sxs-lookup"><span data-stu-id="ae93e-117">Keyword</span></span> | <span data-ttu-id="ae93e-118">Çalışma alanı</span><span class="sxs-lookup"><span data-stu-id="ae93e-118">Runspace</span></span>                                    |
| <span data-ttu-id="ae93e-119">Olay Kimliği</span><span class="sxs-lookup"><span data-stu-id="ae93e-119">EventId</span></span> | <span data-ttu-id="ae93e-120">Engine_ScriptBlockCompiled (0x1008 = 4104)</span><span class="sxs-lookup"><span data-stu-id="ae93e-120">Engine_ScriptBlockCompiled (0x1008 = 4104)</span></span>  |
| <span data-ttu-id="ae93e-121">İleti</span><span class="sxs-lookup"><span data-stu-id="ae93e-121">Message</span></span> | <span data-ttu-id="ae93e-122">Scriptblock metin (%1% 2) oluşturma:</span><span class="sxs-lookup"><span data-stu-id="ae93e-122">Creating Scriptblock text (%1 of %2):</span></span> </br> <span data-ttu-id="ae93e-123">%3</span><span class="sxs-lookup"><span data-stu-id="ae93e-123">%3</span></span> </br> <span data-ttu-id="ae93e-124">ScriptBlock kimliği: %4</span><span class="sxs-lookup"><span data-stu-id="ae93e-124">ScriptBlock ID: %4</span></span> |


<span data-ttu-id="ae93e-125">İletiye ekli derlenmiş betik bloğu kapsamını metindir.</span><span class="sxs-lookup"><span data-stu-id="ae93e-125">The text embedded in the message is the extent of the script block compiled.</span></span> <span data-ttu-id="ae93e-126">Betik bloğu yaşam süreleri boyunca tutulur bir GUID kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="ae93e-126">The ID is a GUID that is retained for the life of the script block.</span></span>

<span data-ttu-id="ae93e-127">Ayrıntılı günlük kaydını etkinleştirdiğinizde, özellik yazma başlamak ve işaretçileri bitiş:</span><span class="sxs-lookup"><span data-stu-id="ae93e-127">When you enable verbose logging, the feature writes begin and end markers:</span></span>

| <span data-ttu-id="ae93e-128">Kanal</span><span class="sxs-lookup"><span data-stu-id="ae93e-128">Channel</span></span> | <span data-ttu-id="ae93e-129">İşletimsel</span><span class="sxs-lookup"><span data-stu-id="ae93e-129">Operational</span></span>                                            |
|---------|--------------------------------------------------------|
| <span data-ttu-id="ae93e-130">Düzey</span><span class="sxs-lookup"><span data-stu-id="ae93e-130">Level</span></span>   | <span data-ttu-id="ae93e-131">Verbose</span><span class="sxs-lookup"><span data-stu-id="ae93e-131">Verbose</span></span>                                                |
| <span data-ttu-id="ae93e-132">İşlem kodu</span><span class="sxs-lookup"><span data-stu-id="ae93e-132">Opcode</span></span>  | <span data-ttu-id="ae93e-133">Açın (/ Kapat)</span><span class="sxs-lookup"><span data-stu-id="ae93e-133">Open (/ Close)</span></span>                                         |
| <span data-ttu-id="ae93e-134">Görev</span><span class="sxs-lookup"><span data-stu-id="ae93e-134">Task</span></span>    | <span data-ttu-id="ae93e-135">CommandStart (/ CommandStop)</span><span class="sxs-lookup"><span data-stu-id="ae93e-135">CommandStart (/ CommandStop)</span></span>                           |
| <span data-ttu-id="ae93e-136">Anahtar sözcüğü</span><span class="sxs-lookup"><span data-stu-id="ae93e-136">Keyword</span></span> | <span data-ttu-id="ae93e-137">Çalışma alanı</span><span class="sxs-lookup"><span data-stu-id="ae93e-137">Runspace</span></span>                                               |
| <span data-ttu-id="ae93e-138">Olay Kimliği</span><span class="sxs-lookup"><span data-stu-id="ae93e-138">EventId</span></span> | <span data-ttu-id="ae93e-139">ScriptBlock\_çağırma\_Başlat\_ayrıntı (0x1009 = 4105) /</span><span class="sxs-lookup"><span data-stu-id="ae93e-139">ScriptBlock\_Invoke\_Start\_Detail (0x1009 = 4105) /</span></span> </br> <span data-ttu-id="ae93e-140">ScriptBlock\_çağırma\_tam\_ayrıntı (0x100A Sınır = 4106)</span><span class="sxs-lookup"><span data-stu-id="ae93e-140">ScriptBlock\_Invoke\_Complete\_Detail (0x100A = 4106)</span></span> |
| <span data-ttu-id="ae93e-141">İleti</span><span class="sxs-lookup"><span data-stu-id="ae93e-141">Message</span></span> | <span data-ttu-id="ae93e-142">Başlarken (/ tamamlanmış) çağırma ScriptBlock kimliği: %1</span><span class="sxs-lookup"><span data-stu-id="ae93e-142">Started (/ Completed) invocation of ScriptBlock ID: %1</span></span> </br> <span data-ttu-id="ae93e-143">Çalışma alanı kimliği: %2</span><span class="sxs-lookup"><span data-stu-id="ae93e-143">Runspace ID: %2</span></span> |

<span data-ttu-id="ae93e-144">Kimliği (olay kimliği 0x1008 ile ilişkili olabilir) betik bloğu temsil eden GUID'dir ve çalışma alanı kimliği bu betik bloğu çalıştırıldı çalışma alanı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ae93e-144">The ID is the GUID representing the script block (that can be correlated with event ID 0x1008), and the Runspace ID represents the runspace in which this script block was run.</span></span>

<span data-ttu-id="ae93e-145">Çağırma iletisinin yüzde işaretleri yapılandırılmış ETW özelliklerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ae93e-145">Percent signs in the invocation message represent structured ETW properties.</span></span> <span data-ttu-id="ae93e-146">İleti metni gerçek değerler ile değiştirilir, bunlara erişmek için daha sağlam bir şekilde Get-WinEvent cmdlet'ini iletisiyle almak ve daha sonra kullanmak için açıkken **özellikleri** ileti dizisi.</span><span class="sxs-lookup"><span data-stu-id="ae93e-146">While they are replaced with the actual values in the message text, a more robust way to access them is to retrieve the message with the Get-WinEvent cmdlet, and then use the **Properties** array of the message.</span></span>

<span data-ttu-id="ae93e-147">Bu işlev bir komut dosyası belirsizleştirirseniz ve şifrelemek için bir kötü amaçlı girişimi kaydırma nasıl yardımcı olabileceğini örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ae93e-147">Here's an example of how this functionality can help unwrap a malicious attempt to encrypt and obfuscate a script:</span></span>

```powershell
## Malware
function SuperDecrypt
{
    param($script)
    $bytes = [Convert]::FromBase64String($script)
             
    ## XOR “encryption”
    $xorKey = 0x42
    for($counter = 0; $counter -lt $bytes.Length; $counter++)
    {
        $bytes[$counter] = $bytes[$counter] -bxor $xorKey
    }
    [System.Text.Encoding]::Unicode.GetString($bytes)
}

$decrypted = SuperDecrypt "FUIwQitCNkInQm9CCkItQjFCNkJiQmVCEkI1QixCJkJlQg=="
Invoke-Expression $decrypted
```

<span data-ttu-id="ae93e-148">Bu çalıştığını aşağıdaki günlük girişlerini oluşturur:</span><span class="sxs-lookup"><span data-stu-id="ae93e-148">Running this generates the following log entries:</span></span>

```
Compiling Scriptblock text (1 of 1):
function SuperDecrypt
{
    param($script)
    $bytes = [Convert]::FromBase64String($script)
    ## XOR "encryption"
    $xorKey = 0x42
    for($counter = 0; $counter -lt $bytes.Length; $counter++)
    {
        $bytes[$counter] = $bytes[$counter] -bxor $xorKey
    }
    [System.Text.Encoding]::Unicode.GetString($bytes)

}
ScriptBlock ID: ad8ae740-1f33-42aa-8dfc-1314411877e3

Compiling Scriptblock text (1 of 1):
$decrypted = SuperDecrypt "FUIwQitCNkInQm9CCkItQjFCNkJiQmVCEkI1QixCJkJlQg=="
ScriptBlock ID: ba11c155-d34c-4004-88e3-6502ecb50f52

Compiling Scriptblock text (1 of 1):
Invoke-Expression $decrypted
ScriptBlock ID: 856c01ca-85d7-4989-b47f-e6a09ee4eeb3

Compiling Scriptblock text (1 of 1):
Write-Host 'Pwnd'
ScriptBlock ID: 5e618414-4e77-48e3-8f65-9a863f54b4c8
```

Betik bloğu uzunluğu ETW tek bir olay tutan yeteneğine nedir aşarsa, Windows PowerShell komut dosyası birden çok bölüme ayırır. <span data-ttu-id="ae93e-150">Kendi günlük iletilerini betikten rahatça için örnek kod aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ae93e-150">Here is sample code to recombine a script from its log messages:</span></span>

```powershell
$created = Get-WinEvent -FilterHashtable @{ ProviderName="Microsoft-Windows-PowerShell"; Id = 4104 } | Where-Object { $_.<...> }
$sortedScripts = $created | sort { $_.Properties[0].Value }
$mergedScript = -join ($sortedScripts | % { $_.Properties[2].Value })
```

<span data-ttu-id="ae93e-151">Sistemleriyle sınırlı bekletme arabellek (yani ETW günlükleri) sahip tüm günlük olarak, önceki kanıt gizlemek için alacaklardır olaylarla günlük bölgesini doldurmak için bu altyapı karşı bir saldırı olduğunu.</span><span class="sxs-lookup"><span data-stu-id="ae93e-151">As with all logging systems that have a limited retention buffer (i.e. ETW logs), one attack against this infrastructure is to flood the log with spurious events to hide earlier evidence.</span></span> <span data-ttu-id="ae93e-152">Bu saldırıya karşı korunmak için ayarlanan olay günlüğü koleksiyonunu çeşit olduğundan emin olun (yani, Windows Olay iletme'yi [Windows olay günlüğünü izleme ile birlikte etkilemeyi belirleme](http://www.nsa.gov/ia/_files/app/Spotting_the_Adversary_with_Windows_Event_Log_Monitoring.pdf)) olay günlükleri bilgisayarı olarak dışına taşımak için mümkün olduğunca çabuk.</span><span class="sxs-lookup"><span data-stu-id="ae93e-152">To protect yourself from this attack, ensure that you have some form of event log collection set up (i.e., Windows Event Forwarding, [Spotting the Adversary with Windows Event Log Monitoring](http://www.nsa.gov/ia/_files/app/Spotting_the_Adversary_with_Windows_Event_Log_Monitoring.pdf)) to move event logs off of the computer as soon as possible.</span></span>
