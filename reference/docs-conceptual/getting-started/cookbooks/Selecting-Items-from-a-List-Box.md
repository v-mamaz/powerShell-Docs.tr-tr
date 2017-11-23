---
ms.date: 2017-06-05
keywords: PowerShell cmdlet'i
title: "Bir liste kutusundan öğeler seçme"
ms.assetid: 327c7cc5-21d0-4ace-b151-aa1491d1d3c2
ms.openlocfilehash: 5b41ebfb193062a17abcc6ad6ddf1a2d9241a39e
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/08/2017
---
# <a name="selecting-items-from-a-list-box"></a><span data-ttu-id="ac91a-103">Bir liste kutusundan öğeler seçme</span><span class="sxs-lookup"><span data-stu-id="ac91a-103">Selecting Items from a List Box</span></span>
<span data-ttu-id="ac91a-104">Windows PowerShell 3.0 ve sonraki sürümlerinde öğeleri bir liste kutusu denetimini kullanıcıların seçmesine izin veren bir iletişim kutusu oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="ac91a-104">Use Windows PowerShell 3.0 and later releases to create a dialog box that lets users select items from a list box control.</span></span>

## <a name="create-a-list-box-control-and-select-items-from-it"></a><span data-ttu-id="ac91a-105">Liste kutusu denetimi oluşturma ve öğeleri seçin</span><span class="sxs-lookup"><span data-stu-id="ac91a-105">Create a list box control, and select items from it</span></span>
<span data-ttu-id="ac91a-106">Kopyalayın ve aşağıdaki Windows PowerShell ISE yapıştırın ve sonra Windows PowerShell Betiği (.ps1) kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ac91a-106">Copy and then paste the following into Windows PowerShell ISE, and then save it as a Windows PowerShell script (.ps1).</span></span>

```
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$form = New-Object System.Windows.Forms.Form 
$form.Text = "Select a Computer"
$form.Size = New-Object System.Drawing.Size(300,200) 
$form.StartPosition = "CenterScreen"

$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = "OK"
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)

$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = "Cancel"
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)

$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20) 
$label.Size = New-Object System.Drawing.Size(280,20) 
$label.Text = "Please select a computer:"
$form.Controls.Add($label) 

$listBox = New-Object System.Windows.Forms.ListBox 
$listBox.Location = New-Object System.Drawing.Point(10,40) 
$listBox.Size = New-Object System.Drawing.Size(260,20) 
$listBox.Height = 80

[void] $listBox.Items.Add("atl-dc-001")
[void] $listBox.Items.Add("atl-dc-002")
[void] $listBox.Items.Add("atl-dc-003")
[void] $listBox.Items.Add("atl-dc-004")
[void] $listBox.Items.Add("atl-dc-005")
[void] $listBox.Items.Add("atl-dc-006")
[void] $listBox.Items.Add("atl-dc-007")

$form.Controls.Add($listBox) 

$form.Topmost = $True

$result = $form.ShowDialog()

if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItem
    $x
}
```

<span data-ttu-id="ac91a-107">İki .NET Framework sınıf yükleyerek komut dosyasının başlar: **System.Drawing** ve **System.Windows.Forms**.</span><span class="sxs-lookup"><span data-stu-id="ac91a-107">The script begins by loading two .NET Framework classes: **System.Drawing** and **System.Windows.Forms**.</span></span> <span data-ttu-id="ac91a-108">.NET Framework sınıfının yeni bir örneğini sonra Başlat **System.Windows.Forms.Form'dan**; boş bir form sağlayan veya olduğu başlatabilirsiniz ekleme penceresi denetler.</span><span class="sxs-lookup"><span data-stu-id="ac91a-108">You then start a new instance of the .NET Framework class **System.Windows.Forms.Form**; that provides a blank form or window to which you can start adding controls.</span></span>

```
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing
```

<span data-ttu-id="ac91a-109">Form sınıfının bir örneği oluşturduktan sonra bu sınıfın üç özelliklerine değerler atayın.</span><span class="sxs-lookup"><span data-stu-id="ac91a-109">After you create an instance of the Form class, assign values to three properties of this class.</span></span>

- <span data-ttu-id="ac91a-110">**Metin.**</span><span class="sxs-lookup"><span data-stu-id="ac91a-110">**Text.**</span></span> <span data-ttu-id="ac91a-111">Bu, pencere başlığı olur.</span><span class="sxs-lookup"><span data-stu-id="ac91a-111">This becomes the title of the window.</span></span>

