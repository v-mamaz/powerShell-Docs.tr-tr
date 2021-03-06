---
ms.date: 12/12/2018
keywords: DSC, powershell, yapılandırma, Kurulum
title: Windows PowerShell önceki sürümlerinde yerel Configuration Manager'ı yapılandırma
ms.openlocfilehash: 31ba2ecdaa5a2ff7fcfddb1791c4d00343f4b5d5
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53405783"
---
# <a name="configuring-the-local-configuration-manager-in-previous-versions-of-windows-powershell"></a>Windows PowerShell önceki sürümlerinde yerel Configuration Manager'ı yapılandırma

>Şunun için geçerlidir: Windows PowerShell 4.0

**Windows PowerShell 5.0 ve üzeri ilgili daha fazla bilgi için bkz: [yerel Configuration Manager Yapılandırma](metaConfig.md).**

Yerel Configuration Manager, Windows PowerShell Desired State Configuration (DSC) altyapısıdır.
Tüm hedef düğümler üzerinde çalışır ve bir DSC yapılandırma betiği içerdiği yapılandırma kaynaklarını çağırmak için sorumludur.
Bu konuda, yerel Configuration Manager'ın özellikleri listeler ve bir hedef düğümde yerel Configuration Manager ayarlarını nasıl değiştireceğinizi açıklar.

## <a name="local-configuration-manager-properties"></a>Yerel Configuration Manager özellikleri

Ayarlama veya alma yerel Configuration Manager özellikleri listeler.

