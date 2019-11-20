---
title: Technical preview releases
titleSuffix: Configuration Manager
description: Learn about the technical preview branch to test-drive new functionality and capabilities in Configuration Manager.
ms.date: 11/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Technical preview for Configuration Manager

*Applies to: Configuration Manager (technical preview branch)*

This article provides details about the monthly technical preview branch of Configuration Manager. The technical preview introduces new functionality that Microsoft is working on. It introduces new features that aren't yet included in the current branch of Configuration Manager. These features might eventually be included in an update to the current branch. Before we finalize the features, we want you to try them out and give us feedback.  

Because this release is a technical preview, details and functionality are subject to change.  

This information applies to all versions of the Configuration Manager technical preview branch. This article lists each new feature along with the technical preview version in which it first appears. For example, version **1908** for August (08) of 2019 (19). Separate articles dedicated to each preview version detail the individual features.  

For information about what's new in the *current branch* of Configuration Manager, see [What's new in Configuration Manager incremental versions](/sccm/core/plan-design/changes/whats-new-incremental-versions).

> [!Tip]  
> To get notified when this page is updated, copy and paste the following URL into your RSS feed reader:
> `https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`

## <a name="bkmk_reqs"></a> Requirements and limitations  

> [!IMPORTANT]  
> The technical preview is licensed for use only in a lab environment. Microsoft may not provide support services and certain features may not be available in technical previews. Additionally, technical preview software may have reduced or different security, privacy, accessibility, availability, and reliability standards relative to commercially provided software.  

For most product prerequisites, use the information in the [Supported configurations](/sccm/core/plan-design/configs/supported-configurations). The following exceptions apply to the technical preview branch:  

- Each install is active for 90 days before it becomes inactive.  

- English is the only language supported.  

- It only supports the following setup command-line parameters:  

    - `/silent`  
    - `/testdbupgrade`  

- The service connection point installs to online mode. It doesn't support offline mode.  

- The separate articles for each specific version of the technical preview include additional limitations or requirements, as applicable.

- The following features aren't supported with the technical preview branch:  

    - [Migration](/sccm/core/migration/migrate-data-between-hierarchies) to or from this preview branch.  

    - [Upgrade](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) to this preview branch.  

    - [Site recovery](/sccm/core/servers/manage/recover-sites) from the cd.latest folder.  <!--507106-->

