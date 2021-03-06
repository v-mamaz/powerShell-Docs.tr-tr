---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: d7aec1a2ba8964e877ddd7406609fe135b1eb462
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34219751"
---
# <a name="call-base-class-method"></a>Temel Sınıf Yöntemini Çağırma

Alt sınıfların varolan yöntemleri geçersiz kılabilirsiniz. Bunu yapmak için aynı ad ve imza kullanarak yöntemleri bildirin:

```powershell
class baseClass
{
    [int]foo() {return 100500}
}

class childClass1 : baseClass
{
    [int]foo() {return 200600}
}

[childClass1]::new().foo() # return 200600
```

Taban sınıf yöntemlerini geçersiz kılınan uygulamaları çağırmak için temel sınıf cast ([baseClass] $Bu) çağırma üzerinde:

```powershell
class childClass2 : baseClass
{
    [int]foo()
    {
        return 3 * ([baseClass]$this).foo()
    }
}

[childClass2]::new().foo() # return 301500
```

Tüm PowerShell sanal yöntemleridir. Bir geçersiz kılma için yaptığınız gibi aynı sözdizimini kullanarak bir alt kümesi sanal olmayan .NET yöntemlerinde gizleyebilirsiniz: yalnızca aynı ad ve imza yöntemleriyle bildirin.

```powershell
class MyIntList : system.collections.generic.list[int]
{
    # Add is final in system.collections.generic.list
    [void] Add([int]$arg)
    {
        ([system.collections.generic.list[int]]$this).Add($arg * 2)
    }
}

$list = [MyIntList]::new()
$list.Add(100)
$list[0] # return 200
```
