---
title: Change the MDM authority
titleSuffix: Configuration Manager
description: Learn how to change the MDM authority from hybrid MDM to Intune standalone for  for specific users (mixed MDM authority).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 05/21/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 6f0201d7-5714-4ba0-b2bf-d1acd0203e9a
ms.collection: M365-identity-device-management
---

# Change the MDM authority for specific users (mixed MDM authority)

*Applies to: System Center Configuration Manager (Current Branch)*

You can configure a mixed MDM authority in the same tenant. Manage some users in Microsoft Intune and others with hybrid MDM. This article provides information about how to start moving users to Intune standalone. It assumes that you've completed the following steps:  

- Used the data import tool to [import Configuration Manager objects to Intune](migrate-import-data.md) (optional).  

- [Prepared Intune for user migration](migrate-prepare-intune.md) to make sure users and their devices continue to be managed after they're migrated.  

> [!Note]  
> A full reset of your tenant removes all policies, apps, and device enrollments. If you decide you want to do this process, call support for assistance.  

Manage migrated users and their devices in Intune. Continue to manage other devices in Configuration Manager. To verify that everything is working as expected, start with a small test group of users. Then gradually migrate additional groups of users. When you're ready, switch the tenant-level MDM authority from Configuration Manager to Intune standalone.

> [!Important]  
> As of August 13, 2018, hybrid mobile device management is a [deprecated feature](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). For more information, see [What is hybrid MDM](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## Things to know before you migrate users

- During the phased migration, any existing MDM policies or apps in Configuration Manager continue to apply to hybrid MDM devices.  

- The devices for the users in the collection associated with the Intune subscription can enroll in hybrid MDM. All devices associated with users not in the collection are managed in Intune as long as the user has an Intune/EMS license.  

    > [!Note]  
    > Users can enroll into Intune standalone even if you've blocked them through the Configuration Manager console. To completely block a user from enrolling, don't license the unwanted users for Intune. They can't enroll without a license.<!--SCCMDocs issue 738-->  

- When you migrate a user to Intune, the user and devices appear in the Intune on Azure portal after about 15 minutes.  

- When you migrate users to Intune standalone, continue to manage the following settings from Configuration Manager for both Intune standalone and hybrid MDM devices:  

    - [Apple Push Notification service (APNs) certificate](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac)  

    - [Device Enrollment Program](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)  

        > [!Note]  
        > You don't need to recreate your DEP token or remove it from Configuration Manager. It automatically migrates to Intune 24 hours after you change the tenant's MDM authority from Configuration Manager to Intune. This change is the final step in the migration. (If the DEP token doesn't migrate within 24 hours, contact Microsoft support for assistance.)  

    - Enrollment profiles  

    - [Volume Purchase Program (VPP) licenses](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)  

    - Corporate identifiers  

    - [Code Signing certificates](/sccm/mdm/deploy-use/enroll-hybrid-windows)  

    - [Device categories](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections)  

    - [Enrollment managers](/sccm/mdm/plan-design/device-enrollment-methods)  

    - Terms and conditions  

    - Windows SLKs  

    - Company Portal branding  

    > [!Important]  
    > Continue to edit the tenant-level policies using the Configuration Manager console. After you [change your tenant-level MDM authority](/sccm/mdm/deploy-use/change-mdm-authority) to Intune, the tenant-level policies that you were managing in Configuration Manager automatically migrate to Intune on Azure. An example of such a policy is for Apple Push Notification service (APNs) certificates.<!--SCCMDocs issue #971-->  

- If you use code signing certificates, we recommend that you migrate users in a phased approach. After a mobile device is migrated, it makes a certificate authority request for a new certificate. By using a phased approach to migrate users (and their devices), it limits the number of simultaneous certificate authority requests.  

- Don't migrate any user accounts that have been added as device enrollment managers (DEM) in Configuration Manager. Later, when you change your tenant-level MDM authority to Intune, these user accounts migrate correctly. If you do migrate the DEM user account before the tenant-level MDM authority change, you must manually add the user as a DEM in Intune on Azure. However, devices enrolled by using a DEM don't migrate successfully. Call support to migrate these devices. For more information, see [Add a device enrollment manager](https://docs.microsoft.com/intune/device-enrollment-manager-enroll#add-a-device-enrollment-manager).  

    > [!Note]  
    > While in mixed authority mode, don't move these accounts to Intune by removing them from the ConfigMgr cloud collection. If you do, the user becomes a standard user, and can't enroll more than 15 devices. Instead, migrate these users and their devices once you fully switch the MDM authority for the tenant.<!--Intune bug 2174210-->  

- Devices enrolled by using a DEM and devices without [user affinity](/sccm/mdm/deploy-use/user-affinity-for-hybrid-managed-devices) aren't automatically migrated to the new MDM authority. To switch the management authority for these MDM devices, see [Migrate devices without user affinity](#migrate-devices-without-user-affinity).  



## Migrate users to Intune

To test that your Intune configurations are working as expected, first migrate a small set of users and their devices. Then, after you confirm things are working as expected, you can start migrating more AAD groups with more users and their devices.



## Migrate a test group of users to Intune standalone

The devices for the users in the collection associated with the Intune subscription can enroll in hybrid MDM. When you remove a user from the collection, if the user has an assigned Intune license, their enrolled devices are migrated to Intune standalone. If you haven't already assigned licenses to users that you plan to migrate, see [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/licenses-assign). In the collection for the Intune subscription, you can exclude user collections from your main collection to migrate the users in the excluded collection.

In the following example, the Hybrid users collection contains all members from the All Users collection. This configuration allows any user to enroll a device into hybrid MDM. To migrate users to Intune standalone, you select Exclude Collections and add a collection with the users to migrate. When you're ready to migrate more users, add additional excluded collections that include those users.

![Exclude collections](../media/migrate-excludecollections.png)

> [!Note]  
>   When you have the **All Users** collection selected for the Intune subscription, you are not allowed to add a rule to exclude collections. Instead, create a new collection based on the **All Users** collection, verify that the collection contains the users that you expect, and then edit the Intune subscription to use the new collection. You can exclude user collections from the new collection to migrate users. If you exclude a user from a collection but include a group that the user is a member of, the user will not be excluded from the collection.

To migrate a test group of users to Intune, create a user collection that contains the users to migrate. Then exclude the user collection from the collection that's used for the Intune subscription.  

The following diagram provides an overview of how user migration works.

![Mixed authority overview](../media/migrate-mixedauthority.svg)

1. Verify that the user has an Intune/EMS license.  

2. Create a collection to exclude from the collection for the Intune subscription. In this example, the **All Hybrid users** collection contains a rule to exclude users in the **Migration pilot** collection. **User1** is a member of the **Migration pilot** collection and is excluded from the **All Hybrid users** collection.  

3. **User1**'s devices are now managed from Intune in the Azure portal.  

4. All other devices continue to be managed from the Configuration Manager console.  

> [!Important]  
> When you move a user from hybrid to standalone, removal of policy is suspended for seven days.<!-- SCCMDocs issue #1066 -->


## Verify Intune standalone functionality

After you migrate a small set of users, verify that the user’s devices are listed in Intune. Go to **Devices**, and select **All devices**.

Then, verify that your policies, profiles, and apps are working as expected on the user devices.



## Migrate additional users

After you verify that Intune standalone is functioning as you expect, start migrating additional users. Just as you created a collection with a set of test users, create collections that include users to migrate. Exclude those collections from the collection that's associated with the Intune subscription. For details, see [Migrate a test group of users to Intune standalone](#migrate-a-test-group-of-users-to-intune-standalone).



## Migrate devices without user affinity

To migrate individual devices form Configuration Manager to Intune that were enrolled without user affinity, use the Switch-MdmDeviceAuthority PowerShell cmdlet.  After migrating selected devices using the cmdlet, validate in Intune in Azure that the migration occurred as expected for the selected devices. Then, when you're ready, change the MDM authority to Intune for the tenant to complete the migration for any remaining devices that have Configuration Manager as their MDM authority.

### Cmdlet *Switch-MdmDeviceAuthority*

#### SYNOPSIS

The cmdlet switches the management authority of MDM devices without user affinity (For example, bulk-enrolled devices). The cmdlet switches between Intune and Configuration Manager management authorities. It switches for the specified devices based on their management authorities when you run the cmdlet.

### SYNTAX

`Switch-MdmDeviceAuthority -DeviceIds <Guid[]> [-Credential <PSCredential>] [-Force] [-LogFilePath <string>] [-LoggingLevel {Off | Critical | Error | Warning | Information | Verbose | ActivityTracing | All}] [-Confirm] [-WhatIf] [<CommonParameters>]`


### PARAMETERS

#### `-Credential <PSCredential>`

A PowerShell credential object for the Azure AD user account that is used when switching device management authorities. If the parameter isn't specified, the user is prompted for credentials. The directory role for this user account should be either a **Global administrator** or a **Limited administrator** with the administrative role of **Intune administrator**.

#### `-DeviceIds <Guid[]>`

The IDs of the MDM devices that need to have their management authority switched. The device IDs are unique identifiers for the devices displayed by the Configuration Manager console.

#### `-Force [<SwitchParameter>]`

Specify parameter to disable the Should Continue prompt.

#### `-LogFilePath <string>`

Path to log file location.

#### `-LoggingLevel <SourceLevels>`

The log level used to determine the type of logs that need to be written to the log file.

The following are the possible values for LoggingLevel:

- ActivityTracing
- All
- Critical
- Error
- Information
- Off
- Verbose
- Warning

#### `-Confirm [<SwitchParameter>]`

Prompts you for confirmation before executing the command.

#### `-WhatIf [<SwitchParameter>]`

Describes what would happen if you executed the command without actually executing the command.

#### `<CommonParameters>`

This cmdlet supports the common parameters: Verbose, Debug,
ErrorAction, ErrorVariable, WarningAction, WarningVariable,
OutBuffer, PipelineVariable, and OutVariable. For more information, see
[about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

### Example 1

``` powershell
C:\PS>Switch-MdmDeviceAuthority -Credential $creds -DeviceIds $deviceIds

  DeviceId       : 62e6ea43-18f8-4278-bcd4-a4baed2c6d24
  Success        : True
  FailureReason  :
  NewAuthority   : Intune
  CompletionTime : 11/15/2017 8:00:11 PM

Description

-----------

Successfully switched the management authority of the device from Configuration Manager to Intune.
```

### REMARKS

- To see the examples, type: `get-help Switch-MdmDeviceAuthority -examples`  
- For more information, type: `get-help Switch-MdmDeviceAuthority -detailed`  
- For technical information, type: `get-help Switch-MdmDeviceAuthority -full`  
- For online help, type: `get-help Switch-MdmDeviceAuthority -online`  



## Next steps

After you migrate users and test Intune functionality, consider whether you're ready to [change the MDM authority](migrate-change-mdm-authority.md) of your Intune tenant from Configuration Manager to Intune.
