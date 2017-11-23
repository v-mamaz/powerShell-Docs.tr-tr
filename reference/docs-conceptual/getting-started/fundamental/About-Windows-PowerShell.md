---
ms.date: 2017-06-05
keywords: PowerShell cmdlet'i
title: "Windows PowerShell hakkında"
ms.assetid: 979654ae-7994-47f8-be43-d79e7a140143
ms.openlocfilehash: 5e6d1bb4d8915ba3c83ba0020b959e444b5211cd
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="about-windows-powershell"></a><span data-ttu-id="7dcc3-103">Windows PowerShell hakkında</span><span class="sxs-lookup"><span data-stu-id="7dcc3-103">About Windows PowerShell</span></span>
<span data-ttu-id="7dcc3-104">Windows PowerShell komut satırı ve komut dosyası ortamı artırmanın uzun süredir bilinen sorunlar ortadan kaldırılır ve yeni özellikler ekleyerek iyileştirmek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-104">Windows PowerShell is designed to improve the command-line and scripting environment by eliminating long-standing problems and adding new features.</span></span>

## <a name="discoverability"></a><span data-ttu-id="7dcc3-105">Bulunabilirliği</span><span class="sxs-lookup"><span data-stu-id="7dcc3-105">Discoverability</span></span>
<span data-ttu-id="7dcc3-106">Windows PowerShell özelliklerini Bul kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-106">Windows PowerShell makes it easy to discover its features.</span></span> <span data-ttu-id="7dcc3-107">Örneğin, görüntüle ve Değiştir Windows Hizmetleri cmdlet'lerinin listesini bulmak için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="7dcc3-107">For example, to find a list of cmdlets that view and change Windows services, type:</span></span>

```
Get-Command *-Service
```

<span data-ttu-id="7dcc3-108">Hangi cmdlet'i bir görevi gerçekleştirir öğrendiğinizde Get-Help cmdlet'ini kullanarak cmdlet hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-108">After discovering which cmdlet accomplishes a task, you can learn more about the cmdlet by using the Get-Help cmdlet.</span></span> <span data-ttu-id="7dcc3-109">Örneğin, Get-Service cmdlet'i hakkında Yardım görüntülemek için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="7dcc3-109">For example, to display help about the Get-Service cmdlet, type:</span></span>

```
Get-Help Get-Service
```
<span data-ttu-id="7dcc3-110">Çoğu cmdlet'leri yönetilebilir ve görüntülemek için metne çizilir nesneleri yayma.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-110">Most cmdlets emit objects which can be manipulated and then rendered into text for display.</span></span> <span data-ttu-id="7dcc3-111">Bu cmdlet'in çıktısı, tam olarak anlamak için kendi çıktı Get-üye cmdlet'i için kanal oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-111">To fully understand the output of that cmdlet, pipe its output to the Get-Member cmdlet.</span></span> <span data-ttu-id="7dcc3-112">Örneğin, aşağıdaki komut, Get-Service cmdlet tarafından nesne çıktısını üyeleri hakkında bilgi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-112">For example, the following command displays information about the members of the object output by the Get-Service cmdlet.</span></span>

```
Get-Service | Get-Member
```

## <a name="consistency"></a><span data-ttu-id="7dcc3-113">Tutarlılık</span><span class="sxs-lookup"><span data-stu-id="7dcc3-113">Consistency</span></span>
<span data-ttu-id="7dcc3-114">Sistemleri yönetme karmaşık bir çaba olabilir ve tutarlı bir arayüz olan araçlarını devralınmış karmaşıklık denetlemek için yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-114">Managing systems can be a complex endeavor and tools that have a consistent interface help to control the inherent complexity.</span></span> <span data-ttu-id="7dcc3-115">Ne yazık ki, komut satırı araçları ne kodlanabilir COM nesneleri için kendi tutarlılık bilinmektedir.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-115">Unfortunately, neither command-line tools nor scriptable COM objects have been known for their consistency.</span></span>

<span data-ttu-id="7dcc3-116">Windows PowerShell tutarlılığını birincil varlıklarını biridir.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-116">The consistency of Windows PowerShell is one of its primary assets.</span></span> <span data-ttu-id="7dcc3-117">Örneğin, Sort-Object cmdlet'i kullanmayı öğrenin, herhangi bir cmdlet'in çıkışını sıralamak için bu bilgi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-117">For example, if you learn how to use the Sort-Object cmdlet, you can use that knowledge to sort the output of any cmdlet.</span></span> <span data-ttu-id="7dcc3-118">Her cmdlet'in farklı sıralama yordamları öğrenin gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-118">You do not have to learn the different sorting routines of each cmdlet.</span></span>

