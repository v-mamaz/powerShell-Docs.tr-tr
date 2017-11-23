---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC, powershell, yapılandırma, Kur"
title: "MSFT_DSCLocalConfigurationManager sınıfının StopConfiguration yöntemi"
ms.openlocfilehash: f0b550615b20f07f99c8ed7009805c45794bfe22
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/12/2017
---
# <a name="stopconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="0cb82-103">MSFT_DSCLocalConfigurationManager sınıfının StopConfiguration yöntemi</span><span class="sxs-lookup"><span data-stu-id="0cb82-103">StopConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="0cb82-104">Devam ediyor yapılandırma değişikliği durdurur.</span><span class="sxs-lookup"><span data-stu-id="0cb82-104">Stops the configuration change that is in progress.</span></span>

<a name="syntax"></a><span data-ttu-id="0cb82-105">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="0cb82-105">Syntax</span></span>
------

```mof
uint32 StopConfiguration(
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="0cb82-106">Parametreler</span><span class="sxs-lookup"><span data-stu-id="0cb82-106">Parameters</span></span>
----------

<span data-ttu-id="0cb82-107">*zorla* \[içinde\]</span><span class="sxs-lookup"><span data-stu-id="0cb82-107">*force* \[in\]</span></span>  
<span data-ttu-id="0cb82-108">**doğru** durdurmak için yapılandırmayı zorla uygulamak için.</span><span class="sxs-lookup"><span data-stu-id="0cb82-108">**true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="0cb82-109">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="0cb82-109">Return value</span></span>
------------

<span data-ttu-id="0cb82-110">Başarı sıfır döndürür; Aksi takdirde bir hata kodu döndürür.</span><span class="sxs-lookup"><span data-stu-id="0cb82-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="0cb82-111">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="0cb82-111">Remarks</span></span>

<span data-ttu-id="0cb82-112">Bu statik bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="0cb82-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="0cb82-113">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="0cb82-113">Requirements</span></span>
------------
><span data-ttu-id="0cb82-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="0cb82-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="0cb82-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="0cb82-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="0cb82-116">Ayrıca bkz:</span><span class="sxs-lookup"><span data-stu-id="0cb82-116">See also</span></span>


[<span data-ttu-id="0cb82-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="0cb82-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 


