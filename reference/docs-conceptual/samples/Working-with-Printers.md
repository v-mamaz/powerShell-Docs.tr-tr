---
ms.date: 06/05/2017
keywords: PowerShell cmdlet'i
title: Yazıcılar ile Çalışma
ms.assetid: 4f29ead3-f83b-4706-ac3e-f2154ff38dc5
ms.openlocfilehash: 5638629fdf79371c8eff9ee9194b642034250fff
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53405950"
---
# <a name="working-with-printers"></a>Yazıcılar ile Çalışma

Windows PowerShell, WMI ve WSH WScript.Network COM nesneden kullanarak yazıcıları yönetmek için kullanabilirsiniz. Belirli görevleri göstermek için her iki araç bir karışımını kullanacağız.

### <a name="listing-printer-connections"></a>Yazıcı bağlantılarını listeleme

En basit yolu, bir bilgisayara yüklenen yazıcıları listelemek için WMI kullanmaktır **Win32_Printer** sınıfı:

```powershell
Get-WmiObject -Class Win32_Printer -ComputerName
```

Kullanarak yazıcıları listeleyebilirsiniz **WScript.Network** genellikle WSH betiklerde kullanılır COM nesnesi:

```powershell
(New-Object -ComObject WScript.Network).EnumPrinterConnections()
```

Bu komut, bağlantı noktası adları ve yazıcı cihaz adlarını ayırt etmenin bir yolunun etiketleri olmadan basit dize koleksiyonu döndürdüğünden, yorumlamak kolay değildir.

### <a name="adding-a-network-printer"></a>Ağ yazıcısı ekleme

Yeni bir ağ yazıcısına eklemek için **WScript.Network**:

```powershell
(New-Object -ComObject WScript.Network).AddWindowsPrinterConnection("\\Printserver01\Xerox5")
```

### <a name="setting-a-default-printer"></a>Varsayılan yazıcı belirleme

Varsayılan yazıcı ayarlamak üzere WMI kullanmak için yazıcının Bul **Win32_Printer** koleksiyonu ve ardından çağırmak **SetDefaultPrinter** yöntemi:

```powershell
(Get-WmiObject -ComputerName . -Class Win32_Printer -Filter "Name='HP LaserJet 5Si'").SetDefaultPrinter()
```

**WScript.Network** olduğundan kullanmak biraz daha basit olan bir **SetDefaultPrinter** yazıcı adı yalnızca bağımsız değişken olarak alan yöntemi:

```powershell
(New-Object -ComObject WScript.Network).SetDefaultPrinter('HP LaserJet 5Si')
```

### <a name="removing-a-printer-connection"></a>Bir yazıcı bağlantısı kaldırılıyor

Bir yazıcı bağlantısı kaldırmak için **WScript.Network RemovePrinterConnection** yöntemi:

```powershell
(New-Object -ComObject WScript.Network).RemovePrinterConnection("\\Printserver01\Xerox5")
```