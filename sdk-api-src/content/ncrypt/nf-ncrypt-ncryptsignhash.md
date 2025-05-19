---
UID: NF:ncrypt.NCryptSignHash
title: NCryptSignHash function (ncrypt.h)
description: Creates a signature of a hash value. (NCryptSignHash)
helpviewer_keywords: ["BCRYPT_PAD_PKCS1","BCRYPT_PAD_PSS","NCRYPT_SILENT_FLAG","NCryptSignHash","NCryptSignHash function [Security]","ncrypt/NCryptSignHash","security.ncryptsignhash_func"]
old-location: security\ncryptsignhash_func.htm
tech.root: security
ms.assetid: 7404e37a-d7c6-49ed-b951-6081dd2b921a
ms.date: 05/15/2025
ms.keywords: BCRYPT_PAD_PKCS1, BCRYPT_PAD_PSS, NCRYPT_SILENT_FLAG, NCryptSignHash, NCryptSignHash function [Security], ncrypt/NCryptSignHash, security.ncryptsignhash_func
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
 - NCryptSignHash
 - ncrypt/NCryptSignHash
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
 - NCryptSignHash
---

# NCryptSignHash function


## -description

The **NCryptSignHash** function creates a signature of a hash value.

## -parameters

### -param hKey [in]

The handle of the key to use to sign the hash.

### -param pPaddingInfo [in, optional]

A pointer to a structure that contains padding information. The actual type of structure this parameter points to depends on the value of the *dwFlags* parameter. This parameter is only used with asymmetric keys and must be `NULL` otherwise.

### -param pbHashValue [in]

A pointer to a buffer that contains the hash value to sign. The *cbInput* parameter contains the size of this buffer.

### -param cbHashValue [in]

The number of bytes in the *pbHashValue* buffer to sign.

### -param pbSignature [out]

The address of a buffer to receive the signature produced by this function. The *cbSignature* parameter contains the size of this buffer.

If this parameter is `NULL`, this function will calculate the size required for the signature and return the size in the location pointed to by the *pcbResult* parameter.

### -param cbSignature [in]

The size, in bytes, of the *pbSignature* buffer. This parameter is ignored if the *pbSignature* parameter is `NULL`.

### -param pcbResult [out]

A pointer to a **DWORD** variable that receives the number of bytes copied to the *pbSignature* buffer. 

If *pbSignature* is `NULL`, this receives the size, in bytes, required for the signature.

### -param dwFlags [in]

Flags that modify function behavior. The allowed set of flags depends on the type of key specified by the *hKey* parameter.

If the key is a symmetric key, this parameter is not used and should be set to zero.

If the key is an asymmetric key, this can be one of the following values:

| Value | Meaning |
|-------|---------|
| **BCRYPT_PAD_PKCS1** | Use the PKCS1 padding scheme. The *pPaddingInfo* parameter is a pointer to a [BCRYPT_PKCS1_PADDING_INFO](../bcrypt/ns-bcrypt-bcrypt_pkcs1_padding_info.md) structure. |
| **BCRYPT_PAD_PQDSA** | Use the PQ padding scheme for ML-DSA or SLH-DSA. The *pPaddingInfo* parameter is a pointer to a [BCRYPT_PQDSA_PADDING_INFO](/windows/win32/seccng/bcrypt/ns-bcrypt-bcrypt_pqdsa_padding_info) structure.<br/><br/>**Note:** This must be set if using a pre-hash ML-DSA variant. |
| **BCRYPT_PAD_PSS** | Use the Probabilistic Signature Scheme (PSS) padding scheme. The *pPaddingInfo* parameter is a pointer to a [BCRYPT_PSS_PADDING_INFO](../bcrypt/ns-bcrypt-bcrypt_pss_padding_info.md) structure. |
| **NCRYPT_SILENT_FLAG** | Requests that the key service provider (KSP) not display any user interface. If the provider must display the UI to operate, the call fails and the KSP should set the **NTE_SILENT_CONTEXT** error code as the last error. |

## -returns

Returns a status code that indicates the success or failure of the function.

Possible return codes include, but are not limited to, the following:

| Return code | Description |
|-------------|-------------|
| **ERROR_SUCCESS** | The function was successful. |
| **NTE_BAD_ALGID** | The key represented by the *hKey* parameter does not support signing. |
| **NTE_BAD_FLAGS** | The *dwFlags* parameter contains a value that is not valid. |
| **NTE_INVALID_HANDLE** | The *hKey* parameter is not valid. |
| **NTE_INVALID_PARAMETER** | One or more parameters are not valid. |
| **NTE_NO_MEMORY** | A memory allocation failure occurred. |

## -remarks

A service must not call this function from its [StartService Function](../winsvc/nf-winsvc-startservicea.md). If a service calls this function from its **StartService** function, a deadlock can occur, and the service may stop responding.
