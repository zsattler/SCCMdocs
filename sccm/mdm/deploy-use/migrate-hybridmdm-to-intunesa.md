---
title: Migrate hybrid MDM resources to Intune standalone
titleSuffix: Configuration Manager
description: Learn how to migrate hybrid MDM users and devices to Intune on Azure.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/14/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 1dd696ce-3e46-4dfa-a76d-592fe0f0320e
ms.collection: M365-identity-device-management
---

# Migrate hybrid MDM users and devices to Intune standalone

*Applies to: System Center Configuration Manager (Current Branch)*    

This article is to migrate from hybrid MDM to a cloud-only experience using Intune on Azure. 

> [!Important]  
> As of August 14, 2018, hybrid mobile device management is a [deprecated feature](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). For more information, see [What is hybrid MDM](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  


Start migrating to Intune standalone using a phased approach. With this approach, you test a small subset of users and devices while most of your users and devices are still managed with hybrid MDM. After you verify Intune functionality, start migrating more resources to Intune.    

For more information, see the following articles:    
  
1. [Import Configuration Manager data to Microsoft Intune](migrate-import-data.md)   

    The Intune Data Importer tool:  

    - Collects data about the objects you select from your Configuration Manager hierarchy  

    - Provides details about the objects you can select for import   

    - Provides information about why some objects can't be imported  

    - Lets you import selected objects into your Microsoft Intune tenant  

    This step is optional. It can save you time by automating the process to recreate objects from Configuration Manager to Intune.  

2. [Prepare Intune for user migration](migrate-prepare-intune.md)    

    - Validate imported objects from Configuration Manager  

    - Create new objects  

    - Create Azure AD groups and make object assignments to these groups  

    - Install NDES and Exchange connectors  

    When you complete the steps and start the migration to Intune standalone, there is no significant impact to your users.   

3. [Change the MDM authority for specific users (mixed MDM authority)](migrate-mixed-authority.md)    

    Configure a mixed MDM authority in the same tenant. Select some users to be managed in Intune, while continuing to manage all other devices with hybrid MDM. Test that Intune functionality is working on the devices for a small subset of users before you start migrating additional users.   

4. [Change your MDM authority to Intune standalone](change-mdm-authority.md)     

    Change your tenant-level MDM authority from Configuration Manager to Intune. All remaining users and devices are migrated to Intune standalone. After you've thoroughly tested Intune functionality in the previous step, and have migrated most or all of your users, then change your tenant-level MDM authority.



## Request assistance
<!--Intune bug 2339232-->
To request assistance from the Microsoft FastTrack program, get started by going to [FastTrack for Microsoft 365](https://fasttrack.microsoft.com/microsoft365/capabilities?view=security).

1. Click "Sign In" and enter your org ID.  

2. Go to the Dashboard, and follow the prompts to access the **Request for Assistance** form.    

3. Microsoft reviews your request, and routes it to the appropriate team to address your specific needs and eligibility.  

From this dashboard, also find best practices, tools, and resources from the FastTrack experts to help make your experience with the Microsoft Cloud a great one.

