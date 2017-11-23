---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC, powershell, yapılandırma, Kur"
title: "Yapılandırma verilerini seçeneklerinde kimlik bilgileri"
ms.openlocfilehash: 94ff541fc517254ef2876c424307513eaf1d362a
ms.sourcegitcommit: 28e71b0ae868014523631fec3f5417de751944f3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/25/2017
---
# <a name="credentials-options-in-configuration-data"></a><span data-ttu-id="3960f-103">Yapılandırma verilerini seçeneklerinde kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="3960f-103">Credentials Options in Configuration Data</span></span>
><span data-ttu-id="3960f-104">İçin geçerlidir: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="3960f-104">Applies To: Windows PowerShell 5.0</span></span>

## <a name="plain-text-passwords-and-domain-users"></a><span data-ttu-id="3960f-105">Düz metin parola ve etki alanı kullanıcıları</span><span class="sxs-lookup"><span data-stu-id="3960f-105">Plain Text Passwords and Domain Users</span></span>

<span data-ttu-id="3960f-106">DSC yapılandırmaları şifreleme olmadan kimlik bilgisi içeren düz metin parolalarını ilgili bir hata iletisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3960f-106">DSC configurations containing a credential without encryption will generate an error message about plain text passwords.</span></span>
<span data-ttu-id="3960f-107">Ayrıca, DSC etki alanı kimlik bilgileri kullanırken bir uyarı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3960f-107">Also, DSC will generate a warning when using domain credentials.</span></span>
<span data-ttu-id="3960f-108">Gizlemek için bu hata ve uyarı iletileri DSC yapılandırma verileri anahtar sözcükler kullanın:</span><span class="sxs-lookup"><span data-stu-id="3960f-108">To suppress these error and warning messages use the DSC configuration data keywords:</span></span>
* <span data-ttu-id="3960f-109">**PsDscAllowPlainTextPassword**</span><span class="sxs-lookup"><span data-stu-id="3960f-109">**PsDscAllowPlainTextPassword**</span></span>
* <span data-ttu-id="3960f-110">**PsDscAllowDomainUser**</span><span class="sxs-lookup"><span data-stu-id="3960f-110">**PsDscAllowDomainUser**</span></span>

><span data-ttu-id="3960f-111">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3960f-111">**Notes:**</span></span> <p><span data-ttu-id="3960f-112">Depolama/iletmek düz metin parolalarını şifrelenmemiş genellikle güvenli değildir.</span><span class="sxs-lookup"><span data-stu-id="3960f-112">Storing/transmitting plaintext passwords unencrypted is generally not secure.</span></span> <span data-ttu-id="3960f-113">Bu konuda açıklanan teknikleri kullanarak kimlik bilgilerini güvenli hale getirme önerilir.</span><span class="sxs-lookup"><span data-stu-id="3960f-113">Securing credentials by using the techniques covered later in this topic is recommended.</span></span></p> <p><span data-ttu-id="3960f-114">Azure Otomasyonu DSC hizmet yapılandırmalarında derlenmiş ve güvenli şekilde depolanan kimlik bilgileri merkezi olarak yönetmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="3960f-114">The Azure Automation DSC service allows you to centrally manage credentials to be compiled in configurations and stored securely.</span></span>  <span data-ttu-id="3960f-115">Bilgi için bkz: [derleme DSC yapılandırmaları / kimlik bilgisi varlıkları](https://docs.microsoft.com/en-in/azure/automation/automation-dsc-compile#credential-assets)</span><span class="sxs-lookup"><span data-stu-id="3960f-115">For information, see: [Compiling DSC Configurations / Credential Assets](https://docs.microsoft.com/en-in/azure/automation/automation-dsc-compile#credential-assets)</span></span></p>

<span data-ttu-id="3960f-116">Düz metin kimlik bilgileri geçirme bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="3960f-116">The following is an example of passing plain text credentials:</span></span>

