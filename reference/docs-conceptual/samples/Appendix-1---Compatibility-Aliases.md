---
ms.date: 06/05/2017
keywords: PowerShell cmdlet'i
title: Ek 1 Uyumluluk Takma Adları
ms.assetid: 96ad921e-1a57-463e-8e60-424faf8b6ef8
ms.openlocfilehash: 113bbee1af185f98777df5767022d54accb69447
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53406007"
---
# <a name="appendix-1---compatibility-aliases"></a><span data-ttu-id="ad99e-103">Ek 1 - uyumluluk takma adları</span><span class="sxs-lookup"><span data-stu-id="ad99e-103">Appendix 1 - Compatibility Aliases</span></span>

<span data-ttu-id="ad99e-104">Windows PowerShell, Windows PowerShell'de tanıdık komut adlarını kullanmak UNIX ve Cmd kullanıcıların çeşitli geçiş diğer adları vardır.</span><span class="sxs-lookup"><span data-stu-id="ad99e-104">Windows PowerShell has several transition aliases that allow UNIX and Cmd users to use familiar command names in Windows PowerShell.</span></span> <span data-ttu-id="ad99e-105">En sık kullanılan diğer adlar diğer adı ve varsa, standart Windows PowerShell diğer Windows PowerShell komutu ile birlikte, aşağıdaki tabloda gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ad99e-105">The most common aliases are shown in the table below, along with the Windows PowerShell command behind the alias and the standard Windows PowerShell alias if one exists.</span></span>

<span data-ttu-id="ad99e-106">Başka bir ad alanından içinde Windows PowerShell Get-diğer ad cmdlet'ini kullanarak işaret eden Windows PowerShell komutunu bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad99e-106">You can find the Windows PowerShell command that any alias points to from within Windows PowerShell by using the Get-Alias cmdlet.</span></span> <span data-ttu-id="ad99e-107">Örneğin **get-diğer ad cls**.</span><span class="sxs-lookup"><span data-stu-id="ad99e-107">For example, type **get-alias cls**.</span></span>

```
CommandType     Name                            Definition
-----------     ----                            ----------
Alias           cls                             Clear-Host
```

