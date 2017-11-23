---
ms.date: 2017-06-12
author: rpsqrd
ms.topic: conceptual
keywords: "jea, powershell, güvenlik"
title: "Tam yetecek kadar yönetim genel bakış"
ms.openlocfilehash: a664a8ad44916f8112f7ef7bac145a54b83f126d
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/12/2017
---
# <a name="just-enough-administration"></a><span data-ttu-id="d0091-103">Yeterli Yönetim</span><span class="sxs-lookup"><span data-stu-id="d0091-103">Just Enough Administration</span></span>

<span data-ttu-id="d0091-104">Yalnızca yetecek kadar Yönetim (JEA) sağlayan bir güvenlik teknoloji PowerShell ile yönetilen her şey için yönetiminin ' dir.</span><span class="sxs-lookup"><span data-stu-id="d0091-104">Just Enough Administration (JEA) is a security technology that enables delegated administration for anything that can be managed with PowerShell.</span></span>
<span data-ttu-id="d0091-105">JEA ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d0091-105">With JEA, you can:</span></span>

- <span data-ttu-id="d0091-106">**Yöneticiler, makinelerde sayısını azaltın** yararlanmayı sanal hesaplar veya grup tarafından yönetilen normal kullanıcılar adına ayrıcalıklı eylemler gerçekleştirmek hizmet hesapları.</span><span class="sxs-lookup"><span data-stu-id="d0091-106">**Reduce the number of administrators on your machines** by leveraging virtual accounts or group managed service accounts that perform privileged actions on behalf of regular users.</span></span>
- <span data-ttu-id="d0091-107">**Kullanıcıların ne sınırlamak** belirterek hangi cmdlet'ler, İşlevler ve dış komutları çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0091-107">**Limit what users can do** by specifying which cmdlets, functions, and external commands they can run.</span></span>
- <span data-ttu-id="d0091-108">**Kullanıcıların ne yaptıklarını daha iyi anlamak** dökümleri ve günlükleri gösterin, tam olarak hangi kullanıcıların oturumu sırasında yürütülen bir kullanıcı komutları.</span><span class="sxs-lookup"><span data-stu-id="d0091-108">**Better understand what your users are doing** with transcripts and logs that show you exactly which commands a user executed during their session.</span></span>

<span data-ttu-id="d0091-109">**Bu neden önemlidir?**</span><span class="sxs-lookup"><span data-stu-id="d0091-109">**Why is this important?**</span></span>

