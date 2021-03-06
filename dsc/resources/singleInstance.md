---
ms.date: 06/12/2017
keywords: DSC, powershell, yapılandırma, Kurulum
title: Tek örnekli DSC kaynağı yazma (en iyi uygulama)
ms.openlocfilehash: 9494964b1b13eaa082ad5cbc279b4586bb7211cc
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53405898"
---
# <a name="writing-a-single-instance-dsc-resource-best-practice"></a>Tek örnekli DSC kaynağı yazma (en iyi uygulama)

>**Not:** Bu konu, yalnızca tek bir örnek bir yapılandırma sağlayan bir DSC kaynağı tanımlamak için en iyi uygulama açıklar. Şu anda, bunu yapmak için yerleşik bir DSC özelliğini yoktur. Bu gelecekte değişebilir.

Burada bir yapılandırmada birden çok kez kullanılacak bir kaynağa izin vermenin istemediğiniz durumlar vardır. Örneğin, bir önceki uygulaması içinde [xTimeZone](https://github.com/PowerShell/xTimeZone) kaynak, bir yapılandırma çağrı kaynak birden çok kez, her kaynak blok içinde farklı bir ayar için saat dilimini ayarlamak:

```powershell
Configuration SetTimeZone
{
    Param
    (
        [String[]]$NodeName = $env:COMPUTERNAME

    )

    Import-DSCResource -ModuleName xTimeZone


    Node $NodeName
    {
         xTimeZone TimeZoneExample
         {

            TimeZone = 'Eastern Standard Time'
         }

         xTimeZone TimeZoneExample2
         {

            TimeZone = 'Pacific Standard Time'

         }

    }
}
```

DSC kaynak anahtarlarını çalışma şekli nedeniyle budur. Bir kaynak en az bir anahtarı özelliği olması gerekir. Bir kaynak örneği tüm anahtar özelliklerinin değerlerinin bileşimi benzersiz olması durumunda benzersiz olarak kabul edilir. Kendi önceki uygulamasında [xTimeZone](https://github.com/PowerShell/xTimeZone) kaynak olduğu tek özelliği--**saat dilimi**, bir anahtar olması için gerekli. Bu nedenle, yukarıdaki gibi bir yapılandırma derleyin ve uyarı olmadan çalıştırın. Her biri **xTimeZone** kaynak bloklar benzersiz olarak değerlendirilir. Bu, saat dilimi İleri ve Geri Dönüşüm düğüme sürekli olarak uygulanacak yapılandırma neden olur.

Kaynak ikinci bir özellik eklemek için bir kez güncelleştirildi yalnızca bir yapılandırma bir hedef düğüm için saat dilimini ayarlayabilirsiniz emin olmak için **IsSingleInstance**, anahtar özelliği hale geldi.
**IsSingleInstance** tek bir değer için "Evet" kullanarak sınırlı bir **ValueMap**. Kaynak için eski MOF şema şöyleydi:

```powershell
[ClassVersion("1.0.0.0"), FriendlyName("xTimeZone")]
class xTimeZone : OMI_BaseResource
{
    [Key, Description("Specifies the TimeZone.")] String TimeZone;
};
```

Kaynak için güncelleştirilmiş MOF Şeması aşağıdaki gibidir:

```powershell
[ClassVersion("1.0.0.0"), FriendlyName("xTimeZone")]
class xTimeZone : OMI_BaseResource
{
    [Key, Description("Specifies the resource is a single instance, the value must be 'Yes'"), ValueMap{"Yes"}, Values{"Yes"}] String IsSingleInstance;
    [Required, Description("Specifies the TimeZone.")] String TimeZone;
};
```

Kaynak betiği ayrıca yeni bir parametre kullanmak için güncelleştirildi. Eski kaynak betiği şu şekildedir:

```powershell
function Get-TargetResource
{
    [CmdletBinding()]
    [OutputType([Hashtable])]
    param
    (
        [parameter(Mandatory = $true)]
        [ValidateSet('Yes')]
        [String]
        $IsSingleInstance,

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $TimeZone
    )

    #Get the current TimeZone
    $CurrentTimeZone = Get-TimeZone

    $returnValue = @{
        TimeZone = $CurrentTimeZone
        IsSingleInstance = 'Yes'
    }

    #Output the target resource
    $returnValue
}


function Set-TargetResource
{
    [CmdletBinding(SupportsShouldProcess=$true)]
    param
    (
        [parameter(Mandatory = $true)]
        [ValidateSet('Yes')]
        [String]
        $IsSingleInstance,

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $TimeZone
    )

    #Output the result of Get-TargetResource function.
    $CurrentTimeZone = Get-TimeZone

    if($PSCmdlet.ShouldProcess("'$TimeZone'","Replace the System Time Zone"))
    {
        try
        {
            if($CurrentTimeZone -ne $TimeZone)
            {
                Write-Verbose -Verbose "Setting the TimeZone"
                Set-TimeZone -TimeZone $TimeZone}
            else
            {
                Write-Verbose -Verbose "TimeZone already set to $TimeZone"
            }
        }
        catch
        {
            $ErrorMsg = $_.Exception.Message
            Write-Verbose -Verbose $ErrorMsg
        }
    }
}


function Test-TargetResource
{
    [CmdletBinding()]
    [OutputType([Boolean])]
    param
    (
        [parameter(Mandatory = $true)]
        [ValidateSet('Yes')]
        [String]
        $IsSingleInstance,

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $TimeZone
    )

    #Output from Get-TargetResource
    $CurrentTimeZone = Get-TimeZone

    if($TimeZone -eq $CurrentTimeZone)
    {
        return $true
    }
    else
    {
        return $false
    }
}

Function Get-TimeZone {
    [CmdletBinding()]
    param()

    & tzutil.exe /g
}

Function Set-TimeZone {
    [CmdletBinding()]
    param(
        [Parameter(Mandatory=$true)]
        [System.String]
        $TimeZone
    )

    try
    {
        & tzutil.exe /s $TimeZone
    }
    catch
    {
        $ErrorMsg = $_.Exception.Message
        Write-Verbose $ErrorMsg
    }
}

Export-ModuleMember -Function *-TargetResource
```

Dikkat **saat dilimi** özellik olup artık bir anahtar. Şimdi, iki kez saat dilimini ayarlamak bir yapılandırma çalışırsa (iki farklı kullanarak **xTimeZone** farklı bloklar **saat dilimi** değerler), yapılandırmayı derlemek çalışılırken bir hata neden olur:

```powershell
Test-ConflictingResources : A conflict was detected between resources '[xTimeZone]TimeZoneExample (::15::10::xTimeZone)' and
'[xTimeZone]TimeZoneExample2 (::22::10::xTimeZone)' in node 'CONTOSO-CLIENT'. Resources have identical key properties but there are differences in the
following non-key properties: 'TimeZone'. Values 'Eastern Standard Time' don't match values 'Pacific Standard Time'. Please update these property
values so that they are identical in both cases.
At line:271 char:9
+         Test-ConflictingResources $keywordName $canonicalizedValue $k ...
+         ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Write-Error], InvalidOperationException
    + FullyQualifiedErrorId : ConflictingDuplicateResource,Test-ConflictingResources
Errors occurred while processing configuration 'SetTimeZone'.
At C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateConfiguration\PSDesiredStateConfiguration.psm1:3705 char:5
+     throw $ErrorRecord
+     ~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (SetTimeZone:String) [], InvalidOperationException
    + FullyQualifiedErrorId : FailToProcessConfiguration
```