<span data-ttu-id="7dcc3-119">Ayrıca, cmdlet geliştiricilerin kendi cmdlet'leri için sıralama özellikleri tasarım gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-119">In addition, cmdlet developers do not have to design sorting features for their cmdlets.</span></span> <span data-ttu-id="7dcc3-120">Windows PowerShell bunları temel özellikleri sağlar ve bunları arabirimi birçok yönleri hakkında tutarlı olacak şekilde zorlar bir çerçeve sağlar.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-120">Windows PowerShell gives them a framework that provides the basic features and forces them to be consistent about many aspects of the interface.</span></span> <span data-ttu-id="7dcc3-121">Framework bazı geliştiriciler için genellikle sol seçimleri ortadan kaldırır, ancak buna karşılık, güçlü ve kullanımı kolay cmdlet'leri geliştirme daha kolay kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-121">The framework eliminates some of the choices that are typically left to the developer, but, in return, it makes the development of robust and easy-to-use cmdlets much simpler.</span></span>

## <a name="interactive-and-scripting-environments"></a><span data-ttu-id="7dcc3-122">Etkileşimli ve komut dosyası ortamlar</span><span class="sxs-lookup"><span data-stu-id="7dcc3-122">Interactive and Scripting Environments</span></span>
<span data-ttu-id="7dcc3-123">Windows PowerShell komut satırı araçları ve COM nesnelerine erişim verir ve ayrıca, .NET Framework Sınıf Kitaplığı'nı (FCL) güç kullanmanıza olanak sağlar birleştirilmiş etkileşimli ve komut dosyası ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-123">Windows PowerShell is a combined interactive and scripting environment that gives you access to command-line tools and COM objects, and also enables you to use the power of the .NET Framework Class Library (FCL).</span></span>

<span data-ttu-id="7dcc3-124">Bu ortamın üzerine Windows birden çok komut satırı araçları ile etkileşimli bir ortam sağlayan komut, artırır.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-124">This environment improves upon the Windows Command Prompt, which provides an interactive environment with multiple command-line tools.</span></span> <span data-ttu-id="7dcc3-125">İzin veren Windows Komut Dosyası Sistemi'ni (WSH) komut dosyaları de geliştirir birden çok komut satırı araçları ve COM Otomasyon nesneleri kullanır, ancak etkileşimli bir ortam sağlamak değildir.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-125">It also improves upon Windows Script Host (WSH) scripts, which let you use multiple command-line tools and COM automation objects, but do not provide an interactive environment.</span></span>

<span data-ttu-id="7dcc3-126">Bu özelliklerin tümü, erişimi birleştirerek, Windows PowerShell etkileşimli kullanıcı ve komut dosyası yazan yeteneklerini genişletir ve sistem yönetimini daha kolay yönetilebilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-126">By combining access to all of these features, Windows PowerShell extends the ability of the interactive user and the script writer, and makes system administration more manageable.</span></span>

## <a name="object-orientation"></a><span data-ttu-id="7dcc3-127">Nesne yönü</span><span class="sxs-lookup"><span data-stu-id="7dcc3-127">Object Orientation</span></span>
<span data-ttu-id="7dcc3-128">Metinde komutları yazarak Windows PowerShell ile etkileşim karşın, Windows PowerShell nesnelerde, metin değil temel alır.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-128">Although you interact with Windows PowerShell by typing commands in text, Windows PowerShell is based on objects, not text.</span></span> <span data-ttu-id="7dcc3-129">Bir komutun çıktısını bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-129">The output of a command is an object.</span></span> <span data-ttu-id="7dcc3-130">Çıkış nesnesi başka bir komuta kendi giriş gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-130">You can send the output object to another command as its input.</span></span> <span data-ttu-id="7dcc3-131">Sonuç olarak, Windows PowerShell yeni ve güçlü bir komut satırı kip tanıtırken diğer Kabukları ile karşılaştı kişilere bilinen bir arayüz sağlar.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-131">As a result, Windows PowerShell provides a familiar interface to people experienced with other shells, while introducing a new and powerful command-line paradigm.</span></span> <span data-ttu-id="7dcc3-132">Metin yerine nesneleri göndermek için etkinleştirerek komutları arasında veri gönderme kavramını genişletmektedir.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-132">It extends the concept of sending data between commands by enabling you to send objects, rather than text.</span></span>

## <a name="easy-transition-to-scripting"></a><span data-ttu-id="7dcc3-133">Komut dosyası için kolay geçiş</span><span class="sxs-lookup"><span data-stu-id="7dcc3-133">Easy Transition to Scripting</span></span>
<span data-ttu-id="7dcc3-134">Yazmasını geçiş kolay, etkileşimli olarak çok komut dosyası oluşturma ve çalıştırma komutları Windows PowerShell yapar.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-134">Windows PowerShell makes it easy to transition from typing commands interactively to creating and running scripts.</span></span> <span data-ttu-id="7dcc3-135">Bir görevi gerçekleştirmek komutları bulmak için Windows PowerShell komut isteminde komutları yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-135">You can type commands at the Windows PowerShell command prompt to discover the commands that perform a task.</span></span> <span data-ttu-id="7dcc3-136">Sonra bunları bir komut dosyası olarak kullanmak için bir dosya için kopyalamadan önce bir dökümü veya bir geçmiş komutlarda kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7dcc3-136">Then, you can save those commands in a transcript or a history before copying them to a file for use as a script.</span></span>
