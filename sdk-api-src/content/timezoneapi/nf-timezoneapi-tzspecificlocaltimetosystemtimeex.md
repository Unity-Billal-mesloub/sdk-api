---
UID: NF:timezoneapi.TzSpecificLocalTimeToSystemTimeEx
title: TzSpecificLocalTimeToSystemTimeEx function (timezoneapi.h)
description: Converts a local time to a time with dynamic daylight saving time settings to Coordinated Universal Time (UTC).
helpviewer_keywords: ["TzSpecificLocalTimeToSystemTimeEx","TzSpecificLocalTimeToSystemTimeEx function","base.tzspecificlocaltimetosystemtimeex","timezoneapi/TzSpecificLocalTimeToSystemTimeEx"]
old-location: base\tzspecificlocaltimetosystemtimeex.htm
tech.root: winprog
ms.assetid: C202F91E-FFFF-412D-A968-3B7AE60A5846
ms.date: 12/16/2025
ms.keywords: TzSpecificLocalTimeToSystemTimeEx, TzSpecificLocalTimeToSystemTimeEx function, base.tzspecificlocaltimetosystemtimeex, timezoneapi/TzSpecificLocalTimeToSystemTimeEx
req.header: timezoneapi.h
req.include-header: Windows.h
req.target-type: Windows
req.target-min-winverclnt: Windows 7 [desktop apps \| UWP apps]
req.target-min-winversvr: Windows Server 2012 [desktop apps \| UWP apps]
req.kmdf-ver:
req.umdf-ver:
req.ddi-compliance:
req.unicode-ansi:
req.idl:
req.max-support:
req.namespace:
req.assembly:
req.type-library:
req.lib: Kernel32.lib
req.dll: Kernel32.dll
req.irql:
targetos: Windows
req.typenames:
req.redist:
ms.custom: 19H1
f1_keywords:
 - TzSpecificLocalTimeToSystemTimeEx
 - timezoneapi/TzSpecificLocalTimeToSystemTimeEx
dev_langs:
 - c++
topic_type:
 - APIRef
 - kbSyntax
api_type:
 - DllExport
api_location:
 - Kernel32.dll
 - API-MS-Win-Core-TimeZone-l1-1-0.dll
 - KernelBase.dll
 - MinKernelBase.dll
api_name:
 - TzSpecificLocalTimeToSystemTimeEx
---

# TzSpecificLocalTimeToSystemTimeEx function


## -description

Converts the local time in the specified time zone (with dynamic daylight saving time settings) to a corresponding Coordinated Universal Time (UTC).

## -parameters

### -param lpTimeZoneInformation [in, optional]

A pointer to a <a href="/windows/desktop/api/timezoneapi/ns-timezoneapi-dynamic_time_zone_information">DYNAMIC_TIME_ZONE_INFORMATION</a> structure that specifies the time zone and dynamic daylight saving time settings.

If <i>lpTimeZoneInformation</i> is <b>NULL</b>, the function uses the currently active time zone.

### -param lpLocalTime [in]

A pointer to a <a href="/windows/desktop/api/minwinbase/ns-minwinbase-systemtime">SYSTEMTIME</a> structure that specifies the local time to be converted. The function converts this time to the corresponding UTC time.

### -param lpUniversalTime [out]

A pointer to a <a href="/windows/desktop/api/minwinbase/ns-minwinbase-systemtime">SYSTEMTIME</a> structure that receives the UTC time.

## -returns

If the function succeeds, the return value is nonzero, and the function sets the members of the <a href="/windows/desktop/api/minwinbase/ns-minwinbase-systemtime">SYSTEMTIME</a> structure pointed to by <i>lpUniversalTime</i> to the appropriate values.

If the function fails, the return value is zero. To get extended error information, call <a href="/windows/desktop/api/errhandlingapi/nf-errhandlingapi-getlasterror">GetLastError</a>.

## -remarks

<b>TzSpecificLocalTimeToSystemTimeEx</b> takes into account whether daylight saving time (DST) is in effect for the local time to be converted.

> [!IMPORTANT]
> The following local times, near DST transitions, can be <b>ambiguous</b> or <b>invalid</b> and might result in unexpected behavior (as there is no guaranteed "correct" result).
> - During the transition from daylight time to standard time, the local clock repeats. A local time within the repeated window is <b>ambiguous</b> because it occurs twice, once in daylight time and once in standard time.
> - During the transition from standard time to daylight time, the local clock jumps forward. A local time within the skipped window is <b>invalid</b> because it does not have a valid UTC conversion.
>
> If the specified local time is either ambiguous or invalid, the function treats it as <b>daylight time</b> and applies the daylight time bias. Applications requiring continuity or precision should avoid this function and use UTC time instead.

## -see-also