```powershell
#Prompt user for their credentials
#credentials will be unencrypted in the MOF
$promptedCreds = get-credential -Message "Please enter your credentials to generate a DSC MOF:"

# Store passwords in plaintext, in the document itself
# will also be stored in plaintext in the mof
$password = "ThisIsAPlaintextPassword" | ConvertTo-SecureString -asPlainText -Force
$username = "User1"
[PSCredential] $credential = New-Object System.Management.Automation.PSCredential($username,$password)

# DSC requires explicit confirmation before storing passwords insecurely
$ConfigurationData = @{
    AllNodes = @(
        @{
            # The "*" means "all nodes named in ConfigData" so we don't have to repeat ourselves
            NodeName="*"
            PSDscAllowPlainTextPassword = $true
        },
        #however, each node still needs to be explicitly defined for "*" to have meaning
        @{
            NodeName = "TestMachine1"
        },
        #we can also use a property to define node-specific passwords, although this is no more secure
        @{
            NodeName = "TestMachine2";
            UserName = "User2"
            LocalPassword = "ThisIsYetAnotherPlaintextPassword"
        }
        )
}
configuration unencryptedPasswordDemo
{
    Node "TestMachine1"
    {
        # We use the plaintext password to generate a new account
        User User1
        {
            UserName = $username
            Password = $credential
            Description = "local account"
            Ensure = "Present"
            Disabled = $false
            PasswordNeverExpires = $true
            PasswordChangeRequired = $false
        }
        # We use the prompted password to add this account to the local admins group
        Group addToAdmin
        {
            # Ensure the user exists before we add the user to a group
            DependsOn = "[User]User1"
            Credential = $promptedCreds
            GroupName = "Administrators"
            Ensure = "Present"
            MembersToInclude = "User1"
        }
    }

    Node "TestMachine2"
    {
        # Now we'll use a node-specific password to this machine
        $password = $Node.LocalPass | ConvertTo-SecureString -asPlainText -Force
        $username = $node.UserName
        [PSCredential] $nodeCred = New-Object System.Management.Automation.PSCredential($username,$password)

        User User2
        {
            UserName = $username
            Password = $nodeCred
            Description = "local account"
            Ensure = "Present"
            Disabled = $false
            PasswordNeverExpires = $true
            PasswordChangeRequired = $false
        }

        Group addToAdmin
        {
            Credential = $domain
            GroupName = "Administrators"
            DependsOn = "[User]User2"
            Ensure = "Present"
            MembersToInclude = "User2"
        }
    }

}
# We declared the ConfigurationData in a local variable, but we need to pass it in to our configuration function
# We need to invoke the configuration function we created to generate a MOF
unencryptedPasswordDemo -ConfigurationData $ConfigurationData
# We need to pass the MOF to the machines we named.
#-wait: doesn't use jobs so we get blocked at the prompt until the configuration is done
#-verbose: so we can see what's going on and catch any errors
#-force: for testing purposes, I run start-dscconfiguration frequently + want to make sure i'm
#        not blocked by previous configurations that are still running
Start-DscConfiguration ./unencryptedPasswordDemo -verbose -wait -force
```

## <a name="handling-credentials-in-dsc"></a><span data-ttu-id="3960f-117">DSC kimlik bilgilerini işleme</span><span class="sxs-lookup"><span data-stu-id="3960f-117">Handling Credentials in DSC</span></span>

<span data-ttu-id="3960f-118">DSC yapılandırması kaynakları Farklı Çalıştır `Local System` varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="3960f-118">DSC configuration resources run as `Local System` by default.</span></span>
<span data-ttu-id="3960f-119">Ancak, bazı kaynaklar bir kimlik bilgileri, örneğin gerektiğinde `Package` kaynak belirli bir kullanıcı hesabı altında yazılımı yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3960f-119">However, some resources need a credential, for example when the `Package` resource needs to install software under a specific user account.</span></span>

