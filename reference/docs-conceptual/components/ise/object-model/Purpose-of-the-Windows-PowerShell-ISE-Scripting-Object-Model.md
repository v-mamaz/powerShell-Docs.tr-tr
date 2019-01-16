---
ms.date: 06/05/2017
keywords: PowerShell cmdlet'i
title: Windows PowerShell ISE Betik Oluşturma Nesne Modelinin Amacı
ms.assetid: d176a131-ab0c-43ee-80c1-f824ab8e4a05
ms.openlocfilehash: fd5ac2c34b173d4eba7636bb5760b1ac9abb4277
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53406003"
---
# <a name="purpose-of-the-windows-powershell-ise-scripting-object-model"></a><span data-ttu-id="7ccf9-103">Windows PowerShell ISE Betik Oluşturma Nesne Modelinin Amacı</span><span class="sxs-lookup"><span data-stu-id="7ccf9-103">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>

<span data-ttu-id="7ccf9-104">Nesneleri, form ve işlevi, Windows PowerShell Tümleşik komut dosyası ortamı (ISE) ile ilişkilendirilir.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-104">Objects are associated with the form and function of Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="7ccf9-105">Nesne Modeli Başvurusu özellikleri ve bu nesneler kullanıma yöntemleri üyeyle ilgili ayrıntıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-105">The object model reference provides details about the member properties and methods that these objects expose.</span></span> <span data-ttu-id="7ccf9-106">Örnekler, doğrudan bu yöntemlere ve özelliklere erişmek için komut dosyalarını nasıl kullanabileceğinizi gösterecek şekilde sağlanır.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-106">Examples are provided to show how you can use scripts to directly access these methods and properties.</span></span> <span data-ttu-id="7ccf9-107">Betik oluşturma nesne modeli, aşağıdaki dizi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-107">The scripting object model makes the following range of tasks easier.</span></span>

## <a name="customizing-the-appearance-of-windows-powershell-ise"></a><span data-ttu-id="7ccf9-108">Windows PowerShell ISE görünümünü özelleştirme</span><span class="sxs-lookup"><span data-stu-id="7ccf9-108">Customizing the appearance of Windows PowerShell ISE</span></span>

<span data-ttu-id="7ccf9-109">Uygulama ayarları ve seçenekleri değiştirmek için nesne modeli kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-109">You can use the object model to modify the application settings and options.</span></span> <span data-ttu-id="7ccf9-110">Örneğin, bunları aşağıdaki gibi değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7ccf9-110">For example, you can modify them as follows:</span></span>

- <span data-ttu-id="7ccf9-111">Hata ayıklama çıkarır ve hataları, uyarıları, ayrıntılı çıkış rengini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-111">You can change the color of errors, warnings, verbose outputs, and debug outputs.</span></span>
- <span data-ttu-id="7ccf9-112">Get veya komut bölmesi, çıkış bölmesi ve betik bölmesini arka plan renklerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-112">You can get or set the background colors for the Command pane, the Output pane, and the Script pane.</span></span>
- <span data-ttu-id="7ccf9-113">Çıkış Bölmesi ' ön plan rengini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-113">You can set the foreground color for the Output pane.</span></span>
- <span data-ttu-id="7ccf9-114">Windows PowerShell ISE için yazı tipi boyutunu ve yazı tipi adı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-114">You can set the font name and font size for Windows PowerShell ISE.</span></span>
- <span data-ttu-id="7ccf9-115">Uyarıları yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-115">You can configure warnings.</span></span> <span data-ttu-id="7ccf9-116">Bu ayar birden fazla PowerShell sekme veya dosyayı kaydetmeden önce bir betik dosyasında çalıştırıldığında bir dosya açıldığında, verilen uyarıları içerir.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-116">This setting includes warnings that are issued when a file is opened in multiple PowerShell tabs or when a script in the file is run before the file has been saved.</span></span>
- <span data-ttu-id="7ccf9-117">Betik bölmesini çıkış Bölmesi'üstünde olduğu betik bölmesi ve çıkış Bölmesi ' yan yana olduğu bir görünümü ve görünüm arasında geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-117">You can switch between a view where the Script pane and the Output pane are side-by-side and a view where the Script pane is on top of the Output pane.</span></span> <span data-ttu-id="7ccf9-118">Alt veya üst çıkış bölmesi için komut bölmesine sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-118">You can dock the Command pane to the bottom or the top of the Output pane.</span></span>

## <a name="enhancing-the-functionality-of-windows-powershell-ise"></a><span data-ttu-id="7ccf9-119">Windows PowerShell ISE işlevselliğini geliştirme</span><span class="sxs-lookup"><span data-stu-id="7ccf9-119">Enhancing the functionality of Windows PowerShell ISE</span></span>

