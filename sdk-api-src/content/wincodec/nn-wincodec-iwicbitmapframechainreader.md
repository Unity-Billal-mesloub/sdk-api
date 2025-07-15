---
UID: NN:wincodec.IWICBitmapFrameChainReader
title: IWICBitmapFrameChainReader
description: Provides access to frames that are linked to the current frame through chains of different types.
ms.date: 07/14/2025
tech.root: wic
targetos: Windows
prerelease: false
req.assembly: 
req.construct-type: iface
req.ddi-compliance: 
req.header: wincodec.h
req.idl: 
req.include-header: 
req.max-support: 
req.namespace: 
req.redist: 
req.target-min-winverclnt: 
req.target-min-winversvr: 
req.target-type: 
req.unicode-ansi: 
topic_type:
 - apiref
api_type:
 - COM
api_location:
 - wincodec.h
api_name:
 - IWICBitmapFrameChainReader
f1_keywords:
 - IWICBitmapFrameChainReader
 - wincodec/IWICBitmapFrameChainReader
dev_langs:
 - c++
helpviewer_keywords:
 - IWICBitmapFrameChainReader
---

## -description

Provides access to frames that are linked to the current frame through chains of different types.

To provide access to subordinate frames, the frame object (which is represented by [IWICBitmapFrameDecode](./nn-wincodec-iwicbitmapframedecode.md)), implements **IWICBitmapFrameChainReader**.

## -remarks

**IWICBitmapFrameChainReader** represents one of a set of COM interfaces that allow WIC to expose chains of linked frames, of different types.

The decoder for an image file can provide multiple frames. Each frame represents a separate image. Similarly, the encoder can accept multiple frames, and encode them into a single file. The typical use case for multiple frames is when scanning a multi-page document into TIFF format. In that scenario, there's no hierarchy of frames (each frame is just as important as another). The newer HEIF image format supports more advanced scenarios, involving secondary frames that are linked to a primary frame. Currently, there's no way to specify such relationships between frames in the WIC API.

The main scenario that this enables is support for HEIF *overlay images*. An overlay image is composed of multiple *layer* images that are stacked on top of each other in a specified order. The overlay image is the primary image, and the layer images are secondary (subordinate) images that are linked to the primary image. The layer images aren't displayed individually by regular photo viewing apps, but there is a use case where an image editing app needs to be able to read and write each individual layer image.

An overlay image requires metadata to describe how to compose the different layers into a single image. WIC API extensions exist for that metadata.

An overlay image often require lossless compression, because that allows image editing apps to open and save a file multiple times without degrading the image quality. WIC currently allows encoders to specify only HEVC and AV1 as compression formats for HEIF image files. Both of those formats are lossy. Additions to the WIC encoding APIs exist that allow HEIF to be used with lossless compression formats such as JPEG XL, and uncompressed formats such as RGBA.

## -see-also