<span data-ttu-id="3960f-120">Önceki kaynakların kullanılan bir sabit kodlanmış `Credential` bu durumu çözmek için özellik adı.</span><span class="sxs-lookup"><span data-stu-id="3960f-120">Earlier resources used a hard-coded `Credential` property name to handle this.</span></span>
<span data-ttu-id="3960f-121">WMF 5.0 eklenen otomatik `PsDscRunAsCredential` tüm kaynaklar için özellik.</span><span class="sxs-lookup"><span data-stu-id="3960f-121">WMF 5.0 added an automatic `PsDscRunAsCredential` property for all resources.</span></span>
<span data-ttu-id="3960f-122">Kullanma hakkında bilgi için `PsDscRunAsCredential`, bkz: [çalıştıran DSC kullanıcı kimlik bilgileriyle](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="3960f-122">For information about using `PsDscRunAsCredential`, see [Running DSC with user credentials](runAsUser.md).</span></span>
<span data-ttu-id="3960f-123">Daha yeni kaynakları ve özel kaynakları için kimlik bilgilerini kendi özelliği oluşturmak yerine bu otomatik özelliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3960f-123">Newer resources and custom resources can use this automatic property instead of creating their own property for credentials.</span></span>

><span data-ttu-id="3960f-124">**Not:** bazı kaynaklar tasarımını olan belirli bir nedenle birden çok kimlik bilgilerini kullanmayı ve kendi kimlik özelliklerine sahip olur.</span><span class="sxs-lookup"><span data-stu-id="3960f-124">**Note:** the design of some resources are to use multiple credentials for a specific reason, and they will have their own credential properties.</span></span>

<span data-ttu-id="3960f-125">Kullanılabilir kimlik bilgisi bulmak için bir kaynak özelliklerini kullanın ya da `Get-DscResource -Name ResourceName -Syntax` veya işe IntelliSense (`CTRL+SPACE`).</span><span class="sxs-lookup"><span data-stu-id="3960f-125">To find the available credential properties on a resource use either `Get-DscResource -Name ResourceName -Syntax` or the Intellisense in the ISE (`CTRL+SPACE`).</span></span>

```powershell
PS C:\> Get-DscResource -Name Group -Syntax
Group [String] #ResourceName
{
    GroupName = [string]
    [Credential = [PSCredential]]
    [DependsOn = [string[]]]
    [Description = [string]]
    [Ensure = [string]{ Absent | Present }]
    [Members = [string[]]]
    [MembersToExclude = [string[]]]
    [MembersToInclude = [string[]]]
    [PsDscRunAsCredential = [PSCredential]]
}
```

<span data-ttu-id="3960f-126">Bu örnekte bir [grup](https://msdn.microsoft.com/en-us/powershell/dsc/groupresource) kaynaktan `PSDesiredStateConfiguration` yerleşik DSC kaynakları modülü.</span><span class="sxs-lookup"><span data-stu-id="3960f-126">This example uses a [Group](https://msdn.microsoft.com/en-us/powershell/dsc/groupresource) resource from the `PSDesiredStateConfiguration` built-in DSC resource module.</span></span>
<span data-ttu-id="3960f-127">Onu yerel gruplar oluşturabilir ve ekleyebilir veya üyeleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="3960f-127">It can create local groups and add or remove members.</span></span>
<span data-ttu-id="3960f-128">Her ikisini de kabul `Credential` özelliği ve otomatik `PsDscRunAsCredential` özelliği.</span><span class="sxs-lookup"><span data-stu-id="3960f-128">It accepts both the `Credential` property and the automatic `PsDscRunAsCredential` property.</span></span>
<span data-ttu-id="3960f-129">Ancak, kaynak yalnızca kullanır `Credential` özelliği.</span><span class="sxs-lookup"><span data-stu-id="3960f-129">However, the resource only uses the `Credential` property.</span></span>

<span data-ttu-id="3960f-130">Hakkında daha fazla bilgi için `PsDscRunAsCredential` özelliği, bkz: [çalıştıran DSC kullanıcı kimlik bilgileriyle](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="3960f-130">For more information about the `PsDscRunAsCredential` property, see [Running DSC with user credentials](runAsUser.md).</span></span>

## <a name="example-the-group-resource-credential-property"></a><span data-ttu-id="3960f-131">Örnek: Grup Kaynak kimlik bilgisi özelliği</span><span class="sxs-lookup"><span data-stu-id="3960f-131">Example: The Group resource Credential property</span></span>

<span data-ttu-id="3960f-132">DSC çalıştıran altında `Local System`, yerel kullanıcılar ve gruplar değiştirme izni zaten sahiptir.</span><span class="sxs-lookup"><span data-stu-id="3960f-132">DSC runs under `Local System`, so it already has permissions to change local users and groups.</span></span>
<span data-ttu-id="3960f-133">Yerel bir hesap eklenen üyesi ise, hiçbir kimlik bilgisi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="3960f-133">If the member added is a local account, then no credential is necessary.</span></span>
<span data-ttu-id="3960f-134">Varsa `Group` kaynak etki alanı hesabı yerel grubuna ekler, sonra bir kimlik bilgisi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="3960f-134">If the `Group` resource adds a domain account to the local group, then a credential is necessary.</span></span>

<span data-ttu-id="3960f-135">Active Directory anonim sorgularına izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="3960f-135">Anonymous queries to Active Directory are not allowed.</span></span>
<span data-ttu-id="3960f-136">`Credential` Özelliği `Group` kaynak Active Directory'yi sorgulamak için kullanılan etki alanı hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="3960f-136">The `Credential` property of the `Group` resource is the domain account used to query Active Directory.</span></span>
<span data-ttu-id="3960f-137">Çoğu amaç için varsayılan olarak kullanıcılar şunları yapabilir Bunun nedeni bir genel kullanıcı hesabı olabilir *okuma* Active Directory içindeki nesneleri çoğu.</span><span class="sxs-lookup"><span data-stu-id="3960f-137">For most purposes this could be a generic user account, because by default users can *read* most of the objects in Active Directory.</span></span>

## <a name="example-configuration"></a><span data-ttu-id="3960f-138">Örnek yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3960f-138">Example Configuration</span></span>

<span data-ttu-id="3960f-139">Aşağıdaki kod örneği, bir etki alanı kullanıcısı ile yerel bir grup doldurmak için DSC kullanır:</span><span class="sxs-lookup"><span data-stu-id="3960f-139">The following example code uses DSC to populate a local group with a domain user:</span></span>

```powershell
Configuration DomainCredentialExample
{
    param
    (
        [PSCredential] $DomainCredential
    )
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    node localhost
    {
        Group DomainUserToLocalGroup
        {
            GroupName        = 'ApplicationAdmins'
            MembersToInclude = 'contoso\alice'
            Credential       = $DomainCredential
        }
    }
}

$cred = Get-Credential -UserName contoso\genericuser -Message "Password please"
DomainCredentialExample -DomainCredential $cred
```

<span data-ttu-id="3960f-140">Bu kod, bir hata ve uyarı iletisi oluşturur:</span><span class="sxs-lookup"><span data-stu-id="3960f-140">This code generates both an error and warning message:</span></span>

```
ConvertTo-MOFInstance : System.InvalidOperationException error processing
property 'Credential' OF TYPE 'Group': Converting and storing encrypted
passwords as plain text is not recommended. For more information on securing
credentials in MOF file, please refer to MSDN blog:
http://go.microsoft.com/fwlink/?LinkId=393729

At line:11 char:9
+   Group
At line:297 char:16
+     $aliasId = ConvertTo-MOFInstance $keywordName $canonicalizedValue
+                ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Write-Error], InvalidOperationException
    + FullyQualifiedErrorId : FailToProcessProperty,ConvertTo-MOFInstance

WARNING: It is not recommended to use domain credential for node 'localhost'.
In order to suppress the warning, you can add a property named
'PSDscAllowDomainUser' with a value of $true to your DSC configuration data
for node 'localhost'.
```

<span data-ttu-id="3960f-141">Bu örnek iki sorunları vardır:</span><span class="sxs-lookup"><span data-stu-id="3960f-141">This example has two issues:</span></span>
1.  <span data-ttu-id="3960f-142">Düz metin parolalarını önerilmez hata açıklar</span><span class="sxs-lookup"><span data-stu-id="3960f-142">An error explains that plain text passwords are not recommended</span></span>
2.  <span data-ttu-id="3960f-143">Bir uyarı etki alanı kimlik bilgilerini kullanarak karşı öneren</span><span class="sxs-lookup"><span data-stu-id="3960f-143">A warning advises against using a domain credential</span></span>

## <a name="psdscallowplaintextpassword"></a><span data-ttu-id="3960f-144">PsDscAllowPlainTextPassword</span><span class="sxs-lookup"><span data-stu-id="3960f-144">PsDscAllowPlainTextPassword</span></span>

<span data-ttu-id="3960f-145">İlk hata iletisi belgelerine bir URL'ye sahip.</span><span class="sxs-lookup"><span data-stu-id="3960f-145">The first error message has a URL with documentation.</span></span>
<span data-ttu-id="3960f-146">Bu bağlantıyı kullanarak parolaları şifrelemek açıklanmaktadır bir [ConfigurationData](https://msdn.microsoft.com/en-us/powershell/dsc/configdata) yapısı ve bir sertifika.</span><span class="sxs-lookup"><span data-stu-id="3960f-146">This link explains how to encrypt passwords using a [ConfigurationData](https://msdn.microsoft.com/en-us/powershell/dsc/configdata) structure and a certificate.</span></span>
<span data-ttu-id="3960f-147">Sertifikalar ve DSC hakkında daha fazla bilgi için [bu gönderisini okuduğunuzu](http://aka.ms/certs4dsc).</span><span class="sxs-lookup"><span data-stu-id="3960f-147">For more information on certificates and DSC [read this post](http://aka.ms/certs4dsc).</span></span>

<span data-ttu-id="3960f-148">Düz metinli bir parola zorlamak için kaynak gerektiriyor `PsDscAllowPlainTextPassword` yapılandırma verilerinde anahtar sözcüğü bölümünde aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="3960f-148">To force a plain text password, the resource requires the `PsDscAllowPlainTextPassword` keyword in the configuration data section as follows:</span></span>

```powershell
Configuration DomainCredentialExample
{
    param
    (
        [PSCredential] $DomainCredential
    )
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    node localhost
    {
        Group DomainUserToLocalGroup
        {
            GroupName        = 'ApplicationAdmins'
            MembersToInclude = 'contoso\alice'
            Credential       = $DomainCredential
        }
    }
}

$cd = @{
    AllNodes = @(
        @{
            NodeName = 'localhost'
            PSDscAllowPlainTextPassword = $true
        }
    )
}

$cred = Get-Credential -UserName contoso\genericuser -Message "Password please"
DomainCredentialExample -DomainCredential $cred -ConfigurationData $cd
```

><span data-ttu-id="3960f-149">**Not:** `NodeName` yıldız işareti, belirli düğüm adı zorunludur eşit olamaz.</span><span class="sxs-lookup"><span data-stu-id="3960f-149">**Note:** `NodeName` cannot equal asterisk, a specific node name is mandatory.</span></span>

<span data-ttu-id="3960f-150">**Düz metin parolalarını önemli güvenlik riski nedeniyle önlemek için Microsoft önerir.**</span><span class="sxs-lookup"><span data-stu-id="3960f-150">**Microsoft advises to avoid plain text passwords due to the significant security risk.**</span></span>
<span data-ttu-id="3960f-151">Yalnızca (aktarımda, hizmet REST ve düğüm üzerinde bekleyen) şifreli her zaman verilerin depolandığı için bir özel durum Azure Otomasyonu DSC hizmetini kullanırken olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3960f-151">An exception would be when using the Azure Automation DSC service, only because the data is always stored encrypted (in transit, at rest in the service, and at rest on the node).</span></span>

## <a name="domain-credentials"></a><span data-ttu-id="3960f-152">Etki alanı kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="3960f-152">Domain Credentials</span></span>

<span data-ttu-id="3960f-153">Örnek yapılandırma betiği yeniden (ile veya şifreleme olmadan) çalıştıran bir etki alanı hesabı bir kimlik bilgisi için önerilmez uyarı hala oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3960f-153">Running the example configuration script again (with or without encryption), still generates the warning that using a domain account for a credential is not recommended.</span></span>
<span data-ttu-id="3960f-154">Yerel bir hesap kullanarak diğer sunucularda kullanılabilir etki alanı kimlik bilgileri olası riskini ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="3960f-154">Using a local account eliminates potential exposure of domain credentials that could be used on other servers.</span></span>

<span data-ttu-id="3960f-155">**Kimlik bilgileri ile DSC kaynakları kullanılırken, yerel bir hesap bir etki alanı hesabı mümkün olduğunda tercih edilir.**</span><span class="sxs-lookup"><span data-stu-id="3960f-155">**When using credentials with DSC resources, prefer a local account over a domain account when possible.**</span></span>

<span data-ttu-id="3960f-156">Varsa bir '\' veya ' @' ın `Username` özelliği kimlik bilgisi, daha sonra DSC işlemek, bir etki alanı hesabı olarak.</span><span class="sxs-lookup"><span data-stu-id="3960f-156">If there is a '\' or '@' in the `Username` property of the credential, then DSC will treat it as a domain account.</span></span>
<span data-ttu-id="3960f-157">"Localhost", "127.0.0.1" için bir özel durum yoktur ve ":: 1" kullanıcı adı etki alanı kısmının.</span><span class="sxs-lookup"><span data-stu-id="3960f-157">There is an exception for "localhost", "127.0.0.1", and "::1" in the domain portion of the user name.</span></span>

## <a name="psdscallowdomainuser"></a><span data-ttu-id="3960f-158">PSDscAllowDomainUser</span><span class="sxs-lookup"><span data-stu-id="3960f-158">PSDscAllowDomainUser</span></span>

<span data-ttu-id="3960f-159">DSC içinde `Group` yukarıda, bir Active Directory etki alanı sorgulama kaynak örnek *gerektirir* bir etki alanı hesabı.</span><span class="sxs-lookup"><span data-stu-id="3960f-159">In the DSC `Group` resource example above, querying an Active Directory domain *requires* a domain account.</span></span>
<span data-ttu-id="3960f-160">Bu durumda eklemek `PSDscAllowDomainUser` özelliğine `ConfigurationData` gibi engelle:</span><span class="sxs-lookup"><span data-stu-id="3960f-160">In this case add the `PSDscAllowDomainUser` property to the `ConfigurationData` block as follows:</span></span>

```powershell
$cd = @{
    AllNodes = @(
        @{
            NodeName = 'localhost'
            PSDscAllowDomainUser = $true
            # PSDscAllowPlainTextPassword = $true
            CertificateFile = "C:\PublicKeys\server1.cer"
        }
    )
}
```

<span data-ttu-id="3960f-161">Artık yapılandırma komut dosyası hata veya uyarı ile MOF dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3960f-161">Now the configuration script will generate the MOF file with no errors or warnings.</span></span>