- **AllowModuleOverwrite**: Denetimleri olup yapılandırma Hizmeti'nden yeni yapılandırma indirilen hedef düğümde bulunan eski değiştirene izin verilir. Olası değerler True ve False.
- **CertificateID**: Bir yapılandırmada geçirilen kimlik bilgileri korumak için kullanılan sertifika parmak izi. Daha fazla bilgi için [Windows PowerShell Desired State Configuration kimlik bilgilerini güvenli hale getirmek istersiniz?](https://blogs.msdn.microsoft.com/powershell/2014/01/31/want-to-secure-credentials-in-windows-powershell-desired-state-configuration/).
- **ConfigurationID**: Bir çekme hizmetinden belirli yapılandırma dosyasını almak için kullanılan bir GUID belirtir. Doğru yapılandırma dosyasının erişilebilir GUID sağlar.
- **ConfigurationMode**: Yerel Configuration Manager gerçekten yapılandırma hedef düğümlere uygulanması hakkında belirtir. Bunu yapmak için şu değerleri alabilir:
  - **ApplyOnly**: Bu seçenekle, DSC yapılandırmasını uygular ve yeni bir yapılandırma, ya da algılanan sürece başka hiçbir şey yapmaz, yeni bir yapılandırma doğrudan hedefe göndermeden tarafından yeni bir yapılandırma düğümü veya bir çekme hizmetini ve DSC bağlanıyorsanız bulur, Bu çekme hizmetiyle denetler. Hedef düğüm yapılandırmasının drifts, hiçbir işlem yapılmaz.
  - **ApplyAndMonitor**: (Varsayılan değer olan) Bu seçenek, DSC sizin tarafınızdan gönderilen hedef düğüme doğrudan veya bir çekme hizmette bulunan tüm yeni yapılandırmalar geçerlidir. Bundan sonra yapılandırma dosyasından hedef düğüm yapılandırmasını drifts, DSC günlükleri tutarsızlık bildirir. DSC günlüğe kaydetme hakkında daha fazla bilgi için bkz. [Desired State Configuration hataları tanılamak için olay günlüklerini kullanarak](http://blogs.msdn.com/b/powershell/archive/2014/01/03/using-event-logs-to-diagnose-errors-in-desired-state-configuration.aspx).
  - **ApplyAndAutoCorrect**: Bu seçenek belirtilmişse, DSC sizin tarafınızdan gönderilen hedef düğüme doğrudan veya bir çekme hizmette bulunan tüm yeni yapılandırmalar geçerlidir. Bundan sonra yapılandırma dosyasından hedef düğüm yapılandırmasını drifts, DSC günlükleri tutarsızlık bildirir ve uygun yapılandırma dosyasını getirmek için hedef düğüm yapılandırmasını ayarlayın dener.
- **ConfigurationModeFrequencyMins**: Geçerli yapılandırmasını hedef düğümde uygulamak DSC arka plan uygulamasının çalışır sıklığı (dakika cinsinden) temsil eder. Varsayılan değer 15'tir. RefreshMode ile birlikte bu değer ayarlanabilir. RefreshMode ÇEKME olarak ayarlandığında, hedef düğüm Yapılandırma hizmeti tarafından RefreshFrequencyMins ayarlanmış aralıklarla iletişim kurar ve yapılandırmasına yüklemeleri. RefreshMode değeri ne olursa olsun ConfigurationModeFrequencyMins tarafından ayarlanmış aralıklarla hedef düğüme indirilen en yeni yapılandırmayı tutarlılık altyapısı uygular. Tamsayıya RefreshFrequencyMins ayarlanmalıdır ConfigurationModeFrequencyMins katı.
- **Kimlik bilgisi**: (Get-Credential gibi ile) kimlik bilgilerini belirten yapılandırma hizmetiyle iletişim kurma gibi uzak kaynaklara erişmek için gerekli.
- **DownloadManagerCustomData**: İndirme Yöneticisi için belirli özel veri içeren bir dizi temsil eder.
- **DownloadManagerName**: Modül yükleme yöneticisi ve yapılandırmayı adını gösterir.
- **RebootNodeIfNeeded**: Belirli bir hedef düğüm yapılandırma değişiklikleri, değişikliklerin uygulanması için yeniden başlatılmasını gerektirebilir. Değerine sahip **True**, yapılandırma olmuştur hemen sonra bu özelliği düğümü yeniden başlatır tamamen uygular, daha fazla uyarı olmadan. Varsa **False** (varsayılan değer) yapılandırma tamamlandı, ancak düğümün değişikliklerin etkili olabilmesi için el ile yeniden başlatılması gerekir.
- **RefreshFrequencyMins**: Bir çekme hizmetini ayarlama olduğunda kullanılır. Geçerli yapılandırmayı indirmek için bir çekme hizmetini, yerel Configuration Manager kişiler sıklığı (dakika cinsinden) temsil eder. Bu değer ConfigurationModeFrequencyMins birlikte ayarlayabilirsiniz. RefreshMode ÇEKME olarak ayarlandığında, hedef düğüm çekme hizmetini RefreshFrequencyMins tarafından ayarlanmış aralıklarla iletişim kurar ve yapılandırmasına yüklemeleri. ConfigurationModeFrequencyMins tarafından ayarlanmış aralıklarla tutarlılık altyapısı ardından hedef düğüme indirilen en yeni yapılandırmayı uygular. RefreshFrequencyMins tamsayıya ayarlanmazsa ConfigurationModeFrequencyMins, sistemin katı, Yukarı YUVARLA. Varsayılan değer 30’dur.
- **RefreshMode**: Olası değerler **anında iletme** (varsayılan) ve **çekme**. "Gönderme temelli" yapılandırmanın herhangi bir istemci bilgisayar kullanan bir yapılandırma dosyası, her hedef düğümde yerleştirmeniz gerekir. "Pull" modunda, bir çekme hizmetini yerel başvurun ve yapılandırma dosyalarına erişmek için Configuration için ayarlamanız gerekir.

### <a name="example-of-updating-local-configuration-manager-settings"></a>Örneği yerel Configuration Manager ayarları güncelleştiriliyor

Hedef düğüm yerel Configuration Manager ayarlarını dahil ederek güncelleştirebilirsiniz bir **LocalConfigurationManager** engelleyecek bir yapılandırma betiği düğüm bloğunda içinde aşağıdaki örnekte gösterildiği gibi.

```powershell
Configuration ExampleConfig
{
    Node “Server001”
    {
        LocalConfigurationManager
        {
            ConfigurationID = "646e48cb-3082-4a12-9fd9-f71b9a562d4e"
            ConfigurationModeFrequencyMins = 45
            ConfigurationMode = "ApplyAndAutocorrect"
            RefreshMode = "Pull"
            RefreshFrequencyMins = 90
            DownloadManagerName = "WebDownloadManager"
            DownloadManagerCustomData = (@{ServerUrl="https://$PullService/psdscpullserver.svc"})
            CertificateID = "71AA68562316FE3F73536F1096B85D66289ED60E"
            Credential = $cred
            RebootNodeIfNeeded = $true
            AllowModuleOverwrite = $false
        }
# One or more resource blocks can be added here
    }
}

# The following line invokes the configuration and creates a file called Server001.meta.mof at the specified path
ExampleConfig -OutputPath "c:\users\public\dsc"
```

Önceki örnekte komut dosyasını çalıştırma belirtir ve ayarları depolayan bir MOF dosyası oluşturur.
Ayarları uygulamak için kullanabileceğiniz **Set-DscLocalConfigurationManager** cmdlet'i, aşağıdaki örnekte gösterildiği gibi.

```powershell
Set-DscLocalConfigurationManager -Path "c:\users\public\dsc"
```

> **Not**: İçin **yolu** parametresi için belirttiğiniz aynı yol belirtmelisiniz **OutputPath** yapılandırmanın önceki örnekte çağrıldığında parametre.

Geçerli yerel Configuration Manager ayarlarını görmek için kullanabileceğiniz **Get-DscLocalConfigurationManager** cmdlet'i.
Bu cmdlet'i parametresiz çağırmak, varsayılan olarak, düğüm üzerinde çalıştırdığınız yerel Configuration Manager ayarlarını alın.
Başka bir düğüme belirtmek için kullanın **CimSession** Bu cmdlet ile parametre.
