---
ms.date: 06/05/2017
keywords: PowerShell cmdlet'i
title: Komut zincirinden nesne kaldırma nesne
ms.assetid: 01df8b22-2d22-4e2c-a18d-c004cd3cc284
ms.openlocfilehash: c060b93a3823be26ad6c7757acc633bb4fc2fcfa
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53405947"
---
# <a name="removing-objects-from-the-pipeline-where-object"></a><span data-ttu-id="7f6b4-103">Nesneler (Where-Object) komut zincirinden nesne kaldırma</span><span class="sxs-lookup"><span data-stu-id="7f6b4-103">Removing Objects from the Pipeline (Where-Object)</span></span>

<span data-ttu-id="7f6b4-104">Windows PowerShell'de, genellikle oluşturmak ve istediğinizden daha daha fazla nesne için bir işlem hattı geçirin.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-104">In Windows PowerShell, you often generate and pass along more objects to a pipeline than you want.</span></span> <span data-ttu-id="7f6b4-105">Kullanarak görüntülemek için belirli nesnelerin özelliklerini belirtebilirsiniz **biçimi** cmdlet'leri, ancak bu yardımcı tüm nesneleri görüntüler kaldırmanın sorunlu.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-105">You can specify the properties of particular objects to display by using the **Format** cmdlets, but this does not help with the problem of removing entire objects from the display.</span></span> <span data-ttu-id="7f6b4-106">Yalnızca başlangıçta oluşturulan nesnelerin bir alt kümesinde eylemleri gerçekleştirebilmek için bir işlem hattı bitmeden önce nesneleri filtrelemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-106">You may want to filter objects before the end of a pipeline, so you can perform actions on only a subset of the initially-generated objects.</span></span>

<span data-ttu-id="7f6b4-107">Windows PowerShell içeren bir `Where-Object` her nesne işlem hattında test etmek ve yalnızca bu başarılı işlem hattı belirli test koşulunu karşılıyorsa olanak tanıyan cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-107">Windows PowerShell includes a `Where-Object` cmdlet that allows you to test each object in the pipeline and only pass it along the pipeline if it meets a particular test condition.</span></span> <span data-ttu-id="7f6b4-108">Test geçmeyin nesneleri ardışık düzen tarafından kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-108">Objects that do not pass the test are removed from the pipeline.</span></span> <span data-ttu-id="7f6b4-109">Test koşulu değeri olarak sağladığınız `Where-Object` **FilterScript** parametresi.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-109">You supply the test condition as the value of the `Where-Object` **FilterScript** parameter.</span></span>

### <a name="performing-simple-tests-with-where-object"></a><span data-ttu-id="7f6b4-110">Where-Object içeren basit testler gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="7f6b4-110">Performing Simple Tests with Where-Object</span></span>

<span data-ttu-id="7f6b4-111">Değerini **FilterScript** olduğu bir *betik bloğu* -ayraçları içine alınmış bir veya daha fazla Windows PowerShell komutlarını {} -true veya false değerlendiren.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-111">The value of **FilterScript** is a *script block* -  one or more Windows PowerShell commands surrounded by braces {} - that evaluates to true or false.</span></span> <span data-ttu-id="7f6b4-112">Bu komut dosyası blokları çok basit olabilir ancak bunları oluşturmak için Karşılaştırma işleçleri başka bir Windows PowerShell kavramı hakkında bilmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-112">These script blocks can be very simple, but creating them requires knowing about another Windows PowerShell concept, comparison operators.</span></span> <span data-ttu-id="7f6b4-113">Karşılaştırma işleci, içerdiği her bir tarafta görüntülenen öğe karşılaştırır.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-113">A comparison operator compares the items that appear on each side of it.</span></span> <span data-ttu-id="7f6b4-114">Karşılaştırma işleçleri ile başlayan bir '-' karakteri ve ardından bir adı.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-114">Comparison operators begin with a '-' character and are followed by a name.</span></span> <span data-ttu-id="7f6b4-115">Temel Karşılaştırma işleçleri, neredeyse her türlü nesnesi üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-115">Basic comparison operators work on almost any kind of object.</span></span> <span data-ttu-id="7f6b4-116">Daha gelişmiş Karşılaştırma işleçleri yalnızca metin veya diziler üzerinde çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-116">The more advanced comparison operators might only work on text or arrays.</span></span>

