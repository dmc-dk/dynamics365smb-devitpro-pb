---
title: "The Microsoft_Application.app File"
ms.author: solsen
ms.custom: na
ms.date: 04/01/2020
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.service: "dynamics365-business-central"
author: SusanneWindfeldPedersen
---

# The Microsoft_Application.app File

The Microsoft_Application.app file is included with [!INCLUDE[d365fin_long_md](includes/d365fin_long_md.md)] and is located in the `\Applications\Application\Source` folder. The `Microsoft_Application.app` file logically encapsulates all of the extensions making up a solution, for example, version `16.0.0.0` of the base and system application package files, and it provides a convenient way to define and refer to this solution identity. 

> [!NOTE]  
> In previous versions the references to base and system application were stated explicitly under `dependencies` in the `app.json` file of the extension. For more information, see [JSON Files](devenv-json-files.md).

The file name of the reference is `Microsoft_Application.app` and in the app.json file of the application package file, the name is `Application`. For code-customized base applications that have their own appId, the `Microsoft_Application.app` file can be modified to reference the appId of the code-customized base applications instead. This allows any extensions that are dependent on the `Application` to resolve to the custom appId. 

> [!NOTE]  
> Whether the extensions that are dependent on the `Application` compile and work is up to the partner redefining the application to ensure by not introducing breaking changes.

> [!IMPORTANT]  
> If you have modified the `Microsoft_Application.app` file, you can rename the file name, and change information about the `publisher`, but it is important to keep `"name": "Application"` in the extension, which is what is being checked for in terms of symbols references. It is also important to keep the `propagateDependencies` set to `true`.

## Changing the app.json file for a code-customized base application

The `app.json` file of the `Microsoft_Application.app` file looks like the following example for Business Central version 15.3.

```
{
    "id":  "c1335042-3002-4257-bf8a-75c898ccb1b8",
    "name":  "Application",
    "publisher":  "Microsoft",
    "version":  "15.3.40074.40254",
    "propagateDependencies":  true,
    "logo":  "ExtensionLogo.png",
    "privacyStatement":  "https://go.microsoft.com/fwlink/?LinkId=724009",
    "EULA":  "https://go.microsoft.com/fwlink/?linkid=2009120",
    "help":  "https://go.microsoft.com/fwlink/?linkid=2104024",
    "url":  "https://go.microsoft.com/fwlink/?LinkId=724011",
    "dependencies":  [
                         {
                             "appId":  "437dbf0e-84ff-417a-965d-ed2bb9650972",
                             "name":  "Base Application",
                             "publisher":  "Microsoft",
                             "version":  "15.3.0.0"
                         },
                         {
                             "appId":  "63ca2fa4-4f03-4f2b-a480-172fef340d3f",
                             "name":  "System Application",
                             "publisher":  "Microsoft",
                             "version":  "15.3.0.0"
                         }
                     ],
    "screenshots":  [

                    ],
    "platform":  "15.0.0.0",
    "showMyCode":  true,
    "brief":  "Application (W1)"
}

```
If you have a code-customized base application, the file can be edited to reflect the dependency to this instead. To do so, update the `"dependencies": []` section and change the `"appId":  "437dbf0e-84ff-417a-965d-ed2bb9650972"` to the `appId` of your code-customized base application. You can update the `"name"` and `"publisher"` information to match too.

```
...
"dependencies":  [
                         {
                             "appId":  "<appId of the code-customized base app>",
                             "name":  "Customized Base Application",
                             "publisher":  "PartnerSolutions",
                             "version":  "15.3.0.0"
                         },
                         ...
                     ],
...
```

## See Also

[JSON Files](devenv-json-files.md)  
[Instal an Update](../upgrade/upgrading-cumulative-update-v15.md)  