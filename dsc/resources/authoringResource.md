---
ms.date: 06/12/2017
keywords: DSC, powershell, yapılandırma, Kurulum
title: Derleme özel Windows PowerShell Desired State Configuration kaynakları
ms.openlocfilehash: 882b6efed4564d2354183d7472b301e1e1758335
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53405701"
---
# <a name="build-custom-windows-powershell-desired-state-configuration-resources"></a><span data-ttu-id="6c6dc-103">Derleme özel Windows PowerShell Desired State Configuration kaynakları</span><span class="sxs-lookup"><span data-stu-id="6c6dc-103">Build Custom Windows PowerShell Desired State Configuration Resources</span></span>

> <span data-ttu-id="6c6dc-104">Şunun için geçerlidir: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="6c6dc-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="6c6dc-105">Windows PowerShell Desired State Configuration (DSC), ortamınızı yapılandırmak için kullanabileceğiniz yerleşik kaynaklara sahip.</span><span class="sxs-lookup"><span data-stu-id="6c6dc-105">Windows PowerShell Desired State Configuration (DSC) has built-in resources that you can use to configure your environment.</span></span> <span data-ttu-id="6c6dc-106">Bu konuda, kaynakları ve bağlantıları konulara özel bilgiler ve örnekler ile geliştirmeye genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="6c6dc-106">This topic provides an overview of developing resources and links to topics with specific information and examples.</span></span>

## <a name="dsc-resource-components"></a><span data-ttu-id="6c6dc-107">DSC kaynak bileşenler</span><span class="sxs-lookup"><span data-stu-id="6c6dc-107">DSC resource components</span></span>

<span data-ttu-id="6c6dc-108">DSC kaynak, bir Windows PowerShell modülüdür.</span><span class="sxs-lookup"><span data-stu-id="6c6dc-108">A DSC resource is a Windows PowerShell module.</span></span> <span data-ttu-id="6c6dc-109">Modülü, kaynak için şemanın (yapılandırılabilir özelliklerin tanımı) hem de (yapılandırması tarafından belirtilen asıl işi yapan kod) uygulaması içerir.</span><span class="sxs-lookup"><span data-stu-id="6c6dc-109">The module contains both the schema (the definition of the configurable properties) and the implementation (the code that does the actual work specified by a configuration) for the resource.</span></span> <span data-ttu-id="6c6dc-110">DSC kaynak şema MOF dosyasında tanımlanabilir ve uygulama bir betik modülü tarafından gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="6c6dc-110">A DSC resource schema can be defined in a MOF file, and the implementation is performed by a script module.</span></span> <span data-ttu-id="6c6dc-111">PowerShell sınıflarını sürüm 5 desteği ile başlayarak, uygulama ve şema hem de bir sınıf içinde tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="6c6dc-111">Beginning with the support of PowerShell classes in version 5, the schema and implementation can both be defined in a class.</span></span> <span data-ttu-id="6c6dc-112">Aşağıdaki konularda, DSC kaynakları oluşturmak nasıl daha ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6c6dc-112">The following topics describe in more detail how to create DSC resources.</span></span>

* [<span data-ttu-id="6c6dc-113">MOF ile özel bir DSC kaynağı yazma</span><span class="sxs-lookup"><span data-stu-id="6c6dc-113">Writing a custom DSC resource with MOF</span></span>](authoringResourceMOF.md)
* [<span data-ttu-id="6c6dc-114">DSC kaynak uygulamaC#</span><span class="sxs-lookup"><span data-stu-id="6c6dc-114">Implementing a DSC resource in C#</span></span>](authoringResourceMofCS.md)
* [<span data-ttu-id="6c6dc-115">PowerShell sınıfları ile özel bir DSC kaynağı yazma</span><span class="sxs-lookup"><span data-stu-id="6c6dc-115">Writing a custom DSC resource with PowerShell classes</span></span>](authoringResourceClass.md)
* [<span data-ttu-id="6c6dc-116">Bileşik kaynaklar: DSC yapılandırma kaynağı olarak kullanma</span><span class="sxs-lookup"><span data-stu-id="6c6dc-116">Composite resources: Using a DSC configuration as a resource</span></span>](authoringResourceComposite.md)
* [<span data-ttu-id="6c6dc-117">Kaynak Tasarımcısı aracını kullanma</span><span class="sxs-lookup"><span data-stu-id="6c6dc-117">Using the Resource Designer tool</span></span>](../authoringResourceMofDesigner.md)