> [!NOTE]
> <span data-ttu-id="7f6b4-117">Varsayılan metin ile çalışırken, Windows PowerShell Karşılaştırma işleçleri büyük/küçük harf duyarsızdır.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-117">By default, when working with text, Windows PowerShell comparison operators are case-insensitive.</span></span>

<span data-ttu-id="7f6b4-118">Dikkat edilecek noktalar ayrıştırma nedeniyle <> gibi simgeler ve = Karşılaştırma işleçleri kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-118">Due to parsing considerations, symbols such as <,>, and = are not used as comparison operators.</span></span> <span data-ttu-id="7f6b4-119">Bunun yerine, Karşılaştırma işleçleri harfini oluşur.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-119">Instead, comparison operators are comprised of letters.</span></span> <span data-ttu-id="7f6b4-120">Aşağıdaki tabloda temel Karşılaştırma işleçleri listelenir.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-120">The basic comparison operators are listed in the following table.</span></span>

|<span data-ttu-id="7f6b4-121">Karşılaştırma işleci</span><span class="sxs-lookup"><span data-stu-id="7f6b4-121">Comparison Operator</span></span>|<span data-ttu-id="7f6b4-122">Anlamı</span><span class="sxs-lookup"><span data-stu-id="7f6b4-122">Meaning</span></span>|<span data-ttu-id="7f6b4-123">Örnek (true değerini döndürür)</span><span class="sxs-lookup"><span data-stu-id="7f6b4-123">Example (returns true)</span></span>|
|-----------------------|-----------|--------------------------|
|<span data-ttu-id="7f6b4-124">-eq</span><span class="sxs-lookup"><span data-stu-id="7f6b4-124">-eq</span></span>|<span data-ttu-id="7f6b4-125">eşittir</span><span class="sxs-lookup"><span data-stu-id="7f6b4-125">is equal to</span></span>|<span data-ttu-id="7f6b4-126">1 - eq 1</span><span class="sxs-lookup"><span data-stu-id="7f6b4-126">1 -eq 1</span></span>|
|<span data-ttu-id="7f6b4-127">-ne</span><span class="sxs-lookup"><span data-stu-id="7f6b4-127">-ne</span></span>|<span data-ttu-id="7f6b4-128">Eşit değildir</span><span class="sxs-lookup"><span data-stu-id="7f6b4-128">Is not equal to</span></span>|<span data-ttu-id="7f6b4-129">1 - ne 2</span><span class="sxs-lookup"><span data-stu-id="7f6b4-129">1 -ne 2</span></span>|
|<span data-ttu-id="7f6b4-130">-lt</span><span class="sxs-lookup"><span data-stu-id="7f6b4-130">-lt</span></span>|<span data-ttu-id="7f6b4-131">olan küçüktür</span><span class="sxs-lookup"><span data-stu-id="7f6b4-131">Is less than</span></span>|<span data-ttu-id="7f6b4-132">1 - lt 2</span><span class="sxs-lookup"><span data-stu-id="7f6b4-132">1 -lt 2</span></span>|
|<span data-ttu-id="7f6b4-133">-le</span><span class="sxs-lookup"><span data-stu-id="7f6b4-133">-le</span></span>|<span data-ttu-id="7f6b4-134">Küçüktür veya eşittir</span><span class="sxs-lookup"><span data-stu-id="7f6b4-134">Is less than or equal to</span></span>|<span data-ttu-id="7f6b4-135">1 - le 2</span><span class="sxs-lookup"><span data-stu-id="7f6b4-135">1 -le 2</span></span>|
|<span data-ttu-id="7f6b4-136">-gt</span><span class="sxs-lookup"><span data-stu-id="7f6b4-136">-gt</span></span>|<span data-ttu-id="7f6b4-137">büyüktür</span><span class="sxs-lookup"><span data-stu-id="7f6b4-137">Is greater than</span></span>|<span data-ttu-id="7f6b4-138">2 - gt 1</span><span class="sxs-lookup"><span data-stu-id="7f6b4-138">2 -gt 1</span></span>|
|<span data-ttu-id="7f6b4-139">-ge</span><span class="sxs-lookup"><span data-stu-id="7f6b4-139">-ge</span></span>|<span data-ttu-id="7f6b4-140">Büyüktür veya eşittir</span><span class="sxs-lookup"><span data-stu-id="7f6b4-140">Is greater than or equal to</span></span>|<span data-ttu-id="7f6b4-141">2 -ge 1</span><span class="sxs-lookup"><span data-stu-id="7f6b4-141">2 -ge 1</span></span>|
|<span data-ttu-id="7f6b4-142">-gibi</span><span class="sxs-lookup"><span data-stu-id="7f6b4-142">-like</span></span>|<span data-ttu-id="7f6b4-143">(Metni için joker karakter karşılaştırma) gibidir</span><span class="sxs-lookup"><span data-stu-id="7f6b4-143">Is like (wildcard comparison for text)</span></span>|<span data-ttu-id="7f6b4-144">"dosyam.doc"-gibi "f\*.yoğun?"</span><span class="sxs-lookup"><span data-stu-id="7f6b4-144">"file.doc" -like "f\*.do?"</span></span>|
|<span data-ttu-id="7f6b4-145">-notlike</span><span class="sxs-lookup"><span data-stu-id="7f6b4-145">-notlike</span></span>|<span data-ttu-id="7f6b4-146">(Metni için joker karakter karşılaştırma) gibi değil</span><span class="sxs-lookup"><span data-stu-id="7f6b4-146">Is not like (wildcard comparison for text)</span></span>|<span data-ttu-id="7f6b4-147">"dosyam.doc"-notlike "p\*.doc"</span><span class="sxs-lookup"><span data-stu-id="7f6b4-147">"file.doc" -notlike "p\*.doc"</span></span>|
|<span data-ttu-id="7f6b4-148">-içerir</span><span class="sxs-lookup"><span data-stu-id="7f6b4-148">-contains</span></span>|<span data-ttu-id="7f6b4-149">içerir</span><span class="sxs-lookup"><span data-stu-id="7f6b4-149">Contains</span></span>|<span data-ttu-id="7f6b4-150">1,2,3 - 1 içerir</span><span class="sxs-lookup"><span data-stu-id="7f6b4-150">1,2,3 -contains 1</span></span>|
|<span data-ttu-id="7f6b4-151">-notcontains</span><span class="sxs-lookup"><span data-stu-id="7f6b4-151">-notcontains</span></span>|<span data-ttu-id="7f6b4-152">içermiyor</span><span class="sxs-lookup"><span data-stu-id="7f6b4-152">Does not contain</span></span>|<span data-ttu-id="7f6b4-153">1,2,3 - notcontains 4</span><span class="sxs-lookup"><span data-stu-id="7f6b4-153">1,2,3 -notcontains 4</span></span>|

