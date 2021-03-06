---
ms.date: 06/12/2017
keywords: jea, powershell, güvenlik
title: Tam yetecek kadar yönetim genel bakış
ms.openlocfilehash: 3dae8b31d4d13ff9033803035c870c02fc7c38ca
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34222097"
---
# <a name="just-enough-administration"></a>Yeterli Yönetim

Yalnızca yetecek kadar Yönetim (JEA) sağlayan bir güvenlik teknoloji PowerShell ile yönetilen her şey için yönetiminin ' dir.
JEA ile şunları yapabilirsiniz:

- **Yöneticiler, makinelerde sayısını azaltın** yararlanmayı sanal hesaplar veya grup tarafından yönetilen normal kullanıcılar adına ayrıcalıklı eylemler gerçekleştirmek hizmet hesapları.
- **Kullanıcıların ne sınırlamak** belirterek hangi cmdlet'ler, İşlevler ve dış komutları çalıştırabilirsiniz.
- **Kullanıcıların ne yaptıklarını daha iyi anlamak** dökümleri ve günlükleri gösterin, tam olarak hangi kullanıcıların oturumu sırasında yürütülen bir kullanıcı komutları.

**Bu neden önemlidir?**

Üst düzey ayrıcalıklı hesapları sunucularınızı yönetmek için kullanılan bir ciddi bir güvenlik riski.
Bir saldırganın tehlikeye Bu hesaplardan birini, bunlar başlatabilir [yanal saldırıları](http://aka.ms/pth) kuruluşunuzdaki.
Bunlar tehlikeye her hesap bunları ve bir hizmet reddi saldırısı başlatmasını şirket gizli çalmak için bir adım daha yaklaşarak artık daha fazla hesapları ve kaynakları, bunları koyma bile erişim verebilirsiniz.

Her zaman yönetici ayrıcalıkları ya da kaldırmak kolay değildir.
DNS rolü, Active Directory etki alanı denetleyicisi ile aynı makinede yüklendiği yaygın bir senaryo düşünün.
DNS yöneticileri DNS sunucusu ile ilgili sorunları giderme ancak üst düzey ayrıcalıklı "Etki alanı yöneticileri" güvenlik grubunun üyesi yapmak zorunda Bunu yapmak için yerel yönetici ayrıcalıkları gerektirir.
Bu yaklaşım bu makinedeki tüm kaynaklarını verimli DNS yöneticileri denetime tam etki alanı ve erişim sağlar.

JEA yardımcı ilkesini benimsemeyi yardımcı olarak bu sorunu gidermek *en az ayrıcalık*.
JEA ile bunları kendi işin yapılması için ihtiyaç duydukları tüm PowerShell komutları için erişmenizi DNS yöneticileri, ancak hiçbir şey için daha fazla yönetim uç noktası yapılandırabilirsiniz.
Bu zarar görmüş bir DNS önbelleği onarmak veya kasıtsız olarak bunları Active Directory hakkı vermeden DNS sunucusunu yeniden başlatın veya dosya sistemi göz atmak için uygun erişim sağlamak veya potansiyel olarak tehlikeli olabilecek komut dosyalarını çalıştır anlamına gelir.
JEA oturum geçici ayrıcalıklı sanal hesaplarını kullanacak şekilde yapılandırıldığında, daha iyi bir yöntem, DNS sunucusu kullanarak yöneticiler için bağlanabilir *yönetici olmayan* kimlik bilgileri ve yine genellikle gerektiren komutları çalıştırmak Yönetici ayrıcalıkları.
Bu özellik, kullanıcıların yaygın ayrıcalıklı yerel/etki alanı yönetici rollerini kaldırın ve bunun yerine dikkatle her makinede yapabileceklerinizi nedir denetlemenizi sağlar.

## <a name="get-started-with-jea"></a>JEA ile çalışmaya başlama

JEA bugün Windows Server 2016 veya Windows 10 çalıştıran herhangi bir makinede kullanmaya başlayabilirsiniz.
JEA, bir Windows Management Framework güncelleştirmesi ile daha eski işletim sistemlerinde de çalıştırabilirsiniz.
JEA kullanılacağını ve nasıl oluşturulacağını öğrenmek için gereksinimleri hakkında daha fazla bilgi için kullanma ve bir JEA uç noktası denetim, aşağıdaki konulara bakın:

- [Önkoşullar](prerequisites.md) -JEA kullanmak için ortamınızı ayarlayın açıklanmaktadır.
- [Rol özellikleri](role-capabilities.md) -bir kullanıcı bir JEA oturumda yapmak izin veriliyor belirleyen roller oluşturma açıklanmaktadır.
- [Oturum yapılandırmaları](session-configurations.md) -Kullanıcıları rollerine eşlemek ve JEA kimliği JEA uç noktalarını yapılandırma açıklanmaktadır
- [JEA kaydetme](register-jea.md) - JEA uç noktası oluşturun ve bağlanmak kullanıcılar için kullanılabilir yapın.
- [JEA kullanarak](using-jea.md) -JEA kullanabileceğiniz çeşitli yollarını öğrenin.
- [Güvenlik konuları](security-considerations.md) -en iyi güvenlik uygulamaları ve JEA yapılandırma seçenekleri etkilerini gözden geçirin.
- [Denetim ve rapor üzerinde JEA](audit-and-report.md) -denetim ve JEA uç noktalarda rapor hakkında bilgi edinin.

## <a name="samples-and-dsc-resource"></a>Örnekler ve DSC kaynağı

Örnek JEA yapılandırmaları ve JEA DSC kaynağı bulunabilir [JEA GitHub deposunu](https://github.com/PowerShell/JEA).