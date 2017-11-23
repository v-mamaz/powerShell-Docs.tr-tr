---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC, powershell, yapılandırma, Kur"
title: "İstenen durum yapılandırması hızlı başlangıç"
ms.openlocfilehash: 295a78f3fd85464239d51d7be0defa04d2344689
ms.sourcegitcommit: f069ff0689006fece768f178c10e3e3eeaee09f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/13/2017
---
> <span data-ttu-id="e670f-103">İçin geçerlidir: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="e670f-103">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

# <a name="desired-state-configuration-quick-start"></a><span data-ttu-id="e670f-104">İstenen durum yapılandırması hızlı başlangıç</span><span class="sxs-lookup"><span data-stu-id="e670f-104">Desired State Configuration Quick Start</span></span>

<span data-ttu-id="e670f-105">Bu alıştırmada oluşturma ve istenen durum Yapılandırması'nı (DSC) yapılandırma başlangıçtan bitişe kadar uygulama anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e670f-105">This exercise walks through creating and applying a Desired State Configuration (DSC) configuration from start to finish.</span></span>
<span data-ttu-id="e670f-106">Bir sunucu olduğunu kullanırız örnek sağlar `Web-Server` (IIS) özelliği etkin ve basit bir "Hello World" Web sitesi için içeriğin mevcut olduğunu `intepub\wwwroot` o sunucunun dizin.</span><span class="sxs-lookup"><span data-stu-id="e670f-106">The example we'll use ensures that a server has the `Web-Server` (IIS) feature enabled, and that the content for a simple "Hello World" website is present in the `intepub\wwwroot` directory of that server.</span></span>

