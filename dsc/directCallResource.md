---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC, powershell, yapılandırma, Kur"
title: "DSC kaynağı yöntemleri doğrudan çağırma"
ms.openlocfilehash: ab00e66d526eda244500a41e450c56b0151274ee
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/12/2017
---
# <a name="calling-dsc-resource-methods-directly"></a><span data-ttu-id="56514-103">DSC kaynağı yöntemleri doğrudan çağırma</span><span class="sxs-lookup"><span data-stu-id="56514-103">Calling DSC resource methods directly</span></span>

><span data-ttu-id="56514-104">İçin geçerlidir: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="56514-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="56514-105">Kullanabileceğiniz [Invoke-DscResource](https://technet.microsoft.com/en-us/library/mt517869.aspx) işlevleri veya DSC kaynağı yöntemleri doğrudan çağırmak için cmdlet ( **Get-TargetResource**, **kümesi TargetResource**ve  **Test-TargetResource** MOF tabanlı bir kaynak işlevlerini veya **almak**, **ayarlamak**, ve **Test** sınıf tabanlı bir kaynak yöntemlerinin).</span><span class="sxs-lookup"><span data-stu-id="56514-105">You can use the [Invoke-DscResource](https://technet.microsoft.com/en-us/library/mt517869.aspx) cmdlet to directly call the functions or methods of a DSC resource (The **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource** functions of a MOF-based resource, or the **Get**, **Set**, and **Test** methods of a class-based resource).</span></span> <span data-ttu-id="56514-106">Bu DSC kaynakları kullanmak istediğiniz üçüncü taraflar tarafından ya da yararlı bir araç olarak kaynakları geliştirirken kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="56514-106">This can be used by third-parties that want to use DSC resources, or as a helpful tool while developing resources.</span></span> 

<span data-ttu-id="56514-107">Bu cmdlet genellikle meta yapılandırmasını özelliği ile birlikte kullanılan `refreshMode = 'Disabled'`, ancak bu ne olursa olsun kullanılabilir **refreshMode** ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="56514-107">This cmdlet is typically used in combination with a metaconfiguration property `refreshMode = 'Disabled'`, but it can be used no matter what **refreshMode** is set to.</span></span>

<span data-ttu-id="56514-108">Çağrılırken **Invoke-DscResource** cmdlet, belirttiğiniz hangi yöntemi veya kullanarak çağrılacak işlevi **yöntemi** parametresi.</span><span class="sxs-lookup"><span data-stu-id="56514-108">When calling the **Invoke-DscResource** cmdlet, you specify which method or function to call by using the **Method** parameter.</span></span> <span data-ttu-id="56514-109">Bir karma tablosu değeri olarak geçirerek kaynak özelliklerini belirtin **özelliği** parametresi.</span><span class="sxs-lookup"><span data-stu-id="56514-109">You specify the properties of the resource by passing a hashtable as the value of the **Property** parameter.</span></span>

<span data-ttu-id="56514-110">Doğrudan kaynak yöntemleri çağırma örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="56514-110">The following are examples of directly calling resource methods:</span></span>

## <a name="ensure-a-file-is-present"></a><span data-ttu-id="56514-111">Bir dosya bulunduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="56514-111">Ensure a file is present</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Set -Property @{
                            DestinationPath = "$env:SystemDrive\\DirectAccess.txt";
                            Contents = 'This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="test-that-a-file-is-present"></a><span data-ttu-id="56514-112">Bir dosya var olup olmadığını test</span><span class="sxs-lookup"><span data-stu-id="56514-112">Test that a file is present</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Test -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="get-the-contents-of-file"></a><span data-ttu-id="56514-113">Dosyanın içeriğini alma</span><span class="sxs-lookup"><span data-stu-id="56514-113">Get the contents of file</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Get -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result.ItemValue | fl
```

><span data-ttu-id="56514-114">**Not:** doğrudan bileşik kaynak yöntemleri çağırma desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="56514-114">**Note:** Directly calling composite resource methods is not supported.</span></span> <span data-ttu-id="56514-115">Bunun yerine, bileşik kaynak olun temel alınan kaynak yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="56514-115">Instead, call the methods of the underlying resources that make up the composite resource.</span></span>

## <a name="see-also"></a><span data-ttu-id="56514-116">Ayrıca bkz:</span><span class="sxs-lookup"><span data-stu-id="56514-116">See Also</span></span>
- [<span data-ttu-id="56514-117">Özel bir DSC kaynağı MOF ile yazma</span><span class="sxs-lookup"><span data-stu-id="56514-117">Writing a custom DSC resource with MOF</span></span>](authoringResourceMOF.md) 
- [<span data-ttu-id="56514-118">PowerShell sınıfları içeren özel bir DSC kaynağı yazma</span><span class="sxs-lookup"><span data-stu-id="56514-118">Writing a custom DSC resource with PowerShell classes</span></span>](authoringResourceClass.md)
- [<span data-ttu-id="56514-119">DSC kaynakları hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="56514-119">Debugging DSC resources</span></span>](debugResource.md)