<span data-ttu-id="7f6b4-154">WHERE-Object komut dosyası blokları kullanmak özel değişkeni `$_` işlem hattındaki geçerli nesneye başvurmak için.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-154">Where-Object script blocks use the special variable `$_` to refer to the current object in the pipeline.</span></span> <span data-ttu-id="7f6b4-155">Nasıl çalıştığına ilişkin bir örnek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-155">Here is an example of how it works.</span></span> <span data-ttu-id="7f6b4-156">Sayıdan oluşan bir liste olması ve yalnızca 3'ten az olan ayarlara dönmek istiyorsanız, Where-Object yazarak sayıları filtrelemek için kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7f6b4-156">If you have a list of numbers, and only want to return the ones that are less than 3, you can use Where-Object to filter the numbers by typing:</span></span>

```
PS> 1,2,3,4 | Where-Object -FilterScript {$_ -lt 3}
1
2
```

### <a name="filtering-based-on-object-properties"></a><span data-ttu-id="7f6b4-157">Nesne özellikleri tabanlı filtreleme</span><span class="sxs-lookup"><span data-stu-id="7f6b4-157">Filtering Based on Object Properties</span></span>

<span data-ttu-id="7f6b4-158">Bu yana `$_` başvurur geçerli işlem hattı nesnesine biz özelliklerini testlerimiz için erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-158">Since `$_` refers to the current pipeline object, we can access its properties for our tests.</span></span>

