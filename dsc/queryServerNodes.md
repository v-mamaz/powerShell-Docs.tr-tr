---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC, powershell, yapılandırma, Kur"
title: "Sorgu düğümü bilgileri işleve DSC çekme sunucusundan."
ms.openlocfilehash: 307fd46f113797c75c6ad2211ec86af30104de36
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-function-to-query-node-information-from-pull-server"></a><span data-ttu-id="9f1a1-103">Sorgu düğümü bilgileri işleve DSC çekme sunucusundan.</span><span class="sxs-lookup"><span data-stu-id="9f1a1-103">DSC function to query node information from pull server.</span></span>

```powershell
function QueryNodeInformation
{
Param (      
       [string] $Uri =
"http://localhost:7070/PSDSCComplianceServer.svc/Status",                         
       [string] $ContentType = "application/json"           
     )

  Write-Host "Querying node information from pull server URI  = $Uri" -ForegroundColor Green

  Write-Host "Querying node status in content type  = $ContentType " -ForegroundColor Green

   $response = Invoke-WebRequest -Uri $Uri -Method Get -ContentType $ContentType -UseDefaultCredentials -Headers 
    @{Accept = $ContentType}

   if($response.StatusCode -ne 200)
 {
     Write-Host "node information was not retrieved." -ForegroundColor Red
 }

 $jsonResponse = ConvertFrom-Json $response.Content

  return $jsonResponse
}
```

<span data-ttu-id="9f1a1-104">Değiştir `Uri` çekme sunucunuz için URI parametresiyle.</span><span class="sxs-lookup"><span data-stu-id="9f1a1-104">Replace the `Uri` parameter with the URI for your pull server.</span></span> <span data-ttu-id="9f1a1-105">Düğüm bilgilerini XML biçiminde istiyorsanız ayarlayın `ContentType` için `application/xml`.</span><span class="sxs-lookup"><span data-stu-id="9f1a1-105">If you want the node information in XML format, set `ContentType` to `application/xml`.</span></span>

<span data-ttu-id="9f1a1-106">Düğüm bilgi almaya `$json` parametresi için aşağıdakini kullanın:</span><span class="sxs-lookup"><span data-stu-id="9f1a1-106">To retrieve the node information from the `$json` parameter, use the following:</span></span>

```powershell
$json = QueryNodeInformation –Uri http://localhost:7070/PSDSCComplianceServer.svc/Status 

$json.value | Format-Table TargetName, ConfigurationId, ServerChecksum, NodeCompliant, LastComplianceTime, StatusCode
```
