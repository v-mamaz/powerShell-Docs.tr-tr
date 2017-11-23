---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC, powershell, yapılandırma, Kur"
title: "DSC kaynakları"
ms.openlocfilehash: 62bf352b929d661e585e145e5aab0f44f13010a1
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-resources"></a><span data-ttu-id="b41b2-103">DSC kaynakları</span><span class="sxs-lookup"><span data-stu-id="b41b2-103">DSC Resources</span></span>

><span data-ttu-id="b41b2-104">İçin geçerlidir: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="b41b2-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="b41b2-105">İstenen durum Yapılandırması'nı (DSC) kaynaklar, DSC yapılandırması için yapı taşlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="b41b2-105">Desired State Configuration (DSC) Resources provide the building blocks for a DSC configuration.</span></span> <span data-ttu-id="b41b2-106">Bir kaynak yapılandırılmış (şema) olabilir ve "Bunu yapmak için" yerel Configuration Manager (LCM'yi) çağıran PowerShell Betiği işlevleri içeren özellikleri sunar.</span><span class="sxs-lookup"><span data-stu-id="b41b2-106">A resource exposes properties that can be configured (schema) and contains the PowerShell script functions that the Local Configuration Manager (LCM) calls to "make it so".</span></span>

<span data-ttu-id="b41b2-107">Bir kaynak olarak bir dosya olarak genel veya bir IIS sunucu ayarı olarak belirli bir şey model oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b41b2-107">A resource can model something as generic as a file or as specific as an IIS server setting.</span></span>  <span data-ttu-id="b41b2-108">Grupları, kaynaklar gibi tüm gerekli dosyaları, taşınabilir ve nasıl kullanılmaya kaynaklara yönelik tanımlamak için meta verileri içeren bir yapı düzenler bir DSC modülü, birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="b41b2-108">Groups of like resources are combined in to a DSC Module, which organizes all the required files in to a structure that is portable and includes metadata to identify how the resources are intended to be used.</span></span>  

<span data-ttu-id="b41b2-109">Aşağıdaki konularda, DSC kaynakları açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="b41b2-109">The following topics describe DSC resources:</span></span>

- [<span data-ttu-id="b41b2-110">Yerleşik DSC kaynakları</span><span class="sxs-lookup"><span data-stu-id="b41b2-110">Built-In DSC resources</span></span>](builtInResource.md)
- [<span data-ttu-id="b41b2-111">Özel DSC kaynakları oluşturma</span><span class="sxs-lookup"><span data-stu-id="b41b2-111">Build custom DSC resources</span></span>](authoringResource.md)
- [<span data-ttu-id="b41b2-112">Linux için yerleşik DSC kaynakları</span><span class="sxs-lookup"><span data-stu-id="b41b2-112">Built-In DSC resources for Linux</span></span>](lnxBuiltInResources.md)
