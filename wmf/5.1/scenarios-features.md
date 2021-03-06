---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,setup
title: Yeni senaryolar ve WMF 5.1 Özellikleri
ms.openlocfilehash: b00069aad7422f86d1462a62a6c4bc8a91e46705
ms.sourcegitcommit: 50b66cada6943784b8d3c103cebc3c1e3e286a16
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090372"
---
# <a name="new-scenarios-and-features-in-wmf-51"></a>Yeni senaryolar ve WMF 5.1 Özellikleri

> Not: Bu bilgiler geçicidir ve değiştirilebilir.

## <a name="powershell-editions"></a>PowerShell Sürümleri

Sürüm 5.1’den başlayarak, PowerShell çeşitli özellik kümelerini ve platform uyumluluğunu belirten farklı sürümler halinde sağlanır.

- **Masaüstü Sürümü:** .NET Framework üzerine yapılandırılmıştır ve Windows’un Sunucu Çekirdeği ve Windows Masaüstü gibi tam boyutlu sürümlerinde çalışan PowerShell sürümlerinin hedeflendiği betikler ve modüllerle uyumluluk sağlar.
- **Çekirdek Sürümü:** .NET Core üzerine yapılandırılmıştır ve Windows’un Nano Sunucu ve Windows IoT gibi azaltılmış boyutlu sürümlerinde çalışan PowerShell sürümlerinin hedeflendiği betikler ve modüllerle uyumluluk sağlar.

**PowerShell sürümleri kullanma hakkında daha fazla bilgi edinin**

- [PowerShell $PSVersionTable kullanarak çalışan sürümünü belirleme](/powershell/module/microsoft.powershell.core/about/about_automatic_variables)
- [Get-Module sonuçları PSEdition parametresini kullanarak CompatiblePSEditions göre filtrele](/powershell/module/microsoft.powershell.core/get-module)
- [Betik yürütme uyumlu bir PowerShell sürümünde çalıştırmadığınız sürece engelle](/powershell/gallery/concepts/script-psedition-support)
- [Bir modülün uyumluluk belirli PowerShell sürümleri için bildirme](/powershell/gallery/concepts/module-psedition-support)

## <a name="catalog-cmdlets"></a>Katalog cmdlet'leri

İçinde iki yeni cmdlet'ler eklenmiştir [Microsoft.PowerShell.Security](/powershell/module/microsoft.powershell.security) modülü; bunlar oluşturmak ve Windows Katalog dosyaları doğrulayın.

### <a name="new-filecatalog"></a>FileCatalog yeni
--------------------------------

FileCatalog yeni dosya ve klasörleri kümesi için bir Windows katalog dosyası oluşturur.
Bu katalog dosyası belirtilen yolda tüm dosyalar için karmaları içerir.
Kullanıcılar bu klasörleri temsil eden karşılık gelen katalog dosyası ile birlikte klasörler kümesi dağıtabilirsiniz.
Bu bilgiler, tüm klasörler için katalog oluşturma işleminden yapılan değişiklikler olup olmadığını doğrulamak yararlıdır.

