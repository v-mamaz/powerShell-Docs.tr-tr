---
ms.date: 06/05/2017
keywords: PowerShell cmdlet'i
title: ISEFile Nesnesi
ms.assetid: 1c6d91f3-c556-42a2-a017-79b6b7b4b7db
ms.openlocfilehash: 24549720b8bc35435882533b0eb138de432ede65
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53405885"
---
# <a name="the-isefile-object"></a><span data-ttu-id="0a64a-103">ISEFile Nesnesi</span><span class="sxs-lookup"><span data-stu-id="0a64a-103">The ISEFile Object</span></span>

<span data-ttu-id="0a64a-104">Bir **Isefile** nesnesi bir dosya içinde Windows PowerShell® Tümleşik komut dosyası ortamı (ISE) temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0a64a-104">An **ISEFile** object represents a file in Windows PowerShell® Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="0a64a-105">Microsoft.PowerShell.Host.ISE.ISEFile sınıfının bir örneğidir.</span><span class="sxs-lookup"><span data-stu-id="0a64a-105">It is an instance of the Microsoft.PowerShell.Host.ISE.ISEFile class.</span></span> <span data-ttu-id="0a64a-106">Bu konu, üye yöntemleri ve üye özellikleri listeler.</span><span class="sxs-lookup"><span data-stu-id="0a64a-106">This topic lists its member methods and member properties.</span></span> <span data-ttu-id="0a64a-107">**$PsISE.CurrentFile** ve bir PowerShell sekmesi dosyaları koleksiyonda dosyalarında Microsoft.PowerShell.Host.ISE.ISEFile sınıfın tüm örnekleri.</span><span class="sxs-lookup"><span data-stu-id="0a64a-107">The **$psISE.CurrentFile** and the files in the Files collection in a PowerShell tab are all instances of the Microsoft.PowerShell.Host.ISE.ISEFile class.</span></span>

## <a name="methods"></a><span data-ttu-id="0a64a-108">Yöntemler</span><span class="sxs-lookup"><span data-stu-id="0a64a-108">Methods</span></span>

### <a name="save-saveencoding-"></a><span data-ttu-id="0a64a-109">Kaydet\( \[saveEncoding\] \)</span><span class="sxs-lookup"><span data-stu-id="0a64a-109">Save\( \[saveEncoding\] \)</span></span>

<span data-ttu-id="0a64a-110">Windows PowerShell ISE 2.0 ve sonraki sürümlerde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="0a64a-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="0a64a-111">Dosyayı diske kaydeder.</span><span class="sxs-lookup"><span data-stu-id="0a64a-111">Saves the file to disk.</span></span>

<span data-ttu-id="0a64a-112">**\[saveEncoding\]**  : isteğe bağlı [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) kaydedilen dosya için kullanılacak parametre kodlama isteğe bağlı bir karakter.</span><span class="sxs-lookup"><span data-stu-id="0a64a-112">**\[saveEncoding\]** - optional [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) An optional character encoding parameter to be used for the saved file.</span></span> <span data-ttu-id="0a64a-113">Varsayılan değer **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="0a64a-113">The default value is **UTF8**.</span></span>

### <a name="exceptions"></a><span data-ttu-id="0a64a-114">Özel Durumlar</span><span class="sxs-lookup"><span data-stu-id="0a64a-114">Exceptions</span></span>

- <span data-ttu-id="0a64a-115">**System.IO.ıoexception**: Dosya kaydedilemedi.</span><span class="sxs-lookup"><span data-stu-id="0a64a-115">**System.IO.IOException**: The file could not be saved.</span></span>

```powershell
# Save the file using the default encoding (UTF8)
$psISE.CurrentFile.Save()

# Save the file as ASCII.
$psISE.CurrentFile.Save([System.Text.Encoding]::ASCII)

# Gets the current encoding.
$myfile = $psISE.CurrentFile
$myfile.Encoding
```

### <a name="saveasfilename-saveencoding"></a><span data-ttu-id="0a64a-116">Farklı Kaydet\(dosya \[saveEncoding\]\)</span><span class="sxs-lookup"><span data-stu-id="0a64a-116">SaveAs\(filename, \[saveEncoding\]\)</span></span>