- <span data-ttu-id="ac91a-112">**Boyutu.**</span><span class="sxs-lookup"><span data-stu-id="ac91a-112">**Size.**</span></span> <span data-ttu-id="ac91a-113">Piksel cinsinden formun boyutudur.</span><span class="sxs-lookup"><span data-stu-id="ac91a-113">This is the size of the form, in pixels.</span></span> <span data-ttu-id="ac91a-114">Önceki komut 300 piksel genişliğinde 200 piksel uzunluğunda olan bir form oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ac91a-114">The preceding script creates a form that’s 300 pixels wide by 200 pixels tall.</span></span>

- <span data-ttu-id="ac91a-115">**StartingPosition.**</span><span class="sxs-lookup"><span data-stu-id="ac91a-115">**StartingPosition.**</span></span> <span data-ttu-id="ac91a-116">Bu isteğe bağlı özellik kümesine **CenterScreen** yukarıdaki komut.</span><span class="sxs-lookup"><span data-stu-id="ac91a-116">This optional property is set to **CenterScreen** in the preceding script.</span></span> <span data-ttu-id="ac91a-117">Bu özellik eklemezseniz Windows formu açıldığında bir konum seçer.</span><span class="sxs-lookup"><span data-stu-id="ac91a-117">If you don’t add this property, Windows selects a location when the form is opened.</span></span> <span data-ttu-id="ac91a-118">Ayarlayarak **StartingPosition** için **CenterScreen**, otomatik olarak formun ekran ortasında her yüklenişinde görüntülediğiniz.</span><span class="sxs-lookup"><span data-stu-id="ac91a-118">By setting the **StartingPosition** to **CenterScreen**, you’re automatically displaying the form in the middle of the screen each time it loads.</span></span>

```
$form.Text = "Select a Computer"
$form.Size = New-Object System.Drawing.Size(300,200) 
$form.StartPosition = "CenterScreen"
```

<span data-ttu-id="ac91a-119">Ardından, oluşturun bir **Tamam** formunuz için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ac91a-119">Next, create an **OK** button for your form.</span></span> <span data-ttu-id="ac91a-120">Boyut ve davranışını belirtin **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ac91a-120">Specify the size and behavior of the **OK** button.</span></span> <span data-ttu-id="ac91a-121">Bu örnekte, düğme formun üst köşeden 120 piksel ve sol kenarından 75 piksel konumdur.</span><span class="sxs-lookup"><span data-stu-id="ac91a-121">In this example, the button position is 120 pixels from the form’s top edge, and 75 pixels from the left edge.</span></span> <span data-ttu-id="ac91a-122">Düğme yüksekliği 23 piksel cinsinden açıkken düğmesi uzunluğu 75 pikseldir.</span><span class="sxs-lookup"><span data-stu-id="ac91a-122">The button height is 23 pixels, while the button length is 75 pixels.</span></span> <span data-ttu-id="ac91a-123">Komut dosyasını önceden tanımlanmış Windows Forms türleri düğmesi davranışları belirlemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="ac91a-123">The script uses predefined Windows Forms types to determine the button behaviors.</span></span>

```
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = "OK"
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

<span data-ttu-id="ac91a-124">Benzer şekilde, oluşturduğunuz bir **iptal** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ac91a-124">Similarly, you create a **Cancel** button.</span></span> <span data-ttu-id="ac91a-125">**İptal** üstten 120 piksel ancak penceresinin sol kenarından 150 piksel düğme vardır.</span><span class="sxs-lookup"><span data-stu-id="ac91a-125">The **Cancel** button is 120 pixels from the top, but 150 pixels from the left edge of the window.</span></span>

```
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = "Cancel"
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

<span data-ttu-id="ac91a-126">Ardından, etiket metnini sağlamak için kullanıcıların istediğiniz bilgileri açıklayan pencerenizi üzerinde sağlar.</span><span class="sxs-lookup"><span data-stu-id="ac91a-126">Next, provide label text on your window that describes the information you want users to provide.</span></span> <span data-ttu-id="ac91a-127">Bu durumda, bir bilgisayar seçin seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="ac91a-127">In this case, you want users to select a computer.</span></span>

```
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20) 
$label.Size = New-Object System.Drawing.Size(280,20) 
$label.Text = "Please select a computer:"
$form.Controls.Add($label)
```

<span data-ttu-id="ac91a-128">Etiket metinde açıklanan bilgiler sağlayan kullanıcıların sağlayan denetimi (Bu durumda, bir liste kutusunda) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ac91a-128">Add the control (in this case, a list box) that lets users provide the information you’ve described in your label text.</span></span> <span data-ttu-id="ac91a-129">Liste kutuları yanı sıra uygulayabilirsiniz birçok denetimleri vardır; Daha fazla bilgi için bkz [System.Windows.Forms Namespace](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="ac91a-129">There are many other controls you can apply besides list boxes; for more controls, see [System.Windows.Forms Namespace](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) on MSDN.</span></span>

