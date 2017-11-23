---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC, powershell, yapılandırma, Kur"
title: "MSFT_DSCLocalConfigurationManager sınıfının ResourceSet yöntemi"
ms.openlocfilehash: 9cd9c1b3f58a5862db6c4eea0488423b8dfe7310
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/12/2017
---
# <a name="resourceset-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="a4648-103">MSFT_DSCLocalConfigurationManager sınıfının ResourceSet yöntemi</span><span class="sxs-lookup"><span data-stu-id="a4648-103">ResourceSet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="a4648-104">Doğrudan çağıran **ayarlamak** DSC kaynağı yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a4648-104">Directly calls the **Set** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="a4648-105">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="a4648-105">Syntax</span></span>
------

```mof
uint32 ResourceSet(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean RebootRequired
);
```

<a name="parameters"></a><span data-ttu-id="a4648-106">Parametreler</span><span class="sxs-lookup"><span data-stu-id="a4648-106">Parameters</span></span>
----------

<span data-ttu-id="a4648-107">*ResourceType* \[içinde\]</span><span class="sxs-lookup"><span data-stu-id="a4648-107">*ResourceType* \[in\]</span></span>  
<span data-ttu-id="a4648-108">Çağrılacak kaynağının adı.</span><span class="sxs-lookup"><span data-stu-id="a4648-108">The name of the resource to call.</span></span>

<span data-ttu-id="a4648-109">*ModuleName* \[içinde\]</span><span class="sxs-lookup"><span data-stu-id="a4648-109">*ModuleName* \[in\]</span></span>  
<span data-ttu-id="a4648-110">Aranacak kaynak içeren modülü adı.</span><span class="sxs-lookup"><span data-stu-id="a4648-110">The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="a4648-111">*resourceProperty* \[içinde\]</span><span class="sxs-lookup"><span data-stu-id="a4648-111">*resourceProperty* \[in\]</span></span>  
<span data-ttu-id="a4648-112">Kaynak özelliği adını ve değerini bir karma tablosunda anahtar ve değer sırasıyla belirtir.</span><span class="sxs-lookup"><span data-stu-id="a4648-112">Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="a4648-113">Kullanım [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) kaynak özelliklerini ve bunların türlerini bulmak için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a4648-113">Use the [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="a4648-114">*RebootRequired* \[çıkışı\]</span><span class="sxs-lookup"><span data-stu-id="a4648-114">*RebootRequired* \[out\]</span></span>  
<span data-ttu-id="a4648-115">Getirisi, bu özelliği ayarlamak **true** hedef düğümün yeniden başlatılması gerekiyorsa.</span><span class="sxs-lookup"><span data-stu-id="a4648-115">On return, this property is set to **true** if the target node needs to be rebooted.</span></span>

## <a name="return-value"></a><span data-ttu-id="a4648-116">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="a4648-116">Return value</span></span>
------------

<span data-ttu-id="a4648-117">Başarı sıfır döndürür; Aksi takdirde bir hata kodu döndürür.</span><span class="sxs-lookup"><span data-stu-id="a4648-117">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="a4648-118">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="a4648-118">Remarks</span></span>

<span data-ttu-id="a4648-119">Bu statik bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="a4648-119">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="a4648-120">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="a4648-120">Requirements</span></span>
------------
><span data-ttu-id="a4648-121">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="a4648-121">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="a4648-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="a4648-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="a4648-123">Ayrıca bkz:</span><span class="sxs-lookup"><span data-stu-id="a4648-123">See also</span></span>


[<span data-ttu-id="a4648-124">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="a4648-124">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)

 

 


