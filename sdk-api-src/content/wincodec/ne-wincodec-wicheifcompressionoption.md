---
UID: NE:wincodec.WICHeifCompressionOption
title: WICHeifCompressionOption
description: Defines constants that specify High Efficiency Image Format (HEIF) compression options.
ms.date: 07/14/2025
tech.root: wic
targetos: Windows
prerelease: true
req.construct-type: enumeration
req.ddi-compliance: 
req.header: wincodec.h
req.include-header: 
req.kmdf-ver: 
req.max-support: 
req.target-min-winverclnt: 
req.target-min-winversvr: 
req.target-type: 
req.typenames: 
typedef_isUnnamed: false
req.umdf-ver: 
topic_type:
 - apiref
api_type:
 - HeaderDef
api_location:
 - wincodec.h
api_name:
 - WICHeifCompressionOption
f1_keywords:
 - WICHeifCompressionOption
 - wincodec/WICHeifCompressionOption
dev_langs:
 - c++
helpviewer_keywords:
 - WICHeifCompressionOption
---

## -description

Defines constants that specify High Efficiency Image Format (HEIF) compression options. Allows you to choose which compression format to use when creating a HEIF image file.

## -enum-fields

### -field WICHeifCompressionDontCare:0x0

Specifies that any compression option may be used.

### -field WICHeifCompressionNone:0x1

Specifies that no compression be used.

### -field WICHeifCompressionHEVC:0x2

Specifies that High Efficiency Video Coding (HEVC) compression be used.

### -field WICHeifCompressionAV1:0x3

Specifies that AOMedia Video 1 (AV1) compression be used.

### -field WICHeifCompressionJpegXL:0x4

TBD

### -field WICHeifCompressionBrotli:0x5

TBD

### -field WICHeifCompressionDeflate:0x6

TBD

### -field WICHEIFCOMPRESSIONOPTION_FORCE_DWORD

## -remarks

## -see-also
