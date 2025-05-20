---
UID: NF:bcrypt.BCryptSignHash
title: BCryptSignHash function (bcrypt.h)
description: Creates a signature of a hash value. (BCryptSignHash)
helpviewer_keywords: ["BCRYPT_PAD_PKCS1","BCRYPT_PAD_PSS","BCryptSignHash","BCryptSignHash function [Security]","bcrypt/BCryptSignHash","security.bcryptsignhash_func"]
old-location: security\bcryptsignhash_func.htm
tech.root: security
ms.assetid: f402ea9e-89ae-4ccc-9591-aa2328287c0e
ms.date: 05/14/2025
ms.keywords: BCRYPT_PAD_PKCS1, BCRYPT_PAD_PSS, BCryptSignHash, BCryptSignHash function [Security], bcrypt/BCryptSignHash, security.bcryptsignhash_func
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
 - BCryptSignHash
 - bcrypt/BCryptSignHash
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
 - BCryptSignHash
---

# BCryptSignHash function


## -description

The **BCryptSignHash** function creates a signature of a hash value.

## -parameters

### -param hKey [in]

The handle of the key to use to sign the hash.

### -param pPaddingInfo [in, optional]

A pointer to a structure that contains padding information. The actual type of structure this parameter points to depends on the value of the *dwFlags* parameter. This parameter is only used with asymmetric keys and must be `NULL` otherwise.

*pPaddingInfo* must be `NULL` for LMS and XMSS since no additional information is required to generate a signature other than the key and the input.

### -param pbInput [in]

A pointer to a buffer that contains the hash value to sign. The *cbInput* parameter contains the size of this buffer.

### -param cbInput [in]

The number of bytes in the *pbInput* buffer to sign.

### -param pbOutput [out]

The address of a buffer to receive the signature produced by this function. The *cbOutput* parameter contains the size of this buffer.

If this parameter is `NULL`, this function will calculate the size required for the signature and return the size in the location pointed to by the *pcbResult* parameter.

### -param cbOutput [in]

The size, in bytes, of the *pbOutput* buffer. This parameter is ignored if the *pbOutput* parameter is `NULL`.

### -param pcbResult [out]

A pointer to a **ULONG** variable that receives the number of bytes copied to the *pbOutput* buffer. 

If *pbOutput* is `NULL`, this receives the size, in bytes, required for the signature.

### -param dwFlags [in]

A set of flags that modify the behavior of this function. The allowed set of flags depends on the type of key specified by the *hKey* parameter.

*dwFlags* must be zero for LMS and XMSS since no additional information is required to generate a signature other than the key and the input.

This can be one of the following values:

| Value | Meaning |
|-------|---------|
| **BCRYPT_PAD_PKCS1** | Use the PKCS1 padding scheme. The *pPaddingInfo* parameter is a pointer to a [BCRYPT_PKCS1_PADDING_INFO](ns-bcrypt-bcrypt_pkcs1_padding_info.md) structure. |
| **BCRYPT_PAD_PQDSA** | Use the PQ padding scheme for ML-DSA or SLH-DSA. The *pPaddingInfo* parameter is a pointer to a [BCRYPT_PQDSA_PADDING_INFO](/windows/win32/seccng/bcrypt/ns-bcrypt-bcrypt_pqdsa_padding_info) structure.<br/><br/>**Note:** This must be set if using a pre-hash ML-DSA variant. |
| **BCRYPT_PAD_PSS** | Use the Probabilistic Signature Scheme (PSS) padding scheme. The *pPaddingInfo* parameter is a pointer to a [BCRYPT_PSS_PADDING_INFO](ns-bcrypt-bcrypt_pss_padding_info.md) structure. |

## -returns

Returns a status code that indicates the success or failure of the function.

Possible return codes include, but are not limited to, the following:

| Return code | Description |
|-------------|-------------|
| **STATUS_SUCCESS** | The function was successful. |
| **STATUS_INVALID_HANDLE** | The key handle specified by the *hKey* parameter is not valid. |
| **STATUS_NOT_SUPPORTED** | The algorithm provider used to create the key handle specified by the *hKey* parameter is not a signing algorithm. |
| **STATUS_NO_MEMORY** | A memory allocation failure occurred. |
| **STATUS_BUFFER_TOO_SMALL** | The memory size specified by the *cbOutput* parameter is not large enough to hold the signature. |

## -remarks

This function will encrypt the hash value with the specified key to create the signature.

To later verify that the signature is valid, call the [BCryptVerifySignature](nf-bcrypt-bcryptverifysignature.md) function with an identical key and an identical hash of the original data.

Depending on what processor modes a provider supports, **BCryptSignHash** can be called either from user mode or kernel mode. Kernel mode callers can execute either at **PASSIVE_LEVEL** [IRQL](/windows/win32/SecGloss/i-gly) or **DISPATCH_LEVEL** IRQL. If the current IRQL level is **DISPATCH_LEVEL**, the handle provided in the *hKey* parameter must be derived from an algorithm handle returned by a provider that was opened with the **BCRYPT_PROV_DISPATCH** flag, and any pointers passed to the **BCryptSignHash** function must refer to nonpaged (or locked) memory.

To call this function in kernel mode, use `Cng.lib`, which is part of the Driver Development Kit (DDK). **Windows Server 2008 and Windows Vista:** To call this function in kernel mode, use `Ksecdd.lib`.

## -see-also

[BCryptVerifySignature](nf-bcrypt-bcryptverifysignature.md)
