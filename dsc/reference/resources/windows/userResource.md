---
ms.date: 06/12/2017
keywords: DSC, powershell, yapılandırma, Kurulum
title: DSC kullanıcı kaynağı
ms.openlocfilehash: 04543351df19160a2da05ccea96e5d392d8c55bf
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048818"
---
# <a name="dsc-user-resource"></a><span data-ttu-id="62686-103">DSC kullanıcı kaynağı</span><span class="sxs-lookup"><span data-stu-id="62686-103">DSC User Resource</span></span>

<span data-ttu-id="62686-104">Şunun için geçerlidir: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="62686-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="62686-105">**Kullanıcı** kaynak olarak Windows PowerShell Desired State Configuration (DSC) hedef düğümde yerel kullanıcı hesaplarını yönetmek için bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="62686-105">The **User** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage local user accounts on the target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="62686-106">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="62686-106">Syntax</span></span>

```
User [string] #ResourceName
{
    UserName = [string]
    [ Description = [string] ]
    [ Disabled = [bool] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ FullName = [string] ]
    [ Password = [PSCredential] ]
    [ PasswordChangeNotAllowed = [bool] ]
    [ PasswordChangeRequired = [bool] ]
    [ PasswordNeverExpires = [bool] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="62686-107">Özellikler</span><span class="sxs-lookup"><span data-stu-id="62686-107">Properties</span></span>

|  <span data-ttu-id="62686-108">Özellik</span><span class="sxs-lookup"><span data-stu-id="62686-108">Property</span></span>  |  <span data-ttu-id="62686-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="62686-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="62686-110">UserName</span><span class="sxs-lookup"><span data-stu-id="62686-110">UserName</span></span>| <span data-ttu-id="62686-111">Belirli bir durumu sağlamak istediğiniz hesap adını gösterir.</span><span class="sxs-lookup"><span data-stu-id="62686-111">Indicates the account name for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="62686-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="62686-112">Description</span></span>| <span data-ttu-id="62686-113">Kullanıcı hesabı için kullanmak istediğiniz açıklamayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="62686-113">Indicates the description you want to use for the user account.</span></span>|
| <span data-ttu-id="62686-114">Devre Dışı</span><span class="sxs-lookup"><span data-stu-id="62686-114">Disabled</span></span>| <span data-ttu-id="62686-115">Hesabın etkin olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="62686-115">Indicates if the account is enabled.</span></span> <span data-ttu-id="62686-116">Bu özellik kümesine `$true` bu hesabı devre dışı ayarlamanız gerektiğini ve emin olmak için `$false` etkinleştirildiğinden emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="62686-116">Set this property to `$true` to ensure that this account is disabled, and set it to `$false` to ensure that it is enabled.</span></span>|
| <span data-ttu-id="62686-117">Emin olun</span><span class="sxs-lookup"><span data-stu-id="62686-117">Ensure</span></span>| <span data-ttu-id="62686-118">Hesap var olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="62686-118">Indicates if the account exists.</span></span> <span data-ttu-id="62686-119">Bu hesabı var olduğundan emin olmak için "var" özelliğini ayarlayın ve "Eksik için" hesabı yok emin olmak için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="62686-119">Set this property to "Present" to ensure that the account exists, and set it to "Absent" to ensure that the account does not exist.</span></span>|
| <span data-ttu-id="62686-120">Tam adı</span><span class="sxs-lookup"><span data-stu-id="62686-120">FullName</span></span>| <span data-ttu-id="62686-121">Kullanıcı hesabı için kullanmak istediğiniz tam ada sahip bir dizeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="62686-121">Represents a string with the full name you want to use for the user account.</span></span>|
| <span data-ttu-id="62686-122">Parola</span><span class="sxs-lookup"><span data-stu-id="62686-122">Password</span></span>| <span data-ttu-id="62686-123">Bu hesap için kullanmak istediğiniz parolayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="62686-123">Indicates the password you want to use for this account.</span></span> |
| <span data-ttu-id="62686-124">PasswordChangeNotAllowed</span><span class="sxs-lookup"><span data-stu-id="62686-124">PasswordChangeNotAllowed</span></span>| <span data-ttu-id="62686-125">Kullanıcı parola değiştirip değiştiremeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="62686-125">Indicates if the user can change the password.</span></span> <span data-ttu-id="62686-126">Bu özellik kümesine `$true` kullanıcı olamaz parolasını değiştirmek, ayarlayın sağlamak ve `$false` parolayı değiştirmek izin vermek için.</span><span class="sxs-lookup"><span data-stu-id="62686-126">Set this property to `$true` to ensure that the user cannot change the password, and set it to `$false` to allow the user to change the password.</span></span> <span data-ttu-id="62686-127">Varsayılan değer `$false`.</span><span class="sxs-lookup"><span data-stu-id="62686-127">The default value is `$false`.</span></span>|
| <span data-ttu-id="62686-128">PasswordChangeRequired</span><span class="sxs-lookup"><span data-stu-id="62686-128">PasswordChangeRequired</span></span>| <span data-ttu-id="62686-129">Kullanıcı bir sonraki oturum açma sırasında parola değiştirmeli gösterir.</span><span class="sxs-lookup"><span data-stu-id="62686-129">Indicates if the user must change the password at the next sign in.</span></span> <span data-ttu-id="62686-130">Bu özellik kümesine `$true` kullanıcı parolasını değiştirmeniz gerekiyorsa.</span><span class="sxs-lookup"><span data-stu-id="62686-130">Set this property to `$true` if the user must change the password.</span></span> <span data-ttu-id="62686-131">Varsayılan değer `$true`.</span><span class="sxs-lookup"><span data-stu-id="62686-131">The default value is `$true`.</span></span>|
| <span data-ttu-id="62686-132">PasswordNeverExpires</span><span class="sxs-lookup"><span data-stu-id="62686-132">PasswordNeverExpires</span></span>| <span data-ttu-id="62686-133">Parola dolacak gösterir.</span><span class="sxs-lookup"><span data-stu-id="62686-133">Indicates if the password will expire.</span></span> <span data-ttu-id="62686-134">Bu hesap süresi asla sona için parolayı bu özelliği ayarlayın emin olmak için `$true`ve `$false` parola doluyorsa.</span><span class="sxs-lookup"><span data-stu-id="62686-134">To ensure that the password for this account will never expire, set this property to `$true`, and set it to `$false` if the password will expire.</span></span> <span data-ttu-id="62686-135">Varsayılan değer `$false`.</span><span class="sxs-lookup"><span data-stu-id="62686-135">The default value is `$false`.</span></span>|
| <span data-ttu-id="62686-136">DependsOn</span><span class="sxs-lookup"><span data-stu-id="62686-136">DependsOn</span></span> | <span data-ttu-id="62686-137">Bu kaynağı yapılandırılmadan önce başka bir kaynak yapılandırmasını çalıştırmanız gerektiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="62686-137">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="62686-138">Örneğin, kaynak yapılandırmasının Kimliğini çalıştırmak istediğiniz bir blok betik ilk ise **ResourceName** ve kendi türünün **ResourceType**, bu özelliği kullanmak için sözdizimi `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="62686-138">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="62686-139">Örnek</span><span class="sxs-lookup"><span data-stu-id="62686-139">Example</span></span>

```powershell
User UserExample
{
    Ensure = "Present"  # To ensure the user account does not exist, set Ensure to "Absent"
    UserName = "SomeName"
    Password = $passwordCred # This needs to be a credential object
    DependsOn = "[Group]GroupExample" # Configures GroupExample first
}
```