```
$listBox = New-Object System.Windows.Forms.ListBox 
$listBox.Location = New-Object System.Drawing.Point(10,40) 
$listBox.Size = New-Object System.Drawing.Size(260,20) 
$listBox.Height = 80
```

<span data-ttu-id="ac91a-130">Sonraki bölümde, kullanıcılara görüntülenecek liste kutusu istediğiniz değerleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="ac91a-130">In the next section, you specify the values you want the list box to display to users.</span></span>

> [!NOTE]
> <span data-ttu-id="ac91a-131">Bu komut dosyası tarafından oluşturulan liste kutusu yalnızca bir seçilmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="ac91a-131">The list box created by this script allows only one selection.</span></span> <span data-ttu-id="ac91a-132">Birden çok seçimin sağlayan bir liste kutusu denetimi oluşturmak için bir değer belirtin **SelectionMode** özelliği, aşağıdakine benzer: `$listBox.SelectionMode = "MultiExtended"`.</span><span class="sxs-lookup"><span data-stu-id="ac91a-132">To create a list box control that allows multiple selections, specify a value for the **SelectionMode** property, similarly to the following:  `$listBox.SelectionMode = "MultiExtended"`.</span></span> <span data-ttu-id="ac91a-133">Daha fazla bilgi için bkz: [çoklu seçim liste kutuları](Multiple-selection-List-Boxes.md).</span><span class="sxs-lookup"><span data-stu-id="ac91a-133">For more information, see [Multiple-selection List Boxes](Multiple-selection-List-Boxes.md).</span></span>

```
[void] $listBox.Items.Add("atl-dc-001")
[void] $listBox.Items.Add("atl-dc-002")
[void] $listBox.Items.Add("atl-dc-003")
[void] $listBox.Items.Add("atl-dc-004")
[void] $listBox.Items.Add("atl-dc-005")
[void] $listBox.Items.Add("atl-dc-006")
[void] $listBox.Items.Add("atl-dc-007")
```

<span data-ttu-id="ac91a-134">Liste kutusu denetimini formunuza ekleyin ve diğer windows ve iletişim kutuları üzerinde formu açıldığında açmak için Windows isteyin.</span><span class="sxs-lookup"><span data-stu-id="ac91a-134">Add the list box control to your form, and instruct Windows to open the form atop other windows and dialog boxes when it’s opened.</span></span>

```
$form.Controls.Add($listBox) 
$form.Topmost = $True
```

<span data-ttu-id="ac91a-135">Aşağıdaki Windows formu görüntülemek için kod satırını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ac91a-135">Add the following line of code to display the form in Windows.</span></span>

```
$result = $form.ShowDialog()
```

<span data-ttu-id="ac91a-136">Son olarak, içinde kod **varsa** blok bildirir Windows kullanıcıları liste kutusundan bir seçenek belirleyin ve ardından sonra ne formla **Tamam** düğmesini veya tuşuna **Enter**anahtarı.</span><span class="sxs-lookup"><span data-stu-id="ac91a-136">Finally, the code inside the **If** block instructs Windows what to do with the form after users select an option from the list box, and then click the **OK** button or press the **Enter** key.</span></span>

```
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItem
    $x
}
```

## <a name="see-also"></a><span data-ttu-id="ac91a-137">Ayrıca bkz:</span><span class="sxs-lookup"><span data-stu-id="ac91a-137">See Also</span></span>
- [<span data-ttu-id="ac91a-138">Merhaba Scripting Guy: neden bu PowerShell GUI örnekler çalışmaz?</span><span class="sxs-lookup"><span data-stu-id="ac91a-138">Hey Scripting Guy:  Why don’t these PowerShell GUI examples work?</span></span>](http://go.microsoft.com/fwlink/?LinkId=506644)
- [<span data-ttu-id="ac91a-139">GitHub: Dave Wyatt'ın WinFormsExampleUpdates</span><span class="sxs-lookup"><span data-stu-id="ac91a-139">GitHub: Dave Wyatt's WinFormsExampleUpdates</span></span>](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [<span data-ttu-id="ac91a-140">Haftanın Windows PowerShell İpucu: bir liste kutusundan öğeler seçme</span><span class="sxs-lookup"><span data-stu-id="ac91a-140">Windows PowerShell Tip of the Week:  Selecting Items from a List Box</span></span>](http://technet.microsoft.com/library/ff730949.aspx)
