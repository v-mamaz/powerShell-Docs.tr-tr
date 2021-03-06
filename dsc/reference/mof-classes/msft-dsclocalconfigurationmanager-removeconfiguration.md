---
ms.date: 06/12/2017
keywords: DSC, powershell, yapılandırma, Kurulum
title: MSFT_DSCLocalConfigurationManager sınıfının RemoveConfiguration yöntemi
ms.openlocfilehash: 03555cc73da1272bdebebc3d93b26aaf8fabc18e
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048703"
---
# <a name="removeconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>MSFT_DSCLocalConfigurationManager sınıfının RemoveConfiguration yöntemi

Yapılandırma dosyaları kaldırır.

## <a name="syntax"></a>Sözdizimi

```mof
uint32 RemoveConfiguration(
  [in] uint32  Stage,
  [in] boolean Force
);
```

## <a name="parameters"></a>Parametreler

*Aşama* \[içinde\] kaldırmak için hangi yapılandırma belgesini belirtir. Aşağıdaki değerler geçerlidir:

|Değer |Açıklama |
|:--- |:---|
|**1** | **Geçerli** yapılandırma belgesi (current.mof). |
|**2** | **Bekleyen** yapılandırma belgesi (pending.mof).  |
|**4** | **Önceki** yapılandırma belgesi (previous.mof). |

*Zorla* \[içinde\] **true** yapılandırma kaldırılmasını zorlamak için.

## <a name="return-value"></a>Dönüş değeri

Başarılıysa sıfır döndürür; Aksi takdirde bir hata kodu döndürür.

## <a name="remarks"></a>Açıklamalar

Statik bir yöntem budur.

## <a name="requirements"></a>Gereksinimler

**MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>Ayrıca bkz:

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)