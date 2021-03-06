---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: da603fda4499129b415477f627842fe10abefe06
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/16/2018
ms.locfileid: "34188505"
---
# <a name="just-enough-administration-jea"></a>Yeterli Yönetim (JEA)
Yalnızca yeterli yönetim WMF 5.0 ile rol tabanlı yönetim PowerShell uzaktan iletişimi aracılığıyla sağlayan yeni bir özelliktir.  Varolan kısıtlanmış uç altyapısı belirli komutları, komut dosyaları ve yürütülebilir bir yönetici olarak çalıştırmak yönetici olmayanlar sağlayarak genişletir.  Bu, ortamınızda tam Yöneticiler sayısını azaltın ve güvenliğinizi artırmak sağlar.  JEA, her şeyi PowerShell aracılığıyla yönetmek için çalışır; PowerShell ile bir şey yönetebilir, JEA, böylece daha güvenli bir şekilde yapmanıza yardımcı olabilir.  Yalnızca yeterli yönetim ayrıntılı bir bakış için kullanıma [Kılavuzu deneyimi](http://aka.ms/JEA).

Eski kısıtlanmış uç noktaları JEA güçlü ve kolayca yapılandırılabilir.  JEA içinde kullanıcı yeteneklerini granularly, hangi parametre kümeleri ve değerleri için belirli bir komut sağlanan kısıtlama aşağıya doğru denetlenebilir. Kullanıcının Eylemler yönetici eylemleri gerçekleştirmek için haklara sahip tek seferlik bir sanal hesabı bağlamında çalışır.  Kullanıcı tarafından çağrılan komutları güvenlik denetimleri için kaydedilebilir.

JEA, kısıtlanmış uç noktalar özel olarak yapılandırılmış oluşturmanıza olanak sağlayarak çalışır.  Bu uç noktaları birkaç önemli özelliklere sahiptir:

1. "Farklı bir ayrıcalıklı sanal yalnızca bu uzak oturum sürekliliği için mevcut hesap Çalıştır" kullanıcılara bağlanan kullanıcıları.  Varsayılan olarak, bu sanal hesap bir etki alanı yöneticileri etki alanı denetleyicilerinde yanı sıra yerleşik Yöneticiler grubunun üyesi olan (Not: Bu izinleri yapılandırılabilir). Bir kullanıcı olarak bağlanma ve farklı, ayrıcalıklı bir kullanıcı olarak çalışıyor, ayrıcalıklı olmayan kullanıcıların sistemleriniz üzerinde yönetici hakları vermeden belirli yönetim görevlerini gerçekleştirmek imkan sağlar.
2. Uç nokta kilitlenmiştir.  Bu, Hayır dil modda PowerShell çalışır anlamına gelir.  Yalnızca belirli komutları, komut dosyaları ve yürütülebilir dosyalar, kullanıcı tarafından görülebilir.
3. Bağlanan farklı kullanıcıların farklı bir grup üyeliğine dayalı özellikler kümesi sunulur.  Farklı roller aynı uç noktada farklı özellikler sağlayabilir.
