---
ms.date: 06/12/2017
keywords: DSC, powershell, yapılandırma, Kurulum
title: DSC kaynaklarında hata ayıklama
ms.openlocfilehash: 9b2e7dd9b42332b869c4d7fabb21bd4b5a6b8800
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53405760"
---
# <a name="debugging-dsc-resources"></a>DSC kaynaklarında hata ayıklama

> Şunun için geçerlidir: Windows PowerShell 5.0

PowerShell 5. 0'da, istenen durum yapılandırma (DSC kaynağı bir yapılandırma uygulanmakta olduğu gibi hata ayıklama olanak tanıyan DSC içinde) yeni bir özellik sunulmuştur.

## <a name="enabling-dsc-debugging"></a>DSC hata ayıklamayı etkinleştirme
Bir kaynak ayıklayabilirsiniz önce çağrı yaparak hata ayıklamayı etkinleştirmek sahip [etkinleştir DscDebug](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug) cmdlet'i.
Bu cmdlet zorunlu bir parametre alır **BreakAll**.

Hata ayıklama yapılan bir çağrının sonucu bakarak etkinleştirildiğini doğrulayın [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager).

Aşağıdaki PowerShell çıktısı, hata ayıklamayı etkinleştirme sonucunu göstermektedir:


```powershell
PS C:\DebugTest> $LCM = Get-DscLocalConfigurationManager

PS C:\DebugTest> $LCM.DebugMode
NONE

PS C:\DebugTest> Enable-DscDebug -BreakAll

PS C:\DebugTest> $LCM = Get-DscLocalConfigurationManager

PS C:\DebugTest> $LCM.DebugMode
ForceModuleImport
ResourceScriptBreakAll

PS C:\DebugTest>
```


## <a name="starting-a-configuration-with-debug-enabled"></a>Bir yapılandırma ile etkin hata ayıklama başlatılıyor
DSC kaynak hata ayıklamak için bu kaynağa çağıran bir yapılandırma başlatın.
Bu örnekte, çağıran basit bir yapılandırma sırasında atacağız **WindowsFeature** kaynağı "WindowsPowerShellWebAccess" özelliği yüklü olduğundan emin olun:

```powershell
Configuration PSWebAccess
    {
    Import-DscResource -ModuleName 'PsDesiredStateConfiguration'
    Node localhost
        {
        WindowsFeature PSWA
            {
            Name = 'WindowsPowerShellWebAccess'
            Ensure = 'Present'
            }
        }
    }
PSWebAccess
```
Yapılandırma derledikten sonra Başlat, çağırarak [Başlat-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration).
Yerel Configuration Manager (LCM) yapılandırma ilk kaynağına çağırdığında yapılandırma durdurur.
Kullanırsanız `-Verbose` ve `-Wait` parametreleri, hata ayıklamayı başlatmak için girmeniz gereken satırları çıktıyı görüntüler.

```powershell
Start-DscConfiguration .\PSWebAccess -Wait -Verbose
VERBOSE: Perform operation 'Invoke CimMethod' with following parameters, ''methodName' = SendConfigurationApply,'className' = MSFT_DSCLocalConfiguration
Manager,'namespaceName' = root/Microsoft/Windows/DesiredStateConfiguration'.
VERBOSE: An LCM method call arrived from computer TEST-SRV with user sid S-1-5-21-2127521184-1604012920-1887927527-108583.
VERBOSE: An LCM method call arrived from computer TEST-SRV with user sid S-1-5-21-2127521184-1604012920-1887927527-108583.
VERBOSE: [TEST-SRV]: LCM:  [ Start  Set      ]
WARNING: [TEST-SRV]:                            [DSCEngine] Warning LCM is in Debug 'ResourceScriptBreakAll' mode.  Resource script processing will
be stopped to wait for PowerShell script debugger to attach.
VERBOSE: [TEST-SRV]:                            [DSCEngine] Importing the module C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateCo
nfiguration\DscResources\MSFT_RoleResource\MSFT_RoleResource.psm1 in force mode.
VERBOSE: [TEST-SRV]: LCM:  [ Start  Resource ]  [[WindowsFeature]PSWA]
VERBOSE: [TEST-SRV]: LCM:  [ Start  Test     ]  [[WindowsFeature]PSWA]
VERBOSE: [TEST-SRV]:                            [[WindowsFeature]PSWA] Importing the module MSFT_RoleResource in force mode.
WARNING: [TEST-SRV]:                            [[WindowsFeature]PSWA] Resource is waiting for PowerShell script debugger to attach.
Use the following commands to begin debugging this resource script:
Enter-PSSession -ComputerName TEST-SRV -Credential <credentials>
Enter-PSHostProcess -Id 9000 -AppDomainName DscPsPluginWkr_AppDomain
Debug-Runspace -Id 9
```
Bu noktada, LCM kaynak adı ve ilk kesme noktasına gelen.
Son üç satır çıktıda işleme ve kaynak betiği hata ayıklamayı Başlat gösterilmektedir.

## <a name="debugging-the-resource-script"></a>Kaynak betiği hata ayıklama

PowerShell ISE yeni bir örneğini başlatın.
Konsol bölmesinde, son üç satır çıktısı girin `Start-DscConfiguration` değiştirerek komutları çıktı `<credentials>` geçerli kullanıcı kimlik bilgileriyle.
Şimdi şuna benzer şekilde bir uyarı görmeniz gerekir:

```powershell
[TEST-SRV]: [DBG]: [Process:9000]: [RemoteHost]: PS C:\DebugTest>>
```

Kaynak betiği betik bölmesinde açılır ve hata ayıklayıcı durduruldu ilk satırında **Test TargetResource** işlevi ( **Test()** sınıf tabanlı bir kaynak yöntemi).
Hata ayıklama komutları ISE'de kaynak betiği adımlamak için artık, değişken değerleri arayın, çağrı yığınını görüntüleme ve benzeri. Kaynak betiği (veya sınıf) her satırda bir kesme noktası olarak ayarlandığını unutmayın.

## <a name="disabling-dsc-debugging"></a>DSC hata ayıklama devre dışı bırakma

Arama sonra [etkinleştir DscDebug](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug), tüm çağrıları [Başlat-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) hata ayıklayıcıya bozucu yapılandırmasında sonuçlanır. Yapılandırmaları normal olarak çalışmasına izin vermek için çağrı yaparak hata ayıklamayı devre dışı bırakmalısınız [devre dışı bırak DscDebug](/powershell/module/PSDesiredStateConfiguration/Disable-DscDebug) cmdlet'i.

>**Not:** Yeniden başlatma LCM hata ayıklama durumunu değiştirmez. Hata ayıklama etkinleştirilirse bir yapılandırması başlatılıyor yine de hata ayıklayıcıya bir yeniden başlatma sonrası çalışmamasına neden olur.

## <a name="see-also"></a>Ayrıca bkz:

- [MOF ile özel bir DSC kaynağı yazma](../resources/authoringResourceMOF.md)
- [PowerShell sınıfları ile özel bir DSC kaynağı yazma](../resources/authoringResourceClass.md)