<span data-ttu-id="0a64a-117">Windows PowerShell ISE 2.0 ve sonraki sürümlerde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="0a64a-117">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="0a64a-118">Dosyayı belirtilen dosya adı ile kaydeder ve kodlama.</span><span class="sxs-lookup"><span data-stu-id="0a64a-118">Saves the file with the specified file name and encoding.</span></span>

<span data-ttu-id="0a64a-119">**filename** -adı, dosyayı kaydetmek için kullanılacak dize.</span><span class="sxs-lookup"><span data-stu-id="0a64a-119">**filename** - String The name to be used to save the file.</span></span>

<span data-ttu-id="0a64a-120">**\[saveEncoding\]**  : isteğe bağlı [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) kaydedilen dosya için kullanılacak parametre kodlama isteğe bağlı bir karakter.</span><span class="sxs-lookup"><span data-stu-id="0a64a-120">**\[saveEncoding\]** - optional [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) An optional character encoding parameter to be used for the saved file.</span></span> <span data-ttu-id="0a64a-121">Varsayılan değer **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="0a64a-121">The default value is **UTF8**.</span></span>

### <a name="exceptions"></a><span data-ttu-id="0a64a-122">Özel Durumlar</span><span class="sxs-lookup"><span data-stu-id="0a64a-122">Exceptions</span></span>

- <span data-ttu-id="0a64a-123">**System.ArgumentNullException**: **Filename** parametresi null.</span><span class="sxs-lookup"><span data-stu-id="0a64a-123">**System.ArgumentNullException**: The **filename** parameter is null.</span></span>
- <span data-ttu-id="0a64a-124">**System.ArgumentException**: **Filename** parametresi boş.</span><span class="sxs-lookup"><span data-stu-id="0a64a-124">**System.ArgumentException**: The **filename** parameter is empty.</span></span>
- <span data-ttu-id="0a64a-125">**System.IO.ıoexception**: Dosya kaydedilemedi.</span><span class="sxs-lookup"><span data-stu-id="0a64a-125">**System.IO.IOException**: The file could not be saved.</span></span>

```powershell
# Save the file with a full path and name.
$fullpath = "c:\temp\newname.txt"
$psISE.CurrentFile.SaveAs($fullPath)
# Save the file with a full path and name and explicitly as UTF8.
$psISE.CurrentFile.SaveAs($fullPath, [System.Text.Encoding]::UTF8)
```

## <a name="properties"></a><span data-ttu-id="0a64a-126">Özellikler</span><span class="sxs-lookup"><span data-stu-id="0a64a-126">Properties</span></span>

### <a name="displayname"></a><span data-ttu-id="0a64a-127">Görünen Ad</span><span class="sxs-lookup"><span data-stu-id="0a64a-127">DisplayName</span></span>

<span data-ttu-id="0a64a-128">Windows PowerShell ISE 2.0 ve sonraki sürümlerde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="0a64a-128">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="0a64a-129">Bu dosya görünen adını içeren dize alan salt okunur özelliği.</span><span class="sxs-lookup"><span data-stu-id="0a64a-129">The read-only property that gets the string that contains the display name of this file.</span></span> <span data-ttu-id="0a64a-130">Şirket adı gösterilir **dosya** Düzenleyici üst kısmındaki sekme.</span><span class="sxs-lookup"><span data-stu-id="0a64a-130">The name is shown on the **File** tab at the top of the editor.</span></span> <span data-ttu-id="0a64a-131">Bir yıldız işareti varlığını \( \* \) adın sonunda dosya kaydedilmemiş değişiklikler sahip olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="0a64a-131">The presence of an asterisk \(\*\) at the end of the name indicates that the file has changes that have not been saved.</span></span>

```powershell
# Shows the display name of the file.
$psISE.CurrentFile.DisplayName
```

### <a name="editor"></a><span data-ttu-id="0a64a-132">Düzenleyici</span><span class="sxs-lookup"><span data-stu-id="0a64a-132">Editor</span></span>