- There's no support for updating to current branch from this preview branch.  

    > [!Note]  
    > When updates are available for a preview version, you still find and install them from the **Updates and Servicing** node of the Configuration Manager console. For a video of the in-console upgrade process, see [Installing Configuration Manager update packages](https://www.youtube.com/embed/KBd_EGFbUT8) on youtube.com.  

- It only supports a standalone primary site. There's no support for a central administration site, multiple primary sites, or secondary sites.  

The technical preview branch of Configuration Manager supports the following products and technologies:

- It only supports the following versions of **SQL Server**:  

    - SQL Server 2017 (with cumulative update 2 or later)
    - SQL Server 2016 (with no service pack or later)
    - SQL Server 2014 (with service pack 1 or later)
    - SQL Server 2012 (with service pack 3 or later)  

- The site supports up to 10 clients, which can run any [supported client OS version](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).<!-- SCCMDocs#1656 -->

> [!Note]  
> The inclusion of these products in this content doesn't imply an extension of support for a version that's beyond its support lifecycle. Configuration Manager doesn't support products that are beyond their support lifecycle. For more information, see [Microsoft Lifecycle Policy](https://go.microsoft.com/fwlink/p/?LinkId=208270).  

## <a name="bkmk_install"></a> Install and update  

The Configuration Manager technical preview branch for lab use is distinct from the Configuration Manager current branch for production use.  

First install a baseline version of the technical preview branch. After installing a baseline version, then use in-console updates to bring your installation up-to-date with the most recent preview version. Typically, new versions of the technical preview are available each month.

Microsoft supports each technical preview version up until three successive versions are available. For example, when version 1708 released, version 1704 was no longer in support. Versions 1705, 1706, and 1707 remained in support. When a baseline falls out of support, it's still supported for installing a new technical preview site, assuming you immediately update to a supported version. The older baseline is supported until a new baseline version is available. Update to the latest available version from the baseline, and then repeat the update process until you install the latest technical preview version.

> [!TIP]  
> When you install an update to the technical preview, you update your preview installation to that new technical preview version. A technical preview installation never has the option to upgrade to a current branch installation. It also never receives updates from the current branch release.
>
> Several times throughout the year, there are technical preview branch and current branch versions with the same version number. For example, there is a technical preview version 1802 and a current branch version 1802.

### Active baseline versions

Install a baseline version for up to one year after its release. When you install a new technical preview site, use the latest baseline version.

- **Technical preview version 1911**: The Configuration Manager technical preview branch version 1911 is available as both an in-console update and as a new baseline version.

Download a baseline version from the [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

## <a name="BKMK_TPFeedback"></a> Providing feedback  

We love to hear your feedback about the new features in the technical preview. For more information, see [Product feedback](/sccm/core/understand/find-help#product-feedback).

If you have ideas about new features you would like to see, we want to know that as well. To submit new ideas and to vote on the ideas submitted by others, [visit our UserVoice page](https://configurationmanager.uservoice.com).  


<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->


## <a name="bkmk_tpCaps"></a> Features in the most recent version  

The following features are available with the most recent Configuration Manager technical preview version:

<!-- This is the full list of new features in the latest TP release -->

### Technical preview version 1911

<!-- - [title](/sccm/core/get-started/2019/technical-preview-1901#bkmk_anchor) <!--ID-->

- [Microsoft Endpoint Configuration Manager](/sccm/core/get-started/2019/technical-preview-1911#bkmk_mem) <!--4960084-->
- [Microsoft Connected Cache support for Intune Win32 apps](/sccm/core/get-started/2019/technical-preview-1911#bkmk_cache) <!--5032900-->

> [!Note]  
> Features that were available in a previous version of the technical preview remain available in later versions. Similarly, features that are added to the Configuration Manager current branch remain available in the technical preview branch.  

## Features in recent technical previews

The following features were released with previous versions of the Configuration Manager technical preview branch since current branch version 1906:

### Technical preview version 1910

- [Deploy Microsoft Edge, version 77 and later](/sccm/core/get-started/2019/technical-preview-1910#bkmk_Microsoft_Edge) <!--4561024-->
- [Include custom configuration baselines as part of compliance policy assessment](/sccm/core/get-started/2019/technical-preview-1910#bkmk_CAbaselines) <!--3608345-->
- [Improvements to application groups](/sccm/core/get-started/2019/technical-preview-1910#bkmk_appgrp) <!--4760058-->
- [Reclaim SEDO lock](/sccm/core/get-started/2019/technical-preview-1910#bkmk_sedo) <!--4786915-->
- [Attach files to feedback](/sccm/core/get-started/2019/technical-preview-1910#attach-files-to-feedback) <!--3556011-->
- [Client diagnostic actions](/sccm/core/get-started/2019/technical-preview-1910#bkmk_diag) <!--4433455-->
- [Office 365 ProPlus pilot and health dashboard](/sccm/core/get-started/2019/technical-preview-1910#office-365-proplus-pilot-and-health-dashboard) <!--4488272-->
- [Improvements to console search](/sccm/core/get-started/2019/technical-preview-1910#bkmk_search) <!--4640570-->
- [New variable for Windows 10 in-place upgrade](/sccm/core/get-started/2019/technical-preview-1910#bkmk_osdvar) <!--4680263-->
- [Improvements to Windows Virtual Desktop support](/sccm/core/get-started/2019/technical-preview-1910#bkmk_wvd) <!--4737447-->

### Technical preview version 1909

- [Orchestration Groups](/sccm/core/get-started/2019/technical-preview-1909#bkmk_OGs) <!--3098816-->
- [Improvements to BitLocker management](/sccm/core/get-started/2019/technical-preview-1909#bkmk_bitlocker) <!--3601034-->
- [Extend and migrate an on-premises site to Microsoft Azure](/sccm/core/get-started/2019/technical-preview-1909#bkmk_Azure-migration) <!--3556022-->
- [Additional CMPivot entities and enhancements](/sccm/core/get-started/2019/technical-preview-1909#bkmk_CMPivot) <!--5410930-->
- [Task sequence download on demand over the internet](/sccm/core/get-started/2019/technical-preview-1909#bkmk_dodcmg) <!--3601238-->
- [Support for Windows Insider](/sccm/core/get-started/2019/technical-preview-1909#bkmk_wifb) <!--3556023-->
- [Improved language support in task sequence](/sccm/core/get-started/2019/technical-preview-1909#bkmk_osd) <!--5411057-->
- [Office 365 ProPlus health dashboard](/sccm/core/get-started/2019/technical-preview-1909#bkmk_o365health) <!--4488301-->
- [Improvements to task sequence debugger](/sccm/core/get-started/2019/technical-preview-1909#bkmk_tsdebug) <!-- 5012536, 5012509 -->

### Technical preview version 1908.2

- [Improvements to Console Connections](/sccm/core/get-started/2019/technical-preview-1908-2#improvements-to-console-connections) <!--4923997-->
- [Improvements to multicast-enabled distribution points](/sccm/core/get-started/2019/technical-preview-1908-2#bkmk_multicast) <!--3785535-->
- [Optimizations to the CMPivot engine](/sccm/core/get-started/2019/technical-preview-1908-2#optimizations-to-the-cmpivot-engine) <!--3197353-->
- [Set keyboard layout during OS deployment](/sccm/core/get-started/2019/technical-preview-1908-2#bkmk_osd) <!--5138936-->

### Technical preview version 1908

- [Task sequence performance improvements for power plans](/sccm/core/get-started/2019/technical-preview-1908#bkmk_tsperf) <!--3555926-->
- [Local device query evaluation using CMPivot standalone](/sccm/core/get-started/2019/technical-preview-1908#local-device-query-evaluation-using-cmpivot-standalone) <!--3197353-->
- [Additional software update filter for ADRs](/sccm/core/get-started/2019/technical-preview-1908#additional-software-update-filter-for-adrs) <!--4852033-->
- [Use Delivery Optimization for all Windows updates](/sccm/core/get-started/2019/technical-preview-1908#use-delivery-optimization-for-all-windows-updates) <!--4699118 (4685210)-->
- [Phased deployment templates](/sccm/core/get-started/2019/technical-preview-1908#phased-deployment-templates) <!--4961086-->
- [Improvements to console connections node](/sccm/core/get-started/2019/technical-preview-1908#improvements-to-console-connections-node) <!--4923997 (4951240)-->
- [Copy and paste task sequence conditions](/sccm/core/get-started/2019/technical-preview-1908#bkmk_tscondition) <!--4621098-->
- [Improvements to task sequence search](/sccm/core/get-started/2019/technical-preview-1908#bkmk_tssearch) <!--4621085-->
- [Improvements to OS deployment](/sccm/core/get-started/2019/technical-preview-1908#bkmk_osd) <!--4910348, 4931110, 4977616-->

### Technical preview version 1907

- [Search the task sequence editor](/sccm/core/get-started/2019/technical-preview-1907#bkmk_tsedit) <!--4621085-->
- [Improvements to Office 365 ProPlus upgrade readiness dashboard](/sccm/core/get-started/2019/technical-preview-1907#improvements-to-office-365-proplus-upgrade-readiness-dashboard) <!--4021125-->


> [!Tip]  
> When a new current branch version is available, features that are available in that version are listed in the latest *What's new* article. For more information, see [What's new in incremental versions](/sccm/core/plan-design/changes/whats-new-incremental-versions#supported-versions).

<!-- This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->


## Features in previous technical previews

The following features were released with previous versions of the Configuration Manager technical preview branch. These features remain available in later versions, but aren't yet available in the current branch.

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

| Feature        | Technical preview version |  
|----------------|---------------------------|
| Remote control anywhere using cloud management gateway <!--4575930--> | [Tech Preview 1906](/sccm/core/get-started/2019/technical-preview-1906#remote-control-anywhere-using-cloud-management-gateway) |
| Improvements to Community Hub <!--3555935--> | [Tech Preview 1906](/sccm/core/get-started/2019/technical-preview-1906#bkmk_hub) |
| Additional options for third-party update catalogs <!--4469002--> | [Tech Preview 1906](/sccm/core/get-started/2019/technical-preview-1906#additional-options-for-third-party-update-catalogs) |
| Task sequence as an app model deployment type <!--3555953--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_tsdt) |
| BitLocker management <!--3601034--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_bitlocker) |
| Improvements to Community Hub <!--4224401--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_hub) |
| Community Hub and GitHub <!--3555935--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#community-hub-and-github) |
| Cloud services cost estimator <!--3555774--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_cmg) |
| Download reports from the Community Hub <!--3555936--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) |
| Community Hub <!--3556020, fka 1357766--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) |
| Client-based PXE responder service <!--3556018, fka 1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| PXE network boot support for IPv6 <!--3601254, fka 1269793--> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Use Azure Active Directory <!--3607315, fka 1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Improvements to Asset Intelligence <!--3601024, fka 1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |


## See also  

For more information, see the following articles:  

- [Evaluate Configuration Manager in a lab](/sccm/core/get-started/evaluate-with-lab-environment)
- [What's new in Configuration Manager incremental versions](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Introduction to Configuration Manager](/sccm/core/understand/introduction)

> [!Tip]  
> For more information on current branch features that require consent to enable, see [pre-release features](/sccm/core/servers/manage/pre-release-features).  
>
> For more information on current branch features that you must enable first, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
