---
ms.date: 06/12/2017
keywords: DSC, powershell, yapılandırma, Kurulum
title: MSFT_DSCLocalConfigurationManager sınıfının ApplyConfiguration yöntemi
ms.openlocfilehash: 559ff1793a18e28dad2f176bdb20eb53bc08630d
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048623"
---
# <a name="applyconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>MSFT_DSCLocalConfigurationManager sınıfının ApplyConfiguration yöntemi

Yapılandırma Aracı, bekleyen yapılandırmayı uygulamak için kullanır.

Bekleyen herhangi bir yapılandırma varsa, bu yöntem geçerli yapılandırmasını yeniden uygular.

## <a name="syntax"></a>Sözdizimi

```mof
uint32 ApplyConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a>Parametreler

*zorla* \[içinde\] buysa **true**, bekleyen bir yapılandırma olsa bile geçerli yapılandırmasını yeniden uygulanır.

## <a name="return-value"></a>Dönüş değeri

Başarılıysa sıfır döndürür; Aksi takdirde bir hata kodu döndürür.

## <a name="remarks"></a>Açıklamalar

Statik bir yöntem budur.

## <a name="requirements"></a>Gereksinimler

**MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>Ayrıca bkz:

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)