<span data-ttu-id="d0091-110">Üst düzey ayrıcalıklı hesapları sunucularınızı yönetmek için kullanılan bir ciddi bir güvenlik riski.</span><span class="sxs-lookup"><span data-stu-id="d0091-110">Highly privileged accounts used to administer your servers pose a serious security risk.</span></span>
<span data-ttu-id="d0091-111">Bir saldırganın tehlikeye Bu hesaplardan birini, bunlar başlatabilir [yanal saldırıları](http://aka.ms/pth) kuruluşunuzdaki.</span><span class="sxs-lookup"><span data-stu-id="d0091-111">Should an attacker compromise one of these accounts, they could launch [lateral attacks](http://aka.ms/pth) across your organization.</span></span>
<span data-ttu-id="d0091-112">Bunlar tehlikeye her hesap bunları ve bir hizmet reddi saldırısı başlatmasını şirket gizli çalmak için bir adım daha yaklaşarak artık daha fazla hesapları ve kaynakları, bunları koyma bile erişim verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0091-112">Each account they compromise can give them access to even more accounts and resources, putting them one step closer to stealing company secrets, launching a denial-of-service attack, and more.</span></span>

<span data-ttu-id="d0091-113">Her zaman yönetici ayrıcalıkları ya da kaldırmak kolay değildir.</span><span class="sxs-lookup"><span data-stu-id="d0091-113">It is not always easy to remove administrative privileges, either.</span></span>
<span data-ttu-id="d0091-114">DNS rolü, Active Directory etki alanı denetleyicisi ile aynı makinede yüklendiği yaygın bir senaryo düşünün.</span><span class="sxs-lookup"><span data-stu-id="d0091-114">Consider the common scenario where the DNS role is installed on the same machine as your Active Directory Domain Controller.</span></span>
<span data-ttu-id="d0091-115">DNS yöneticileri DNS sunucusu ile ilgili sorunları giderme ancak üst düzey ayrıcalıklı "Etki alanı yöneticileri" güvenlik grubunun üyesi yapmak zorunda Bunu yapmak için yerel yönetici ayrıcalıkları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d0091-115">Your DNS administrators require local administrator privileges to fix issues with the DNS server, but in order to do so you have to make them members of the highly privileged "Domain Admins" security group.</span></span>
<span data-ttu-id="d0091-116">Bu yaklaşım bu makinedeki tüm kaynaklarını verimli DNS yöneticileri denetime tam etki alanı ve erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0091-116">This approach effectively gives DNS Administrators control over your whole domain and access to all resources on that machine.</span></span>

<span data-ttu-id="d0091-117">JEA yardımcı ilkesini benimsemeyi yardımcı olarak bu sorunu gidermek *en az ayrıcalık*.</span><span class="sxs-lookup"><span data-stu-id="d0091-117">JEA helps address this problem by helping you adopt the principle of *Least Privilege*.</span></span>
<span data-ttu-id="d0091-118">JEA ile bunları kendi işin yapılması için ihtiyaç duydukları tüm PowerShell komutları için erişmenizi DNS yöneticileri, ancak hiçbir şey için daha fazla yönetim uç noktası yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0091-118">With JEA, you can configure a management endpoint for DNS administrators that gives them access to all the PowerShell commands they need to get their job done, but nothing more.</span></span>
<span data-ttu-id="d0091-119">Bu zarar görmüş bir DNS önbelleği onarmak veya kasıtsız olarak bunları Active Directory hakkı vermeden DNS sunucusunu yeniden başlatın veya dosya sistemi göz atmak için uygun erişim sağlamak veya potansiyel olarak tehlikeli olabilecek komut dosyalarını çalıştır anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="d0091-119">This means you can provide the appropriate access to repair a poisoned DNS cache or restart the DNS server without unintentionally giving them rights to Active Directory, or to browse the file system, or run potentially dangerous scripts.</span></span>
<span data-ttu-id="d0091-120">JEA oturum geçici ayrıcalıklı sanal hesaplarını kullanacak şekilde yapılandırıldığında, daha iyi bir yöntem, DNS sunucusu kullanarak yöneticiler için bağlanabilir *yönetici olmayan* kimlik bilgileri ve yine genellikle gerektiren komutları çalıştırmak Yönetici ayrıcalıkları.</span><span class="sxs-lookup"><span data-stu-id="d0091-120">Better yet, when the JEA session is configured to use temporary privileged virtual accounts, your DNS administrators can connect to the server using *non-admin* credentials and still be able to run commands which typically require admin privileges.</span></span>
<span data-ttu-id="d0091-121">Bu özellik, kullanıcıların yaygın ayrıcalıklı yerel/etki alanı yönetici rollerini kaldırın ve bunun yerine dikkatle her makinede yapabileceklerinizi nedir denetlemenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0091-121">This capability enables you to remove users from widely-privileged local/domain administrator roles and instead carefully control what they are able to do on each machine.</span></span>

## <a name="get-started-with-jea"></a><span data-ttu-id="d0091-122">JEA ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d0091-122">Get Started with JEA</span></span>

<span data-ttu-id="d0091-123">JEA bugün Windows Server 2016 veya Windows 10 çalıştıran herhangi bir makinede kullanmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0091-123">You can start using JEA today on any machine running Windows Server 2016 or Windows 10.</span></span>
<span data-ttu-id="d0091-124">JEA, bir Windows Management Framework güncelleştirmesi ile daha eski işletim sistemlerinde de çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0091-124">You can also run JEA on older operating systems with a Windows Management Framework update.</span></span>
<span data-ttu-id="d0091-125">JEA kullanılacağını ve nasıl oluşturulacağını öğrenmek için gereksinimleri hakkında daha fazla bilgi için kullanma ve bir JEA uç noktası denetim, aşağıdaki konulara bakın:</span><span class="sxs-lookup"><span data-stu-id="d0091-125">To learn more about the requirements to use JEA and to learn how to create, use, and audit a JEA endpoint, check out the following topics:</span></span>

- <span data-ttu-id="d0091-126">[Önkoşullar](prerequisites.md) -JEA kullanmak için ortamınızı ayarlayın açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d0091-126">[Prerequisites](prerequisites.md) - explains how to set up your environment to use JEA.</span></span>
- <span data-ttu-id="d0091-127">[Rol özellikleri](role-capabilities.md) -bir kullanıcı bir JEA oturumda yapmak izin veriliyor belirleyen roller oluşturma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d0091-127">[Role Capabilities](role-capabilities.md) - explains how to create roles which determine what a user is allowed to do in a JEA session.</span></span>
- <span data-ttu-id="d0091-128">[Oturum yapılandırmaları](session-configurations.md) -Kullanıcıları rollerine eşlemek ve JEA kimliği JEA uç noktalarını yapılandırma açıklanmaktadır</span><span class="sxs-lookup"><span data-stu-id="d0091-128">[Session Configurations](session-configurations.md) - explains how to configure JEA endpoints that map users to roles and set the JEA identity</span></span>
- <span data-ttu-id="d0091-129">[JEA kaydetme](register-jea.md) - JEA uç noktası oluşturun ve bağlanmak kullanıcılar için kullanılabilir yapın.</span><span class="sxs-lookup"><span data-stu-id="d0091-129">[Registering JEA](register-jea.md) - create a JEA endpoint and make it available for users to connect to.</span></span>
- <span data-ttu-id="d0091-130">[JEA kullanarak](using-jea.md) -JEA kullanabileceğiniz çeşitli yollarını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d0091-130">[Using JEA](using-jea.md) - learn the various ways you can use JEA.</span></span>
- <span data-ttu-id="d0091-131">[Güvenlik konuları](security-considerations.md) -en iyi güvenlik uygulamaları ve JEA yapılandırma seçenekleri etkilerini gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="d0091-131">[Security Considerations](security-considerations.md) - review security best practices and implications of JEA configuration options.</span></span>
- <span data-ttu-id="d0091-132">[Denetim ve rapor üzerinde JEA](audit-and-report.md) -denetim ve JEA uç noktalarda rapor hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="d0091-132">[Audit and Report on JEA](audit-and-report.md) - learn how to audit and report on JEA endpoints.</span></span>

## <a name="samples-and-dsc-resource"></a><span data-ttu-id="d0091-133">Örnekler ve DSC kaynağı</span><span class="sxs-lookup"><span data-stu-id="d0091-133">Samples and DSC resource</span></span>

<span data-ttu-id="d0091-134">Örnek JEA yapılandırmaları ve JEA DSC kaynağı bulunabilir [JEA GitHub deposunu](https://github.com/PowerShell/JEA).</span><span class="sxs-lookup"><span data-stu-id="d0091-134">Sample JEA configurations and the JEA DSC resource can be found in the [JEA GitHub repository](https://github.com/PowerShell/JEA).</span></span>
