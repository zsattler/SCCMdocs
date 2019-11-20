---
title: Create application groups
titleSuffix: Configuration Manager
description: Create a group of applications that you can send to a user or device collection as a single deployment in Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: e67c691e-62ef-4f43-9cfb-0e957d1e7a5f
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Create application groups

<!--3555907-->

Starting in version 1906, create a group of applications that you can send to a user or device collection as a single deployment. The metadata you specify about the app group is seen in Software Center as a single entity. You can order the apps in the group so that the client installs them in a specific order.

> [!Note]  
> In this version of Configuration Manager, app groups are a pre-release feature. To enable it, see [Pre-release features](/sccm/core/servers/manage/pre-release-features).  

1. In the Configuration Manager console, go to the **Software Library** workspace. Expand **Application Management** and select the **Application Group** node.  

1. In the Create group in the ribbon, select **Create Application Group**.

1. On the **General Information** page, specify information about the app group.  

1. On the **Software Center** page, include information that shows in Software Center.  

1. On the **Application Group** page, select **Add**. Select one or more apps for this group. Reorder them using the **Move Up** and **Move Down** actions.  

1. Complete the wizard.  

Deploy the app group using the same process as for an application. For more information, see [Deploy applications](/sccm/apps/deploy-use/deploy-applications).

If you add a new app to the group after you deploy the group, you have to separately distribute the new app content to distribution points.

To troubleshoot an app group deployment, use the following log files on the client:

- **AppGroupHandler.log**
- **AppEnforce.log**
- **SettingsAgent.log**

> [!Important]  
> Don't create or deploy an app group until you update the entire hierarchy and targeted clients to at least version 1906.

### Known issues

- Apps in the group can only contain **Windows Installer** or **Script** deployment types. Set the deployment type installation behavior to **Install for system**.
- You can only deploy the app group to a device collection.