<span data-ttu-id="0a64a-133">Windows PowerShell ISE 2.0 ve sonraki sürümlerde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="0a64a-133">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="0a64a-134">Salt okunur özelliği [Düzenleyici nesnesi](The-ISEEditor-Object.md) belirtilen dosya için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0a64a-134">The read-only property that gets the [editor object](The-ISEEditor-Object.md) that is used for the specified file.</span></span>

```powershell
# Gets the editor and the text.
$psISE.CurrentFile.Editor.Text
```

### <a name="encoding"></a><span data-ttu-id="0a64a-135">Kodlama</span><span class="sxs-lookup"><span data-stu-id="0a64a-135">Encoding</span></span>

<span data-ttu-id="0a64a-136">Windows PowerShell ISE 2.0 ve sonraki sürümlerde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="0a64a-136">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="0a64a-137">Özgün dosya kodlamasını alır salt okunur özellik.</span><span class="sxs-lookup"><span data-stu-id="0a64a-137">The read-only property that gets the original file encoding.</span></span> <span data-ttu-id="0a64a-138">Bu bir **System.Text.Encoding** nesne.</span><span class="sxs-lookup"><span data-stu-id="0a64a-138">This is a **System.Text.Encoding** object.</span></span>

```powershell
# Shows the encoding for the file.
$psISE.CurrentFile.Encoding
```

### <a name="fullpath"></a><span data-ttu-id="0a64a-139">FullPath</span><span class="sxs-lookup"><span data-stu-id="0a64a-139">FullPath</span></span>

<span data-ttu-id="0a64a-140">Windows PowerShell ISE 2.0 ve sonraki sürümlerde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="0a64a-140">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="0a64a-141">Dize, salt okunur özelliği açık dosyanın tam yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="0a64a-141">The read-only property that gets the string that specifies the full path of the opened file.</span></span>

```powershell
# Shows the full path for the file.
$psISE.CurrentFile.FullPath
```

### <a name="issaved"></a><span data-ttu-id="0a64a-142">Kaydedilirken</span><span class="sxs-lookup"><span data-stu-id="0a64a-142">IsSaved</span></span>

<span data-ttu-id="0a64a-143">Windows PowerShell ISE 2.0 ve sonraki sürümlerde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="0a64a-143">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="0a64a-144">Döndürür salt okunur Boolean özelliği **$true** dosyanın son değiştirilme zamanı sonra kaydedilmişse.</span><span class="sxs-lookup"><span data-stu-id="0a64a-144">The read-only Boolean property that returns **$true** if the file has been saved after it was last modified.</span></span>

```powershell
# Determines whether the file has been saved since it was last modified.
$myfile = $psISE.CurrentFile
$myfile.IsSaved
```

### <a name="isuntitled"></a><span data-ttu-id="0a64a-145">IsUntitled</span><span class="sxs-lookup"><span data-stu-id="0a64a-145">IsUntitled</span></span>

<span data-ttu-id="0a64a-146">Windows PowerShell ISE 2.0 ve sonraki sürümlerde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="0a64a-146">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="0a64a-147">Döndüren salt okunur özelliği **$true** dosya hiçbir zaman bir başlık verilmişse.</span><span class="sxs-lookup"><span data-stu-id="0a64a-147">The read-only property that returns **$true** if the file has never been given a title.</span></span>

```powershell
# Determines whether the file has never been given a title.
$psISE.CurrentFile.IsUntitled
$psISE.CurrentFile.SaveAs("temp.txt")
$psISE.CurrentFile.IsUntitled
```

## <a name="see-also"></a><span data-ttu-id="0a64a-148">Ayrıca bkz:</span><span class="sxs-lookup"><span data-stu-id="0a64a-148">See Also</span></span>

- [<span data-ttu-id="0a64a-149">ISEFileCollectionObject</span><span class="sxs-lookup"><span data-stu-id="0a64a-149">The ISEFileCollectionObject</span></span>](The-ISEFileCollection-Object.md)
- [<span data-ttu-id="0a64a-150">Windows PowerShell ISE betik oluşturma nesne modelinin amacı</span><span class="sxs-lookup"><span data-stu-id="0a64a-150">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="0a64a-151">ISE Nesne Modeli Hiyerarşisi</span><span class="sxs-lookup"><span data-stu-id="0a64a-151">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)