<span data-ttu-id="7f6b4-159">Örneğin, WMI Win32_SystemDriver sınıfında biz göz atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-159">As an example, we can look at the Win32_SystemDriver class in WMI.</span></span> <span data-ttu-id="7f6b4-160">Sistem sürücüleri belirli bir sistemde yüzlerce olabilir, ancak yalnızca sistem sürücüleri, hangi şu anda çalışıyor gibi belirli bir kümesini ilginizi çekebilir.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-160">There might be hundreds of system drivers on a particular system, but you might only be interested in a particular set of the system drivers, such as those which are currently running.</span></span> <span data-ttu-id="7f6b4-161">Win32_SystemDriver üyeleri görüntülemek için Get-Member kullanıyorsanız (**Get-WmiObject-sınıfı Win32_SystemDriver | Get-Member - MemberType özelliği**), ilgili özellik durumudur ve sürücü çalışırken "Çalışıyor" değerine sahip olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-161">If you use Get-Member to view Win32_SystemDriver members (**Get-WmiObject -Class Win32_SystemDriver | Get-Member -MemberType Property**) you will see that the relevant property is State, and that it has a value of "Running" when the driver is running.</span></span> <span data-ttu-id="7f6b4-162">Sistem sürücüleri yalnızca çalışan olanları yazarak seçerek filtreleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7f6b4-162">You can filter the system drivers, selecting only the running ones by typing:</span></span>

```powershell
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq 'Running'}
```

<span data-ttu-id="7f6b4-163">Bu, yine de uzun bir liste oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-163">This still produces a long list.</span></span> <span data-ttu-id="7f6b4-164">Yalnızca StartMode değeri de test ederek otomatik olarak başlatılacak şekilde ayarlandığı sürücüleri seçmek için filtre isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7f6b4-164">You may want to filter to only select the drivers set to start automatically by testing the StartMode value as well:</span></span>

```
PS> Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq "Running"} | Where-Object -FilterScript {$_.StartMode -eq "Auto"}

DisplayName : RAS Asynchronous Media Driver
Name        : AsyncMac
State       : Running
Status      : OK
Started     : True

DisplayName : Audio Stub Driver
Name        : audstub
State       : Running
Status      : OK
Started     : True
```

<span data-ttu-id="7f6b4-165">Bu birçok bilgi sürücüleri çalıştığını bildiğimiz artık ihtiyacımız sağlıyor.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-165">This gives us a lot of information we no longer need because we know that the drivers are running.</span></span> <span data-ttu-id="7f6b4-166">Aslında, tek bilgi büyük olasılıkla bu noktada ihtiyacımız var. adı ve görünen adı</span><span class="sxs-lookup"><span data-stu-id="7f6b4-166">In fact, the only information we probably need at this point are the name and the display name.</span></span> <span data-ttu-id="7f6b4-167">Aşağıdaki komutu, çok daha basit çıktısında kaynaklanan yalnızca bu iki özellik içerir:</span><span class="sxs-lookup"><span data-stu-id="7f6b4-167">The following command includes only those two properties, resulting in much simpler output:</span></span>