<span data-ttu-id="7ccf9-120">Windows PowerShell ISE işlevselliğini geliştirmek için nesne modeli kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-120">You can use the object model to enhance the functionality of Windows PowerShell ISE.</span></span> <span data-ttu-id="7ccf9-121">Örneğin, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7ccf9-121">For example, you can:</span></span>

- <span data-ttu-id="7ccf9-122">Ekleyebilir ve Windows PowerShell ISE kendi örneğini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-122">Add and modify the instance of Windows PowerShell ISE itself.</span></span> <span data-ttu-id="7ccf9-123">Örneğin, menüleri değiştirmek için yeni menü öğeleri ekleme ve betikleri için yeni menü öğelerini eşleyin.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-123">For example, to change the menus, you can add new menu items and map the new menu items to scripts.</span></span>
- <span data-ttu-id="7ccf9-124">Windows PowerShell ISE'de düğmeler ve menü komutlarını kullanarak gerçekleştirebileceğiniz görevlerden bazılarını gerçekleştirmek betikleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-124">Create scripts that perform some of the tasks that you can perform by using the menu commands and buttons in Windows PowerShell ISE.</span></span> <span data-ttu-id="7ccf9-125">Örneğin, Ekle, Kaldır veya PowerShell sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-125">For example, you can add, remove, or select a PowerShell tab.</span></span>
- <span data-ttu-id="7ccf9-126">Menü komutları ve düğmeleri kullanarak gerçekleştirilebilir tamamlayan görev.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-126">Complement tasks that can be performed by using menu commands and buttons.</span></span> <span data-ttu-id="7ccf9-127">Örneğin, bir PowerShell sekmesi yeniden adlandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-127">For example, you can rename a PowerShell tab.</span></span>
- <span data-ttu-id="7ccf9-128">Bir dosyayla ilişkili metin arabelleği komut bölmesi, çıkış bölmesi ve betik bölmesini işleyin.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-128">Manipulate text buffers for the Command pane, the Output pane, and the Script pane that are associated with a file.</span></span> <span data-ttu-id="7ccf9-129">Örneğin, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7ccf9-129">For example, you can:</span></span>
  - <span data-ttu-id="7ccf9-130">Alın veya tüm metni ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-130">Get or set all text.</span></span>
  - <span data-ttu-id="7ccf9-131">Alın veya metin seçimi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-131">Get or set a text selection.</span></span>
  - <span data-ttu-id="7ccf9-132">Komut dosyası çalıştırma veya seçili bir bölümü bir komut çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-132">Run a script or run a selected portion of a script.</span></span>
  - <span data-ttu-id="7ccf9-133">Bir satır görünümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-133">Scroll a line into view.</span></span>
  - <span data-ttu-id="7ccf9-134">Giriş işareti konumuna metin ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-134">Insert text at a caret position.</span></span>
  - <span data-ttu-id="7ccf9-135">Metin bloğu seçin.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-135">Select a block of text.</span></span>
  - <span data-ttu-id="7ccf9-136">Son satır numarasını alın.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-136">Get the last line number.</span></span>
- <span data-ttu-id="7ccf9-137">Dosya işlemleri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-137">Perform file operations.</span></span> <span data-ttu-id="7ccf9-138">Örneğin, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7ccf9-138">For example, you can:</span></span>
  - <span data-ttu-id="7ccf9-139">Bir dosyayı açmak, bir dosyaya kaydedin veya farklı bir ad kullanarak bir dosyaya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-139">Open a file, save a file, or save a file by using a different name.</span></span>
  - <span data-ttu-id="7ccf9-140">Son kaydedildikten sonra bir dosyanın değiştirilip değiştirilmediğini belirler.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-140">Determine whether a file has been changed after it was last saved.</span></span>
  - <span data-ttu-id="7ccf9-141">Dosya adını alın.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-141">Get the file name.</span></span>
  - <span data-ttu-id="7ccf9-142">Bir dosya seçin.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-142">Select a file.</span></span>

## <a name="automating-tasks"></a><span data-ttu-id="7ccf9-143">Görevleri otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="7ccf9-143">Automating tasks</span></span>

<span data-ttu-id="7ccf9-144">Betik oluşturma nesne modeli, sık kullanılan işlemler için klavye kısayolları oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ccf9-144">You can use the scripting object model to create keyboard shortcuts for frequent operations.</span></span>

## <a name="see-also"></a><span data-ttu-id="7ccf9-145">Ayrıca bkz:</span><span class="sxs-lookup"><span data-stu-id="7ccf9-145">See also</span></span>

- [<span data-ttu-id="7ccf9-146">ISE Nesne Modeli Hiyerarşisi</span><span class="sxs-lookup"><span data-stu-id="7ccf9-146">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)