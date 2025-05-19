---
UID: NF:ncrypt.NCryptVerifySignature
title: NCryptVerifySignature function (ncrypt.h)
description: Verifies that the specified signature matches the specified hash. (NCryptVerifySignature)
helpviewer_keywords: ["NCRYPT_PAD_PKCS1_FLAG","NCRYPT_PAD_PSS_FLAG","NCRYPT_SILENT_FLAG","NCryptVerifySignature","NCryptVerifySignature function [Security]","ncrypt/NCryptVerifySignature","security.ncryptverifysignature_func"]
old-location: security\ncryptverifysignature_func.htm
tech.root: security
ms.assetid: 9a839d99-4e9a-4114-982c-51dee38d2949
ms.date: 05/15/2025
ms.keywords: NCRYPT_PAD_PKCS1_FLAG, NCRYPT_PAD_PSS_FLAG, NCRYPT_SILENT_FLAG, NCryptVerifySignature, NCryptVerifySignature function [Security], ncrypt/NCryptVerifySignature, security.ncryptverifysignature_func
req.header: ncrypt.h
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
req.lib: Ncrypt.lib
req.dll: Ncrypt.dll
req.irql: 
targetos: Windows
req.typenames: 
req.redist: 
ms.custom: 19H1
f1_keywords:
 - NCryptVerifySignature
 - ncrypt/NCryptVerifySignature
dev_langs:
 - c++
topic_type:
 - APIRef
 - kbSyntax
api_type:
 - DllExport
api_location:
 - Ncrypt.dll
api_name:
 - NCryptVerifySignature
---

# NCryptVerifySignature function

## -description

The **NCryptVerifySignature** function verifies that the specified signature matches the specified hash.

## -parameters

### -param hKey [in]

The handle of the key to use to decrypt the signature. This must be an identical key or the public key portion of the key pair used to sign the data with the [NCryptSignHash](nf-ncrypt-ncryptsignhash.md) function.

### -param pPaddingInfo [in, optional]

A pointer to a structure that contains padding information. The actual type of structure this parameter points to depends on the value of the *dwFlags* parameter. This parameter is only used with asymmetric keys and must be `NULL` otherwise.

### -param pbHashValue [in]

The address of a buffer that contains the hash of the data. The *cbHash* parameter contains the size of this buffer.

### -param cbHashValue [in]

The size, in bytes, of the *pbHash* buffer.

### -param pbSignature [in]

The address of a buffer that contains the signed hash of the data. The [NCryptSignHash](nf-ncrypt-ncryptsignhash.md) function is used to create the signature. The *cbSignature* parameter contains the size of this buffer.

### -param cbSignature [in]

The size, in bytes, of the *pbSignature* buffer. The [NCryptSignHash](nf-ncrypt-ncryptsignhash.md) function is used to create the signature.

### -param dwFlags [in]

Flags that modify function behavior. The allowed set of flags depends on the type of key specified by the *hKey* parameter.

If the key is a symmetric key, this parameter is not used and should be zero.

If the key is an asymmetric key, this can be one of the following values:

| Value | Meaning |
|-------|---------|
| **NCRYPT_PAD_PKCS1_FLAG** | The PKCS1 padding scheme was used when the signature was created. The *pPaddingInfo* parameter is a pointer to a [BCRYPT_PKCS1_PADDING_INFO](../bcrypt/ns-bcrypt-bcrypt_pkcs1_padding_info.md) structure. |
| **BCRYPT_PAD_PQDSA** | Use the PQ padding scheme for ML-DSA or SLH-DSA. The *pPaddingInfo* parameter is a pointer to a [BCRYPT_PQDSA_PADDING_INFO](/windows/win32/seccng/bcrypt/ns-bcrypt-bcrypt_pqdsa_padding_info) structure.<br/><br/>**Note:** This must be set if using a pre-hash ML-DSA variant. |
| **NCRYPT_PAD_PSS_FLAG** | The Probabilistic Signature Scheme (PSS) padding scheme was used when the signature was created. The *pPaddingInfo* parameter is a pointer to a [BCRYPT_PSS_PADDING_INFO](../bcrypt/ns-bcrypt-bcrypt_pss_padding_info.md) structure. |
| **NCRYPT_SILENT_FLAG** | Requests that the key service provider (KSP) not display any user interface. If the provider must display the UI to operate, the call fails and the KSP should set the **NTE_SILENT_CONTEXT** error code as the last error. |

## -returns

Returns a status code that indicates the success or failure of the function.

Possible return codes include, but are not limited to, the following:

| Return code | Description |
|-------------|-------------|
| **ERROR_SUCCESS** | The function was successful. |
| **NTE_BAD_SIGNATURE** | The signature was not verified. |
| **NTE_INVALID_HANDLE** | The *hKey* parameter is not valid. |
| **NTE_NO_MEMORY** | A memory allocation failure occurred. |
| **NTE_NOT_SUPPORTED** | The algorithm provider used to create the key handle specified by the *hKey* parameter is not a signing algorithm. |

## -remarks

A service must not call this function from its [StartService Function](../winsvc/nf-winsvc-startservicea.md). If a service calls this function from its **StartService** function, a deadlock can occur, and the service may stop responding.

## -see-also

[NCryptSignHash](nf-ncrypt-ncryptsignhash.md)