```
PS> Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq "Running"} | Where-Object -FilterScript {$_.StartMode -eq "Manual"} | Format-Table -Property Name,DisplayName

Name                                    DisplayName
----                                    -----------
AsyncMac                                RAS Asynchronous Media Driver
Fdc                                     Floppy Disk Controller Driver
Flpydisk                                Floppy Disk Driver
Gpc                                     Generic Packet Classifier
IpNat                                   IP Network Address Translator
mouhid                                  Mouse HID Driver
MRxDAV                                  WebDav Client Redirector
mssmbios                                Microsoft System Management BIOS Driver
```

<span data-ttu-id="7f6b4-168">Yukarıdaki komutta iki Where-Object öğe vardır, ancak bunlar içinde tek bir Where-Object öğesi kullanarak ifade edilebilir ve bunun gibi mantıksal işleç:</span><span class="sxs-lookup"><span data-stu-id="7f6b4-168">There are two Where-Object elements in the above command, but they can be expressed in a single Where-Object element by using the -and logical operator, like this:</span></span>

```powershell
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript { ($_.State -eq 'Running') -and ($_.StartMode -eq 'Manual') } | Format-Table -Property Name,DisplayName
```

<span data-ttu-id="7f6b4-169">Aşağıdaki tabloda standart mantıksal işleçleri listelenir.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-169">The standard logical operators are listed in the following table.</span></span>

|<span data-ttu-id="7f6b4-170">Mantıksal işleci</span><span class="sxs-lookup"><span data-stu-id="7f6b4-170">Logical Operator</span></span>|<span data-ttu-id="7f6b4-171">Anlamı</span><span class="sxs-lookup"><span data-stu-id="7f6b4-171">Meaning</span></span>|<span data-ttu-id="7f6b4-172">Örnek (true değerini döndürür)</span><span class="sxs-lookup"><span data-stu-id="7f6b4-172">Example (returns true)</span></span>|
|--------------------|-----------|--------------------------|
|<span data-ttu-id="7f6b4-173">- ve</span><span class="sxs-lookup"><span data-stu-id="7f6b4-173">-and</span></span>|<span data-ttu-id="7f6b4-174">Mantıksal ve; Her iki tarafında da true ise true</span><span class="sxs-lookup"><span data-stu-id="7f6b4-174">Logical and; true if both sides are true</span></span>|<span data-ttu-id="7f6b4-175">(1 - eq 1) - ve (2 - eq 2).</span><span class="sxs-lookup"><span data-stu-id="7f6b4-175">(1 -eq 1) -and (2 -eq 2)</span></span>|
|<span data-ttu-id="7f6b4-176">- veya</span><span class="sxs-lookup"><span data-stu-id="7f6b4-176">-or</span></span>|<span data-ttu-id="7f6b4-177">Mantıksal veya; Her iki taraf doğru ise true</span><span class="sxs-lookup"><span data-stu-id="7f6b4-177">Logical or; true if either side is true</span></span>|<span data-ttu-id="7f6b4-178">(1 - eq 1) - veya (1 - eq 2).</span><span class="sxs-lookup"><span data-stu-id="7f6b4-178">(1 -eq 1) -or (1 -eq 2)</span></span>|
|<span data-ttu-id="7f6b4-179">-değil</span><span class="sxs-lookup"><span data-stu-id="7f6b4-179">-not</span></span>|<span data-ttu-id="7f6b4-180">Mantıksal değil; TRUE ve false tersine çevirir.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-180">Logical not; reverses true and false</span></span>|<span data-ttu-id="7f6b4-181">-değil (1 - eq 2)</span><span class="sxs-lookup"><span data-stu-id="7f6b4-181">-not (1 -eq 2)</span></span>|
|\!|<span data-ttu-id="7f6b4-182">Mantıksal değil; TRUE ve false tersine çevirir.</span><span class="sxs-lookup"><span data-stu-id="7f6b4-182">Logical not; reverses true and false</span></span>|<span data-ttu-id="7f6b4-183">\!(1 - eq 2)</span><span class="sxs-lookup"><span data-stu-id="7f6b4-183">\!(1 -eq 2)</span></span>|