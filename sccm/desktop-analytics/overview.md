---
title: Desktop Analytics
titleSuffix: Configuration Manager
description: An overview of the Desktop Analytics service integrated with Configuration Manager.
ms.date: 10/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# What is Desktop Analytics?

Desktop Analytics is a cloud-based service that integrates with Configuration Manager. The service provides insight and intelligence for you to make more informed decisions about the update readiness of your Windows clients. It combines data from your organization with data aggregated from millions of devices connected to Microsoft cloud services.

Use Desktop Analytics with Configuration Manager to:  

- Create an inventory of apps running in your organization  

- Assess app compatibility with the latest Windows 10 feature updates  

- Identify compatibility issues, and receive mitigation suggestions based on cloud-enabled data insights  

- Create pilot groups that represent the entire application and driver estate across a minimal set of devices  

- Deploy Windows 10 to pilot and production-managed devices  

![Screenshot of the Desktop Analytics home page in the Azure portal](media/portal-home.png)

> [!Note]  
> Desktop Analytics is a successor of Windows Analytics. The *Windows Analytics* service includes Upgrade Readiness, Update Compliance, and Device Health.
>
> All of these capabilities are combined in the *Desktop Analytics* service. Desktop Analytics also is more tightly integrated with Configuration Manager.



## Benefits

Many customers have challenges with getting and staying current with Windows 10. The primary challenge is testing applications. This process is typically manual. It's time-consuming for IT administrators and application owners to continually analyze existing applications. Then remediate any issues that arise.

Desktop Analytics provides the following benefits:

- **Device and software inventory**: Inventory of key factors such as apps and versions of Windows.  

- **Pilot identification**: Identification of the smallest set of devices that provide the widest coverage of factors. It focuses on the factors that are most important to a pilot of Windows upgrades and updates. Making sure the pilot is more successful allows you to proceed more quickly and confidently to broad deployments in production.  

- **Issue identification**: Using aggregated market data along with data from your environment, the service predicts potential issues to getting and staying current with Windows. It then suggests potential mitigations.  

- **Configuration Manager integration**: The service cloud-enables your existing on-premises infrastructure. Use this data and analysis to deploy and manage Windows on your devices.  



## Prerequisites

To use Desktop Analytics, make sure your environment meets the following prerequisites.


### Technical

- An active Azure subscription, with [Global Admin](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions) permissions. [Microsoft Accounts](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts) aren't supported.  

    > [!Important]  
    > Desktop Analytics currently requires that you deploy an Office 365 service in your Azure AD tenant. This won't be a requirement in the future.

    - **Workspace owner** or **contributor** permissions to **Set up your workspace**, and the following roles:  

      - [**Desktop Analytics Administrator**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) role.

      - [**Log Analytics Contributor**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#log-analytics-contributor) and [**User Access Administrator**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) on the resource group to use an existing workspace or create a new workspace in an existing resource group.

      - [**Owner**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner), or [**Contributor**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) and [**User Access Administrator**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) permissions on the subscription to create a workspace in a new resource group.  

- Configuration Manager, version 1902 with update rollup (4500571) or later. For more information, see [Update Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix).  

    - [**Full Administrator**](/sccm/core/understand/fundamentals-of-role-based-administration#bkmk_Planroles) role in Configuration Manager  

    > [!Note]  
    > Desktop Analytics supports one Commercial ID per Azure Active Directory (Azure AD) tenant and Configuration Manager hierarchy. If you have multiple hierarchies in your environment, use different Commercial IDs and Azure AD tenants.<!-- 4958160 -->

- Devices running Windows 7, Windows 8.1, or Windows 10  

    - Install the latest updates. For more information, see [Update devices](/sccm/desktop-analytics/enroll-devices#update-devices).  

    - Devices also need to have the Configuration Manager client, version 1902 with update rollup (4500571) or later. For more information, see [Update Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix).  

    > [!Note]  
    > Desktop Analytics doesn't support upgrades to Windows 10 long-term servicing channel (LTSC). For more information, see [Windows as a service overview](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).
    >
    > Desktop Analytics is designed to best support the in-place upgrade scenario. If you need to make major changes, such as from 32-bit to 64-bit architecture, use an imaging scenario. Desktop Analytics insights are still valuable in these classic OS deployment scenarios, but you can ignore the in-place upgrade specific guidance. For more information, see [Scenarios to deploy enterprise operating systems with Configuration Manager](/sccm/osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems).

- Windows diagnostics data. For more information, see the following articles:  

    - [Diagnostic data levels](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)  

    - [Desktop Analytics privacy](/sccm/desktop-analytics/privacy)  

- Network connectivity from devices to the Microsoft public cloud. For more information, see [How to enable data sharing](/sccm/desktop-analytics/enable-data-sharing)  

> [!Important]   
> Microsoft has a strong commitment to providing the tools and resources that put you in control of your privacy. As a result, Microsoft doesn't collect the following data from devices located in European countries (EEA and Switzerland):
>
> - Windows diagnostic data from Windows 8.1 devices
> - App usage data for Windows 7

### Licensing and costs

Devices enrolled in Desktop Analytics may only be used by licensed users of:

- Windows 10 Enterprise E3 or E5 (included in Microsoft 365 F1, E3, or E5)

- Windows 10 Education A3 or A5 (included in Microsoft 365 A3 or A5)

- Windows Virtual Desktop Access E3 or E5  

Beyond the cost of license subscriptions, there's no additional cost for using Desktop Analytics. Within Azure Log Analytics, Desktop Analytics is "zero-rated." This rating means it's excluded from data limits and costs, regardless of the Azure Log Analytics pricing tier you chose. For more information on Azure Log Analytics pricing tiers, see [Pricing - Log Analytics](https://azure.microsoft.com/pricing/details/monitor/).

- If you use the free tier, which has a cap on the amount of data collected per day, the Desktop Analytics data doesn't count towards this cap. You can collect all the Desktop Analytics data from your devices and still have the full cap available for collecting additional data from other sources.

- If you use a paid tier that charges per GB of data collected, you're not charged for the Desktop Analytics data. You can collect all the Desktop Analytics data from your devices and not incur any costs.

> [!Note]  
> Different Azure Log Analytics plans have different data retention periods. Desktop Analytics inherits the workspace's data retention policy. If your workspace is on the free plan, then Desktop Analytics retains the last 30 days of "daily snapshots" that are collected in the workspace.


## Next steps

The following tutorial provides a step-by-step guide to getting started with Desktop Analytics and Configuration Manager:  

- [Deploy Windows 10 to pilot](/sccm/desktop-analytics/tutorial-windows10)  