<span data-ttu-id="e670f-107">DSC nedir ve nasıl çalıştığı genel bakış için bkz: [istenen durum yapılandırması için genel bakış karar alıcılar](decisionMaker.md).</span><span class="sxs-lookup"><span data-stu-id="e670f-107">For an overview of what DSC is and how it works, see [Desired State Configuration Overview for Decision Makers](decisionMaker.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="e670f-108">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="e670f-108">Requirements</span></span>

<span data-ttu-id="e670f-109">Bu örneği çalıştırmak için Windows Server 2012 veya sonraki sürümünü ve PowerShell 4.0 veya sonraki sürümü çalıştıran bir bilgisayar gerekir.</span><span class="sxs-lookup"><span data-stu-id="e670f-109">To run this example, you will need a computer running Windows Server 2012 or later and PowerShell 4.0 or later.</span></span>

## <a name="write-and-place-the-indexhtm-file"></a><span data-ttu-id="e670f-110">Yazma ve index.htm dosyasını yerleştirin</span><span class="sxs-lookup"><span data-stu-id="e670f-110">Write and place the index.htm file</span></span>

<span data-ttu-id="e670f-111">İlk olarak, Web sitesi içeriği olarak kullanacağız HTML dosyası oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="e670f-111">First, we'll create the HTML file that we will use as the website content.</span></span>

<span data-ttu-id="e670f-112">Kök klasörünüzde adlı bir klasör oluşturun `test`.</span><span class="sxs-lookup"><span data-stu-id="e670f-112">In your root folder, create a folder named `test`.</span></span>

<span data-ttu-id="e670f-113">Bir metin Düzenleyicisi'nde, aşağıdaki metni yazın:</span><span class="sxs-lookup"><span data-stu-id="e670f-113">In a text editor, type the following text:</span></span>

```html
<head></head>
<body>
<p>Hello World!</p>
</body>
```

<span data-ttu-id="e670f-114">Bu olarak Kaydet `index.htm` içinde `test` daha önce oluşturduğunuz klasör.</span><span class="sxs-lookup"><span data-stu-id="e670f-114">Save this as `index.htm` in the `test` folder you created earlier.</span></span> 

## <a name="write-the-configuration"></a><span data-ttu-id="e670f-115">Yazma yapılandırması</span><span class="sxs-lookup"><span data-stu-id="e670f-115">Write the configuration</span></span>

<span data-ttu-id="e670f-116">A [DSC Yapılandırması](configurations.md) tanımlayan bir veya daha fazla hedef bilgisayarların (düğümlerin) yapılandırmak istediğiniz nasıl özel bir PowerShell işlevdir.</span><span class="sxs-lookup"><span data-stu-id="e670f-116">A [DSC configuration](configurations.md) is a special PowerShell function that defines how you want to configure one or more target computers (nodes).</span></span>

<span data-ttu-id="e670f-117">PowerShell ISE aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="e670f-117">In the PowerShell ISE, type the following:</span></span>

```powershell
Configuration WebsiteTest {

    # Import the module that contains the resources we're using.
    Import-DscResource -ModuleName PsDesiredStateConfiguration

    # The Node statement specifies which targets this configuration will be applied to.
    Node 'localhost' {

        # The first resource block ensures that the Web-Server (IIS) feature is enabled.
        WindowsFeature WebServer {
            Ensure = "Present"
            Name   = "Web-Server"
        }

        # The second resource block ensures that the website content copied to the website root folder.
        File WebsiteContent {
            Ensure = 'Present'
            SourcePath = 'c:\test\index.htm'
            DestinationPath = 'c:\inetpub\wwwroot'
        }
    }
}
```

<span data-ttu-id="e670f-118">Dosyayı Farklı Kaydet `WebsiteTest.ps1`.</span><span class="sxs-lookup"><span data-stu-id="e670f-118">Save the file as `WebsiteTest.ps1`.</span></span>

<span data-ttu-id="e670f-119">Bir PowerShell işleviyle anahtar sözcüğü eklenmesi gibi görünüyor görebilirsiniz **yapılandırma** işlevi adı önce kullanıldı.</span><span class="sxs-lookup"><span data-stu-id="e670f-119">You can see that it looks like a PowerShell function, with the addition of the keyword **Configuration** used before the name of the function.</span></span>

<span data-ttu-id="e670f-120">**Düğümü** blok belirtir, bu durumda yapılandırılması için hedef düğümü `localhost`.</span><span class="sxs-lookup"><span data-stu-id="e670f-120">The **Node** block specifies the target node to be configured, in this case `localhost`.</span></span>

<span data-ttu-id="e670f-121">Yapılandırmanın iki çağırır [kaynakları](resources.md), [WindowsFeature](windowsFeatureResource.md) ve [dosya](fileResource.md).</span><span class="sxs-lookup"><span data-stu-id="e670f-121">The configuration calls two [resources](resources.md), [WindowsFeature](windowsFeatureResource.md) and [File](fileResource.md).</span></span>
<span data-ttu-id="e670f-122">Kaynakları hedef düğüm yapılandırması tarafından tanımlanan durumda sağlama iş yapın.</span><span class="sxs-lookup"><span data-stu-id="e670f-122">Resources do the work of ensuring that the target node is in the state defined by the configuration.</span></span>

## <a name="compile-the-configuration"></a><span data-ttu-id="e670f-123">Yapılandırmayı derleme</span><span class="sxs-lookup"><span data-stu-id="e670f-123">Compile the configuration</span></span>

<span data-ttu-id="e670f-124">DSC yapılandırması bir düğüme uygulanacak ilk MOF dosyasına derlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="e670f-124">For a DSC configuration to be applied to a node, it must first be compiled into a MOF file.</span></span>
<span data-ttu-id="e670f-125">Bunu yapmak için yapılandırmanın bir işlev gibi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e670f-125">To do this, you run the configuration like a function.</span></span>
<span data-ttu-id="e670f-126">Bir PowerShell konsolunda yapılandırmanızı kaydettiğiniz klasöre gidin ve bir MOF dosyasına yapılandırmayı derlemek için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e670f-126">In a PowerShell console, navigate to the same folder where you saved your configuration and run the following commands to compile the configuration into a MOF file:</span></span>

```powershell
. .\WebsiteTest.ps1
WebsiteTest
```

<span data-ttu-id="e670f-127">Şu çıkışı üretir:</span><span class="sxs-lookup"><span data-stu-id="e670f-127">This generates the following output:</span></span>

```
Directory: C:\ConfigurationTest\WebsiteTest


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/13/2017   5:20 PM           2746 localhost.mof
```

<span data-ttu-id="e670f-128">İlk satırı yapılandırma işlevi konsolunda kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="e670f-128">The first line makes the configuration function available in the console.</span></span>
<span data-ttu-id="e670f-129">İkinci satır yapılandırması çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="e670f-129">The second line runs the configuration.</span></span>
<span data-ttu-id="e670f-130">Yeni bir klasör adında sonucudur `WebsiteTest` bir alt klasör geçerli klasörde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e670f-130">The result is that a new folder, named `WebsiteTest` is created as a subfolder of the current folder.</span></span>
<span data-ttu-id="e670f-131">`WebsiteTest` Adlı bir dosyayı içeren klasör `localhost.mof`.</span><span class="sxs-lookup"><span data-stu-id="e670f-131">The `WebsiteTest` folder contains a file named `localhost.mof`.</span></span>
<span data-ttu-id="e670f-132">Daha sonra hedef düğüme uygulanan bu dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="e670f-132">It is this file that can then be applied to the target node.</span></span>

## <a name="apply-the-configuration"></a><span data-ttu-id="e670f-133">Yapılandırmasını Uygula</span><span class="sxs-lookup"><span data-stu-id="e670f-133">Apply the configuration</span></span>

<span data-ttu-id="e670f-134">Derlenmiş MOF sahip olduğunuza göre yapılandırma (Bu durumda, yerel bilgisayar) hedef düğüm çağırarak uygulayabileceğiniz [başlangıç DscConfiguration](/reference/5.1/PSDesiredStateConfiguration/Start-DscConfiguration) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="e670f-134">Now that you have the compiled MOF, you can apply the configuration to the target node (in this case, the local computer) by calling the [Start-DscConfiguration](/reference/5.1/PSDesiredStateConfiguration/Start-DscConfiguration) cmdlet.</span></span>

<span data-ttu-id="e670f-135">`Start-DscConfiguration` Cmdlet söyler [yerel Configuration Manager (LCM'yi)](metaConfig.md), yapılandırmayı uygulamak için DSC altyapısı olduğu.</span><span class="sxs-lookup"><span data-stu-id="e670f-135">The `Start-DscConfiguration` cmdlet tells the [Local Configuration Manager (LCM)](metaConfig.md), which is the engine of DSC, to apply the configuration.</span></span>
<span data-ttu-id="e670f-136">Yapılandırmayı uygulamak için DSC kaynakları çağırma işini LCM'yi yapar.</span><span class="sxs-lookup"><span data-stu-id="e670f-136">The LCM does the work of calling the DSC resources to apply the configuration.</span></span>

<span data-ttu-id="e670f-137">Bir PowerShell konsolunda yapılandırmanızı kaydettiğiniz klasöre gidin ve aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e670f-137">In a PowerShell console, navigate to the same folder where you saved your configuration and run the following command:</span></span>

```powershell
Start-DscConfiguration .\WebsiteTest
```

## <a name="test-the-configuration"></a><span data-ttu-id="e670f-138">Yapılandırmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e670f-138">Test the configuration</span></span>

<span data-ttu-id="e670f-139">Çağırabilirsiniz [Get-DscConfigurationStatus](/reference/5.1/PSDesiredStateConfiguration/Get-DscConfigurationStatus) yapılandırmanın başarılı olup olmadığını görmek için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e670f-139">You can call the [Get-DscConfigurationStatus](/reference/5.1/PSDesiredStateConfiguration/Get-DscConfigurationStatus) cmdlet to see whether the configuration succeeded.</span></span> 

<span data-ttu-id="e670f-140">Ayrıca sonuçları doğrudan, bu durumda göz atarak sınayabilirsiniz `http://localhost/` bir web tarayıcısında.</span><span class="sxs-lookup"><span data-stu-id="e670f-140">You can also test the results directly, in this case by browsing to `http://localhost/` in a web browser.</span></span>
<span data-ttu-id="e670f-141">Bu örnekte ilk adım olarak, oluşturduğunuz "Hello World" HTML sayfası görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e670f-141">You should see the "Hello World" HTML page you created as the first step in this example.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e670f-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e670f-142">Next steps</span></span>

- <span data-ttu-id="e670f-143">DSC yapılandırmaları hakkında daha fazla bilgi [DSC yapılandırmaları](configurations.md).</span><span class="sxs-lookup"><span data-stu-id="e670f-143">Find out more about DSC configurations at [DSC configurations](configurations.md).</span></span>
- <span data-ttu-id="e670f-144">Hangi DSC kaynakları kullanılabilir ve özel DSC kaynakları oluşturma bkz [DSC kaynakları](resources.md).</span><span class="sxs-lookup"><span data-stu-id="e670f-144">See what DSC resources are available, and how to create custom DSC resources at [DSC resources](resources.md).</span></span>
- <span data-ttu-id="e670f-145">DSC yapılandırmaları ve kaynakları bulmak [PowerShell Galerisi](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="e670f-145">Find DSC configurations and resources in the [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>


