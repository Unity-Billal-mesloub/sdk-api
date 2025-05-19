---
UID: NF:bcrypt.BCryptVerifySignature
title: BCryptVerifySignature function (bcrypt.h)
description: Verifies that the specified signature matches the specified hash. (BCryptVerifySignature)
helpviewer_keywords: ["BCRYPT_PAD_PKCS1","BCRYPT_PAD_PSS","BCryptVerifySignature","BCryptVerifySignature function [Security]","bcrypt/BCryptVerifySignature","security.bcryptverifysignature_func"]
old-location: security\bcryptverifysignature_func.htm
tech.root: security
ms.assetid: 95c32056-e444-441c-bbc1-c5ae82aba964
ms.date: 05/14/2025
ms.keywords: BCRYPT_PAD_PKCS1, BCRYPT_PAD_PSS, BCryptVerifySignature, BCryptVerifySignature function [Security], bcrypt/BCryptVerifySignature, security.bcryptverifysignature_func
req.header: bcrypt.h
req.include-header: 
req.target-type: Windows
req.target-min-winverclnt: Windows Vista [desktop apps \| UWP apps]
req.target-min-winversvr: Windows Server 2008 [desktop apps \| UWP apps]
req.kmdf-ver: 
req.umdf-ver: 
req.ddi-compliance: 
req.unicode-ansi: 
req.idl: 
req.max-support: 
req.namespace: 
req.assembly: 
req.type-library: 
req.lib: Bcrypt.lib
req.dll: Bcrypt.dll
req.irql: 
targetos: Windows
req.typenames: 
req.redist: 
ms.custom: 19H1
f1_keywords:
 - BCryptVerifySignature
 - bcrypt/BCryptVerifySignature
dev_langs:
 - c++
topic_type:
 - APIRef
 - kbSyntax
api_type:
 - DllExport
api_location:
 - Bcrypt.dll
 - Ksecdd.sys
api_name:
 - BCryptVerifySignature
---

# BCryptVerifySignature function

## -description

The **BCryptVerifySignature** function verifies that the specified signature matches the specified hash.

## -parameters

### -param hKey [in]

The handle of the key to use to decrypt the signature. This must be an identical key or the public key portion of the key pair used to sign the data with the [BCryptSignHash](nf-bcrypt-bcryptsignhash.md) function.

### -param pPaddingInfo [in, optional]

A pointer to a structure that contains padding information. The actual type of structure this parameter points to depends on the value of the *dwFlags* parameter. This parameter is only used with asymmetric keys and must be `NULL` otherwise.

*pPaddingInfo* must be `NULL` for LMS and XMSS since no additional information is required to generate a signature other than the key and the input.

### -param pbHash [in]

The address of a buffer that contains the hash of the data. The *cbHash* parameter contains the size of this buffer.

### -param cbHash [in]

The size, in bytes, of the *pbHash* buffer.

### -param pbSignature [in]

The address of a buffer that contains the signed hash of the data. The [BCryptSignHash](nf-bcrypt-bcryptsignhash.md) function is used to create the signature. The *cbSignature* parameter contains the size of this buffer.

### -param cbSignature [in]

The size, in bytes, of the *pbSignature* buffer. The [BCryptSignHash](nf-bcrypt-bcryptsignhash.md) function is used to create the signature.

### -param dwFlags [in]

A set of flags that modify the behavior of this function. The allowed set of flags depends on the type of key specified by the *hKey* parameter.

*dwFlags* must be zero for LMS and XMSS since no additional information is required to generate a signature other than the key and the input.

If the key is a symmetric key, this parameter is not used and should be zero.

If the key is an asymmetric key, this can be one of the following values:

| Value | Meaning |
|-------|---------|
| **BCRYPT_PAD_PKCS1** | The PKCS1 padding scheme was used when the signature was created. The *pPaddingInfo* parameter is a pointer to a [BCRYPT_PKCS1_PADDING_INFO](ns-bcrypt-bcrypt_pkcs1_padding_info.md) structure. |
| **BCRYPT_PAD_PQDSA** | Use the PQ padding scheme for ML-DSA or SLH-DSA. The *pPaddingInfo* parameter is a pointer to a [BCRYPT_PQDSA_PADDING_INFO](/windows/win32/seccng/bcrypt/ns-bcrypt-bcrypt_pqdsa_padding_info) structure.<br/><br/>**Note:** This must be set if using a pre-hash ML-DSA variant. |
| **BCRYPT_PAD_PSS** | The Probabilistic Signature Scheme (PSS) padding scheme was used when the signature was created. The *pPaddingInfo* parameter is a pointer to a [BCRYPT_PSS_PADDING_INFO](ns-bcrypt-bcrypt_pss_padding_info.md) structure. |

## -returns

Returns a status code that indicates the success or failure of the function.

Possible return codes include, but are not limited to, the following:

| Return code | Description |
|-------------|-------------|
| **STATUS_SUCCESS** | The function was successful. |
| **STATUS_INVALID_SIGNATURE** | The signature was not verified. |
| **NTE_NO_MEMORY** | A memory allocation failure occurred. |
| **STATUS_INVALID_PARAMETER** | One of the supplied parameters is invalid. |
| **STATUS_INVALID_HANDLE** | The key handle specified by the *hKey* parameter is not valid. |
| **STATUS_NOT_SUPPORTED** | The algorithm provider used to create the key handle specified by the *hKey* parameter is not a signing algorithm. |

## -remarks

This function calculates the signature with provided key and then compares calculated signature value to the specified signature value.

To use this function, you must hash the data by using the same hashing algorithm that was used to create the hash value that was signed. If applicable, you must also specify the same padding scheme that was specified when the signature was created.

For ML-DSA and SLH-DSA, *pbHash* and *cbHash* do not have to be hash values and can be arbitrary length input. 

Depending on what processor modes a provider supports, **BCryptVerifySignature** can be called either from user mode or kernel mode. Kernel mode callers can execute either at **PASSIVE_LEVEL** [IRQL](/windows/win32/SecGloss/i-gly) or **DISPATCH_LEVEL** IRQL. If the current IRQL level is **DISPATCH_LEVEL**, the handle provided in the *hKey* parameter must be derived from an algorithm handle returned by a provider that was opened by using the **BCRYPT_PROV_DISPATCH** flag, and any pointers passed to the **BCryptVerifySignature** function must refer to nonpaged (or locked) memory.

To call this function in kernel mode, use `Cng.lib`, which is part of the Driver Development Kit (DDK). **Windows Server 2008 and Windows Vista:** To call this function in kernel mode, use `Ksecdd.lib`.

## -see-also

[BCryptSignHash](nf-bcrypt-bcryptsignhash.md)
