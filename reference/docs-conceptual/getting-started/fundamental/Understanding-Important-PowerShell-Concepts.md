---
ms.date: 08/23/2018
keywords: PowerShell cmdlet'i
title: Önemli PowerShell kavramlarını anlama
ms.assetid: 3e601e38-4520-4578-a48d-b6779f1d35ee
ms.openlocfilehash: 5f8192f962cebb8ee5e5384e39b48de811b11003
ms.sourcegitcommit: 59727f71dc204785a1bcdedc02716d8340a77aeb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2018
ms.locfileid: "43134218"
---
# <a name="understanding-important-powershell-concepts"></a><span data-ttu-id="99b38-103">Önemli PowerShell kavramlarını anlama</span><span class="sxs-lookup"><span data-stu-id="99b38-103">Understanding important PowerShell concepts</span></span>

<span data-ttu-id="99b38-104">PowerShell tasarım kavramları birçok farklı ortamlarından tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="99b38-104">The PowerShell design integrates concepts from many different environments.</span></span> <span data-ttu-id="99b38-105">Birkaç kavramı, kişilere tanıdık Kabukları veya programlama ortamlarında deneyimine sahip olur.</span><span class="sxs-lookup"><span data-stu-id="99b38-105">Several of the concepts will be familiar to people with experience in shells or programming environments.</span></span> <span data-ttu-id="99b38-106">Ancak, birkaç insanın tümünün hakkında öğrenmiş olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="99b38-106">However, few people will know about all of them.</span></span> <span data-ttu-id="99b38-107">Bu kavramlar bazıları isteyen Kabuk yararlı bir genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="99b38-107">Looking at some of these concepts provides a useful overview of the shell.</span></span>

## <a name="output-is-object-based"></a><span data-ttu-id="99b38-108">Nesne tabanlı bir çıktıdır</span><span class="sxs-lookup"><span data-stu-id="99b38-108">Output is object-based</span></span>

<span data-ttu-id="99b38-109">Geleneksel komut satırı arabirimlerinden, PowerShell cmdlet'leri nesneleriyle ilgili şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="99b38-109">Unlike traditional command-line interfaces, PowerShell cmdlets are designed to deal with objects.</span></span>
<span data-ttu-id="99b38-110">Daha fazlasını ekranda görünen karakter dizesini yapılandırılmış bilgileri bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="99b38-110">An object is structured information that is more than just the string of characters appearing on the screen.</span></span> <span data-ttu-id="99b38-111">Komut çıktısında her zaman ihtiyacınız olduğunda kullanabileceğiniz ek bilgiler taşır.</span><span class="sxs-lookup"><span data-stu-id="99b38-111">Command output always carries extra information that you can use if you need it.</span></span>

<span data-ttu-id="99b38-112">Geçmiş verileri işlemek için metin işleme araçları kullandıysanız, farklı PowerShell'de kullanıldığında davranırlar olduğunu bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99b38-112">If you've used text-processing tools to process data in the past, you'll find that they behave differently when used in PowerShell.</span></span> <span data-ttu-id="99b38-113">Çoğu durumda, belirli bilgileri ayıklamak için metin işleme araçları gerekmez.</span><span class="sxs-lookup"><span data-stu-id="99b38-113">In most cases, you don't need text-processing tools to extract specific information.</span></span> <span data-ttu-id="99b38-114">Doğrudan, standart PowerShell nesne sözdizimi kullanarak verileri bölümlerini de erişin.</span><span class="sxs-lookup"><span data-stu-id="99b38-114">You directly access portions of the data using standard PowerShell object syntax.</span></span>

## <a name="the-command-family-is-extensible"></a><span data-ttu-id="99b38-115">Komut seridir Genişletilebilir</span><span class="sxs-lookup"><span data-stu-id="99b38-115">The command family is extensible</span></span>

<span data-ttu-id="99b38-116">Arabirimleri Cmd.exe gibi yerleşik bir komut kümesini doğrudan genişletmek bir yol sunmaz.</span><span class="sxs-lookup"><span data-stu-id="99b38-116">Interfaces such as Cmd.exe don't provide a way for you to directly extend the built-in command set.</span></span>
<span data-ttu-id="99b38-117">Cmd.exe içinde çalışan dış komut satırı araçları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99b38-117">You can create external command-line tools that run in Cmd.exe.</span></span> <span data-ttu-id="99b38-118">Ancak bu dış Araçlar Yardım tümleştirmesi gibi hizmetlerin yoktur.</span><span class="sxs-lookup"><span data-stu-id="99b38-118">But these external tools don't have services, such as Help integration.</span></span> <span data-ttu-id="99b38-119">Cmd.exe otomatik olarak bu dış Araçlar geçerli komutları olduğunu bilmez.</span><span class="sxs-lookup"><span data-stu-id="99b38-119">Cmd.exe doesn't automatically know that these external tools are valid commands.</span></span>

<span data-ttu-id="99b38-120">PowerShell komutları yerel olarak da bilinir *cmdlet'leri* (command-let olarak okunur).</span><span class="sxs-lookup"><span data-stu-id="99b38-120">The native commands in PowerShell are known as *cmdlets* (pronounced command-lets).</span></span> <span data-ttu-id="99b38-121">Kendi cmdlet modülleri oluşturabilir ve işlevleri kullanarak kod veya betiklerde derlenir.</span><span class="sxs-lookup"><span data-stu-id="99b38-121">You can create your own cmdlets modules and functions using compiled code or scripts.</span></span> <span data-ttu-id="99b38-122">Modülleri, cmdlet'leri ve sağlayıcıları kabuğa ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99b38-122">Modules can add cmdlets and providers to the shell.</span></span> <span data-ttu-id="99b38-123">PowerShell UNIX Kabuk betikleri ve Cmd.exe toplu iş dosyaları benzer komut dosyalarını da destekler.</span><span class="sxs-lookup"><span data-stu-id="99b38-123">PowerShell also supports scripts that are analogous to UNIX shell scripts and Cmd.exe batch files.</span></span>

