---
UID: NE:appmodel.PackagePathType
title: PackagePathType
description: Indicates the type of package folder to retrieve.
helpviewer_keywords: ["PackagePathType"]
tech.root: appxpkg
ms.date: 10/06/2025
ms.keywords: PackagePathType
req.construct-type: enumeration
req.ddi-compliance: 
req.header: appmodel.h
req.include-header: 
req.kmdf-ver: 
req.max-support: 
req.target-min-winverclnt: Windows 10 [desktop apps only]
req.target-min-winversvr: Windows Server 2016 [desktop apps only]
req.target-type: Windows
req.lib: Kernel32.lib
req.dll: Kernel32.dll
req.typenames: 
req.umdf-ver: 
targetos: Windows
ms.custom: 19H1
f1_keywords:
 - PackagePathType
 - appmodel/PackagePathType
dev_langs:
 - c++
topic_type:
 - apiref
api_type:
 - HeaderDef
api_location:
 - appmodel.h
api_name:
 - PackagePathType
---

## -description

Indicates the type of folder path to retrieve in a query for the path or other info about a package.

## -enum-fields

### -field PackagePathType_Install

Retrieve the package path in the original install folder for the application.

### -field PackagePathType_Mutable

Retrieve the package path in the mutable install folder for the application, if the application is declared as mutable in the package manifest.

### -field PackagePathType_Effective

Specifies that the package path should be retrieved according to the following logic:

* If the package has a User-External location, then return that path.
* Otherwise, if the package has a Machine-External location, then return that path.
* Otherwise, if the package has a [Mutable location](/uwp/schemas/appxpackage/uapmanifestschema/element-desktop8-mutablepackagedirectories), then return the Mutable path. Also see [Create a directory in any location based on packaged app directory](/windows/msix/manage/create-directory).
* Otherwise, return an error.

### -field PackagePathType_MachineExternal

Specifies that the package path should be retrieved according to the following logic:

* If the package has a Machine-External location, then return that path.
* Otherwise, return an error.

### -field PackagePathType_UserExternal

Specifies that the package path should be retrieved according to the following logic:

* If the package has a User-External location, then return that path.
* Otherwise, return an error.

### -field PackagePathType_EffectiveExternal

Specifies that the package path should be retrieved according to the following logic:

* If the package has a User-External location, then return that path.
* Otherwise, if the package has a Machine-External location, then return that path.
* Otherwise, return an error.

## -remarks

An application has a mutable install folder if it uses the [windows.mutablePackageDirectories extension](/uwp/schemas/appxpackage/uapmanifestschema/element-desktop6-package-extension) in its package manifest. This extension specifies a folder under the %ProgramFiles%\ModifiableWindowsApps path where the contents of the application's install folder are projected so that users can modify the installation files. This feature is currently available only for certain types of desktop PC games that are published by Microsoft and our partners, and it enables these types of games to support mods.

A package always has an Install location, and it can also have a Mutable or an External location, or even both. The concept of "effective" is the location that has the highest precedence for the package/user.

## -see-also

[GetCurrentPackageInfo2](nf-appmodel-getcurrentpackageinfo2.md)


[GetCurrentPackagePath2](nf-appmodel-getcurrentpackagepath2.md)


[GetPackagePathByFullName2](nf-appmodel-getpackagepathbyfullname2.md)


[GetPackageInfo2](nf-appmodel-getpackageinfo2.md)


[GetStagedPackagePathByFullName2](nf-appmodel-getstagedpackagepathbyfullname2.md)