```powershell
New-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-CatalogVersion <int>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

Katalog sürüm 1 ve 2 desteklenir.
Sürüm 1 dosya karmaları oluşturmak için SHA1 karma algoritmasını kullanır; sürüm 2 SHA256 kullanır.
Katalog sürüm 2 desteklenmiyor *Windows Server 2008 R2* veya *Windows 7*.
Katalog sürüm 2 kullanması gereken *Windows 8*, *Windows Server 2012*ve sonraki işletim sistemleri.

![](../images/NewFileCatalog.jpg)

Bu, katalog dosyası oluşturur.

![](../images/CatalogFile1.jpg)

![](../images/CatalogFile2.jpg)

Katalog dosyası (yukarıdaki örnekte, Pester.cat) bütünlüğünü doğrulamak için kullanarak oturum [kümesi AuthenticodeSignature](/powershell/module/Microsoft.PowerShell.Security/Set-AuthenticodeSignature) cmdlet'i.

### <a name="test-filecatalog"></a>Test-FileCatalog
--------------------------------

Test FileCatalog klasörleri kümesini temsil eden katalog doğrular.

```powershell
Test-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-Detailed] [-FilesToSkip <string[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

![](../images/TestFileCatalog.jpg)

Bu cmdlet tüm dosyaları karmaları karşılaştırır ve bunların göreli yollar bulunan *katalog* bulunanlarla *disk*.
Herhangi dosya karmaları ve yolları arasında uyuşmazlık algılarsa, durum olarak döndürür *ValidationFailed*.
Kullanıcılar, tüm bu bilgileri kullanarak alabilir *-ayrıntılı* parametresi.
Ayrıca Kataloğu'nda imzalama durumunu görüntüler *imza* arama için eşdeğer olan özelliği [Get-AuthenticodeSignature](/powershell/module/Microsoft.PowerShell.Security/Get-AuthenticodeSignature) katalog dosyası cmdlet'ini.
Kullanıcılar ayrıca atlayabilirsiniz herhangi bir dosya doğrulama sırasında kullanarak *- FilesToSkip* parametresi.

## <a name="module-analysis-cache"></a>Modül analiz önbelleği

WMF 5.1 ile başlayarak, PowerShell bunu aktarır komutları gibi bir modülüyle ilgili verileri önbelleğe kullanılan dosya üzerinde denetim sağlar.

Varsayılan olarak, bu önbellek dosyasında depolanan `${env:LOCALAPPDATA}\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.
Önbellek başlangıçta komutu için aranırken genelde okur ve bir modülü içeri aktarıldıktan sonra arka plan iş parçacığında süre yazılır.

Önbelleğinin varsayılan konumu değiştirmek için ayarlayın `$env:PSModuleAnalysisCachePath` PowerShell başlatmadan önce ortam değişkeni.
Bu ortam değişkenini yapılan değişiklikler yalnızca alt işlemleri etkiler.
Değeri PowerShell dosya oluşturma ve yazma izni olan bir tam yol (içeren dosya adı) adı.
Dosya önbelleği devre dışı bırakmak için geçersiz bir konum için bu değeri örneğin ayarlayın:

```powershell
$env:PSModuleAnalysisCachePath = 'nul'
```

Bu, geçersiz bir aygıta yolunu ayarlar.
PowerShell yolunu yazılamıyor, herhangi bir hata döndürdü, ancak hata bir izleyici kullanarak raporlama görebilirsiniz:

```powershell
Trace-Command -PSHost -Name Modules -Expression { Import-Module Microsoft.PowerShell.Management -Force }
```

Önbelleği yazarken, PowerShell düşükse bir önbellek önlemek için artık mevcut modülleri için kontrol eder.
Bazen bu denetimler, bu durumda, bunları ayarlayarak kapatabilirsiniz, istenmez:

```powershell
$env:PSDisableModuleAnalysisCacheCleanup = 1
```

Bu ortam değişkenini ayarı hemen geçerli işlemde etkinleşir.

## <a name="specifying-module-version"></a>Modül sürümü belirtme

WMF 5.1 içinde `using module` diğer ilgili modülü kurulumlarını PowerShell'de aynı şekilde davranır.
Daha önce belirli modülü sürüm belirtmek için hiçbir yolu yoktu; Mevcut birden çok sürüm varsa, bu hatayla sonuçlandı.

WMF 5.1:

- Kullanabileceğiniz [ModuleSpecification Oluşturucusu (karma)](/dotnet/api/microsoft.powershell.commands.modulespecification.-ctor?view=powershellsdk-1.1.0#Microsoft_PowerShell_Commands_ModuleSpecification__ctor_System_Collections_Hashtable_).
Bu karma tablosu ile aynı biçimi sahip `Get-Module -FullyQualifiedName`.

**Örnek:** `using module @{ModuleName = 'PSReadLine'; RequiredVersion = '1.1'}`

- Birden çok modül sürümü varsa, PowerShell kullanan **aynı çözümleme mantığı** olarak `Import-Module` ve bir hata oluştu--aynı davranışı dönmez `Import-Module` ve `Import-DscResource`.

## <a name="improvements-to-pester"></a>Pester geliştirmeleri

WMF 5.1, PowerShell ile birlikte gelen Pester sürümü 3.3.5 tamamlama eklenmesi ile 3.4.0 güncelleştirildi https://github.com/pester/Pester/pull/484/commits/3854ae8a1f215b39697ac6c2607baf42257b102e, hangi etkinleştirir daha iyi davranış Nano Server üzerinde Pester için.

ChangeLog.md dosyasını inceleyerek sürümleri için 3.3.5 3.4.0 değişiklikleri gözden geçirebilirsiniz: https://github.com/pester/Pester/blob/master/CHANGELOG.md