## <a name="powershell-handles-console-input-and-display"></a><span data-ttu-id="99b38-124">PowerShell konsol girdisi ve görüntü işleme</span><span class="sxs-lookup"><span data-stu-id="99b38-124">PowerShell handles console input and display</span></span>

<span data-ttu-id="99b38-125">Bir komut yazın, PowerShell'i her zaman komut satırı girişi doğrudan işler.</span><span class="sxs-lookup"><span data-stu-id="99b38-125">When you type a command, PowerShell always processes the command-line input directly.</span></span> <span data-ttu-id="99b38-126">PowerShell, ayrıca ekranda gördüğünüz çıkış biçimlendirir.</span><span class="sxs-lookup"><span data-stu-id="99b38-126">PowerShell also formats the output that you see on the screen.</span></span> <span data-ttu-id="99b38-127">İş her cmdlet azaltır çünkü bu önemli bir farktır.</span><span class="sxs-lookup"><span data-stu-id="99b38-127">This difference is significant because it reduces the work required of each cmdlet.</span></span> <span data-ttu-id="99b38-128">Herhangi bir cmdlet'i ile aynı şekilde her zaman şeyler yapabilirsiniz sağlar.</span><span class="sxs-lookup"><span data-stu-id="99b38-128">It ensures that you can always do things the same way with any cmdlet.</span></span> <span data-ttu-id="99b38-129">Cmdlet geliştiriciler komut satırı bağımsız değişkenlerini ayrıştırma veya çıktıyı biçimlendirmek için kod yazmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="99b38-129">Cmdlet developers don't need to write code to parse the command-line arguments or format the output.</span></span>

<span data-ttu-id="99b38-130">Geleneksel komut satırı araçları, isteme ve Yardım görüntüleme için kendi şemalara sahip.</span><span class="sxs-lookup"><span data-stu-id="99b38-130">Traditional command-line tools have their own schemes for requesting and displaying Help.</span></span> <span data-ttu-id="99b38-131">Bazı komut satırı araçlarını kullanmak **/?**</span><span class="sxs-lookup"><span data-stu-id="99b38-131">Some command-line tools use **/?**</span></span> <span data-ttu-id="99b38-132">Yardım görüntüleme tetiklemek için; diğerlerinde **-?**, **/H**, hatta **//**.</span><span class="sxs-lookup"><span data-stu-id="99b38-132">to trigger the Help display; others use **-?**, **/H**, or even **//**.</span></span> <span data-ttu-id="99b38-133">Bir GUI penceresi yerine konsolunda görünen bazı Yardım görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="99b38-133">Some will display Help in a GUI window, rather than in the console display.</span></span> <span data-ttu-id="99b38-134">Yanlış parametre kullanırsanız, araç, yazılan ve otomatik olarak bir görevi çalıştırmaya başlar yoksay.</span><span class="sxs-lookup"><span data-stu-id="99b38-134">If you use the wrong parameter, the tool might ignore what you typed and begin executing a task automatically.</span></span>
<span data-ttu-id="99b38-135">PowerShell otomatik olarak ayrıştırır ve komut satırı işlemleri **-?**</span><span class="sxs-lookup"><span data-stu-id="99b38-135">Since PowerShell automatically parses and processes the command line, the **-?**</span></span> <span data-ttu-id="99b38-136">parametresi her zaman "Yardım için bu komutu Göster" anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="99b38-136">parameter always means "show me Help for this command".</span></span>

> [!NOTE]
> <span data-ttu-id="99b38-137">PowerShell'de bir grafik uygulaması çalıştırırsanız, uygulama için bir pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="99b38-137">If you run a graphic application in PowerShell, the window for the application opens.</span></span>
> <span data-ttu-id="99b38-138">PowerShell, yalnızca zaman komut satırı işleme, tedarik veya konsol penceresine döndürülen uygulama çıktısı giriş müdahalesi.</span><span class="sxs-lookup"><span data-stu-id="99b38-138">PowerShell intervenes only when processing the command-line input you supply or the application output returned to the console window.</span></span> <span data-ttu-id="99b38-139">Uygulama dahili olarak şeklini etkilemez.</span><span class="sxs-lookup"><span data-stu-id="99b38-139">It does not affect how the application works internally.</span></span>

## <a name="powershell-uses-some-c-syntax"></a><span data-ttu-id="99b38-140">PowerShell kullanan bazı C# sözdizimi</span><span class="sxs-lookup"><span data-stu-id="99b38-140">PowerShell uses some C# syntax</span></span>

<span data-ttu-id="99b38-141">PowerShell, .NET Framework üzerinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="99b38-141">PowerShell is built on the .NET Framework.</span></span> <span data-ttu-id="99b38-142">Bu bazı özellikleri söz dizimi ve anahtar sözcükler C# programlama dilinin paylaşır.</span><span class="sxs-lookup"><span data-stu-id="99b38-142">It shares some syntax features and keywords with the C# programming language.</span></span> <span data-ttu-id="99b38-143">PowerShell öğrenmek, C# öğrenmek çok daha kolay zorlaştırabilir.</span><span class="sxs-lookup"><span data-stu-id="99b38-143">Learning PowerShell can make it much easier to learn C#.</span></span> <span data-ttu-id="99b38-144">Zaten C# ile biliyorsanız, bu benzerlikler PowerShell daha kolay öğrenme yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99b38-144">If you're already familiar with C#, these similarities can make learning PowerShell easier.</span></span>