|<span data-ttu-id="ad99e-108">CMD komut</span><span class="sxs-lookup"><span data-stu-id="ad99e-108">CMD Command</span></span>|<span data-ttu-id="ad99e-109">UNIX komutu</span><span class="sxs-lookup"><span data-stu-id="ad99e-109">UNIX Command</span></span>|<span data-ttu-id="ad99e-110">PS Komut</span><span class="sxs-lookup"><span data-stu-id="ad99e-110">PS Command</span></span>|<span data-ttu-id="ad99e-111">PS Diğer adı</span><span class="sxs-lookup"><span data-stu-id="ad99e-111">PS Alias</span></span>|
|---------------|----------------|--------------|------------|
|<span data-ttu-id="ad99e-112">**dizini**</span><span class="sxs-lookup"><span data-stu-id="ad99e-112">**dir**</span></span>|<span data-ttu-id="ad99e-113">**Ls**</span><span class="sxs-lookup"><span data-stu-id="ad99e-113">**ls**</span></span>|<span data-ttu-id="ad99e-114">**Get-Childıtem**</span><span class="sxs-lookup"><span data-stu-id="ad99e-114">**Get-ChildItem**</span></span>|<span data-ttu-id="ad99e-115">**gcı**</span><span class="sxs-lookup"><span data-stu-id="ad99e-115">**gci**</span></span>|
|<span data-ttu-id="ad99e-116">**CLS**</span><span class="sxs-lookup"><span data-stu-id="ad99e-116">**cls**</span></span>|<span data-ttu-id="ad99e-117">**Temizle**</span><span class="sxs-lookup"><span data-stu-id="ad99e-117">**clear**</span></span>|<span data-ttu-id="ad99e-118">**Clear-Host** (işlev)</span><span class="sxs-lookup"><span data-stu-id="ad99e-118">**Clear-Host** (function)</span></span>|<span data-ttu-id="ad99e-119">**CLS**</span><span class="sxs-lookup"><span data-stu-id="ad99e-119">**cls**</span></span>|
|<span data-ttu-id="ad99e-120">**DEL, Sil, rmdir**</span><span class="sxs-lookup"><span data-stu-id="ad99e-120">**del, erase, rmdir**</span></span>|<span data-ttu-id="ad99e-121">**RM**</span><span class="sxs-lookup"><span data-stu-id="ad99e-121">**rm**</span></span>|<span data-ttu-id="ad99e-122">**Remove öğesi**</span><span class="sxs-lookup"><span data-stu-id="ad99e-122">**Remove-Item**</span></span>|<span data-ttu-id="ad99e-123">**RI**</span><span class="sxs-lookup"><span data-stu-id="ad99e-123">**ri**</span></span>|
|<span data-ttu-id="ad99e-124">**Kopyalama**</span><span class="sxs-lookup"><span data-stu-id="ad99e-124">**copy**</span></span>|<span data-ttu-id="ad99e-125">**CP**</span><span class="sxs-lookup"><span data-stu-id="ad99e-125">**cp**</span></span>|<span data-ttu-id="ad99e-126">**Öğeyi Kopyala**</span><span class="sxs-lookup"><span data-stu-id="ad99e-126">**Copy-Item**</span></span>|<span data-ttu-id="ad99e-127">**CI**</span><span class="sxs-lookup"><span data-stu-id="ad99e-127">**ci**</span></span>|
|<span data-ttu-id="ad99e-128">**taşıma**</span><span class="sxs-lookup"><span data-stu-id="ad99e-128">**move**</span></span>|<span data-ttu-id="ad99e-129">**MV**</span><span class="sxs-lookup"><span data-stu-id="ad99e-129">**mv**</span></span>|<span data-ttu-id="ad99e-130">**Öğe Taşı**</span><span class="sxs-lookup"><span data-stu-id="ad99e-130">**Move-Item**</span></span>|<span data-ttu-id="ad99e-131">**mı**</span><span class="sxs-lookup"><span data-stu-id="ad99e-131">**mi**</span></span>|
|<span data-ttu-id="ad99e-132">**Yeniden adlandırma**</span><span class="sxs-lookup"><span data-stu-id="ad99e-132">**rename**</span></span>|<span data-ttu-id="ad99e-133">**MV**</span><span class="sxs-lookup"><span data-stu-id="ad99e-133">**mv**</span></span>|<span data-ttu-id="ad99e-134">**Öğeyi yeniden adlandır**</span><span class="sxs-lookup"><span data-stu-id="ad99e-134">**Rename-Item**</span></span>|<span data-ttu-id="ad99e-135">**rni**</span><span class="sxs-lookup"><span data-stu-id="ad99e-135">**rni**</span></span>|
|<span data-ttu-id="ad99e-136">**Türü**</span><span class="sxs-lookup"><span data-stu-id="ad99e-136">**type**</span></span>|<span data-ttu-id="ad99e-137">**cat**</span><span class="sxs-lookup"><span data-stu-id="ad99e-137">**cat**</span></span>|<span data-ttu-id="ad99e-138">**Get-içerik**</span><span class="sxs-lookup"><span data-stu-id="ad99e-138">**Get-Content**</span></span>|<span data-ttu-id="ad99e-139">**GC**</span><span class="sxs-lookup"><span data-stu-id="ad99e-139">**gc**</span></span>|
|<span data-ttu-id="ad99e-140">**CD**</span><span class="sxs-lookup"><span data-stu-id="ad99e-140">**cd**</span></span>|<span data-ttu-id="ad99e-141">**CD**</span><span class="sxs-lookup"><span data-stu-id="ad99e-141">**cd**</span></span>|<span data-ttu-id="ad99e-142">**Konum ayarlama**</span><span class="sxs-lookup"><span data-stu-id="ad99e-142">**Set-Location**</span></span>|<span data-ttu-id="ad99e-143">**SL**</span><span class="sxs-lookup"><span data-stu-id="ad99e-143">**sl**</span></span>|
|<span data-ttu-id="ad99e-144">**MD**</span><span class="sxs-lookup"><span data-stu-id="ad99e-144">**md**</span></span>|<span data-ttu-id="ad99e-145">**mkdir**</span><span class="sxs-lookup"><span data-stu-id="ad99e-145">**mkdir**</span></span>|<span data-ttu-id="ad99e-146">**Yeni öğe**</span><span class="sxs-lookup"><span data-stu-id="ad99e-146">**New-Item**</span></span>|<span data-ttu-id="ad99e-147">**nı**</span><span class="sxs-lookup"><span data-stu-id="ad99e-147">**ni**</span></span>|
|<span data-ttu-id="ad99e-148">**pushd**</span><span class="sxs-lookup"><span data-stu-id="ad99e-148">**pushd**</span></span>|<span data-ttu-id="ad99e-149">**pushd**</span><span class="sxs-lookup"><span data-stu-id="ad99e-149">**pushd**</span></span>|<span data-ttu-id="ad99e-150">**Anında iletme konumu**</span><span class="sxs-lookup"><span data-stu-id="ad99e-150">**Push-Location**</span></span>|<span data-ttu-id="ad99e-151">**pushd**</span><span class="sxs-lookup"><span data-stu-id="ad99e-151">**pushd**</span></span>|
|<span data-ttu-id="ad99e-152">**popd**</span><span class="sxs-lookup"><span data-stu-id="ad99e-152">**popd**</span></span>|<span data-ttu-id="ad99e-153">**popd**</span><span class="sxs-lookup"><span data-stu-id="ad99e-153">**popd**</span></span>|<span data-ttu-id="ad99e-154">**POP konumu**</span><span class="sxs-lookup"><span data-stu-id="ad99e-154">**Pop-Location**</span></span>|<span data-ttu-id="ad99e-155">**popd**</span><span class="sxs-lookup"><span data-stu-id="ad99e-155">**popd**</span></span>|