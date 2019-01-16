---
ms.date: 06/12/2017
keywords: DSC, powershell, yapılandırma, Kurulum
title: Yapılandırmaları iç içe yerleştirme
ms.openlocfilehash: 54162cd72d2d1e7773e3be636bfa681329854498
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53405702"
---
# <a name="nesting-dsc-configurations"></a><span data-ttu-id="041ba-103">DSC yapılandırmaları iç içe yerleştirme</span><span class="sxs-lookup"><span data-stu-id="041ba-103">Nesting DSC configurations</span></span>

<span data-ttu-id="041ba-104">(Bileşik configuration olarak da bilinir) bir iç içe geçmiş yapılandırması içinde başka bir yapılandırma bir kaynağı kabul edildiğinde çağrılan bir yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="041ba-104">A nested configuration (also called composite configuration) is a configuration that is called within another configuration as if it were a resource.</span></span>
<span data-ttu-id="041ba-105">Aynı dosyada iki yapılandırma tanımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="041ba-105">Both configurations must be defined in the same file.</span></span>

<span data-ttu-id="041ba-106">Basit bir örneğe göz atalım:</span><span class="sxs-lookup"><span data-stu-id="041ba-106">Let's look at a simple example:</span></span>

```powershell
Configuration FileConfig
{
    param (
        [Parameter(Mandatory = $true)]
        [String] $CopyFrom,

        [Parameter(Mandatory = $true)]
        [String] $CopyTo
    )

    Import-DscResource -ModuleName PSDesiredStateConfiguration

    File FileTest
       {
           SourcePath = $CopyFrom
           DestinationPath = $CopyTo
           Ensure = 'Present'
       }

}

Configuration NestedFileConfig
{
    Node localhost
    {
        FileConfig NestedConfig
        {
            CopyFrom = 'C:\Test\TestFile.txt'
            CopyTo = 'C:\Test2'
        }
    }
}
```

<span data-ttu-id="041ba-107">Bu örnekte, `FileConfig` iki zorunlu parametre **CopyFrom** ve **CopyTo**, için değerler olarak kullanılan **SourcePath** ve  **HedefYolu** özelliklerinde `File` kaynak blok.</span><span class="sxs-lookup"><span data-stu-id="041ba-107">In this example, `FileConfig` takes two mandatory parameters,  **CopyFrom** and **CopyTo**, which are used as the values for the **SourcePath** and **DestinationPath** properties in the `File` resource block.</span></span>
<span data-ttu-id="041ba-108">`NestedConfig` Yapılandırma çağrıları `FileConfig` kaynak değilmiş gibi.</span><span class="sxs-lookup"><span data-stu-id="041ba-108">The `NestedConfig` configuration calls `FileConfig` as if it were a resource.</span></span>
<span data-ttu-id="041ba-109">Özelliklerinde `NestedConfig` kaynak blok (**CopyFrom** ve **CopyTo**) parametreleri `FileConfig` yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="041ba-109">The properties in the `NestedConfig` resource block (**CopyFrom** and **CopyTo**) are the parameters of the `FileConfig` configuration.</span></span>

## <a name="see-also"></a><span data-ttu-id="041ba-110">Ayrıca bkz:</span><span class="sxs-lookup"><span data-stu-id="041ba-110">See Also</span></span>

- [<span data-ttu-id="041ba-111">Bileşik kaynaklar bir kaynak olarak bir DSC Yapılandırması kullanılarak--</span><span class="sxs-lookup"><span data-stu-id="041ba-111">Composite resources--Using a DSC configuration as a resource</span></span>](../resources/authoringResourceComposite.md)