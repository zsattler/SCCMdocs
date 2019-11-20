---
title: Management insights
titleSuffix: Configuration Manager
description: Learn about the management insights functionality available in the Configuration Manager console.
ms.date: 08/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
---

# Management insights in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Management insights in Configuration Manager provide information about the current state of your environment. The information is based on analysis of data from the site database. Insights help you to better understand your environment and take action based on the insight. This feature was released in Configuration Manager version 1802. <!--1353967-->


## Review management insights

To view the rules, your account needs the **read** permission on the **site** object.

1. Open the Configuration Manager Console.  

2. Go to the **Administration** workspace, expand **Management Insights**, and select **All Insights**.  

    > [!Note]  
    > Starting in version 1810, when you select the **Management Insights** node, it shows the [Management insights dashboard](#bkmk_insights).  

3. Open the management insights group name you want to review. Select **Show Insights** in the ribbon.  

The following four tabs are available for review:

- **All Rules**: Gives the complete list of rules for the management insight group chosen.  

- **Complete**:  Lists rules where no action is needed.  

- **In Progress**: Shows rules where some, but not all, prerequisites are complete.  

- **Action Needed**: Rules needing actions taken are listed. Select **More Details** to retrieve specific items where action is needed.  

The **Prerequisites** pane lists the required items needed to run the rule.

### All rules and prerequisites for the cloud services group

![Management insights- All rules and prerequisites for cloud services group](./media/Management-insights-all-cloud-rules.png)

Select a rule and then select **More Details** to see the rule details.


## Operations

The management insight rules reevaluate their applicability on a weekly schedule. To reevaluate a rule on-demand, right-click the rule and select **Re-evaluate**.

The log file for management insight rules is **SMS_DataEngine.log** on the site server.

<!--1357930-->
Starting in version 1806, some rules let you take action. Select a rule, select **More Details**, and then if available select **Take action**.

Depending upon the rule, this action has one of the following behaviors:  

- Automatically navigate in the console to the node where you can take further action. For example, if the management insight recommends changing a client setting, taking action navigates to the Client Settings node. Then take further action by modifying the default or a custom client settings object.  

- Navigate to a filtered view based on a query. For example, taking action on the empty collections rule shows just these collections in the list of collections. Then take further action, such as deleting a collection or modifying its membership rules.  


## <a name="bkmk_insights"></a> Management insights dashboard

<!--1357979-->

Starting in version 1810, the **Management Insights** node includes a graphical dashboard. This dashboard displays an overview of the rule states, which makes it easier for you to show your progress.

Use the following filters at the top of the dashboard to refine the view:

- Show Completed
- Optional
- Recommended
- Critical

The dashboard includes the following tiles:  

- **Management insights index**: Tracks overall progress on management insights rules. The index is a weighted average. Critical rules are worth the most. This index gives the least weight to optional rules.  

- **Management insights groups**: Shows percent of rules in each group, honoring the filters. Select a group to drill down to the specific rules in this group.  

- **Management insights priority**: Shows percent of rules by priority, honoring the filters.  

- **All insights**: A table of insights including priority and state. Use the **Filter** field at the top of the table to match strings in any of the available columns. The dashboard sorts the table in the following order:

    - Status: Action Needed, Completed, Unknown  
    - Priority: Critical, Recommended, Optional  
    - Last Changed: older dates on top  

![Screenshot of management insights dashboard](media/1357979-management-insights-dashboard.png)


## Groups and rules

Rules are organized into the following management insight groups:

- [Applications](#applications)  
- [Cloud services](#cloud-services)  
- [Collections](#collections)  
- [Proactive maintenance](#proactive-maintenance)  
- [Security](#security)  
- [Simplified management](#simplified-management)  
- [Software Center](#software-center)  
- [Windows 10](#windows-10)  

### Applications

Insights for your application management.

- **Applications without deployments**: Lists the applications in your environment that don't have active deployments. This rule helps you find and delete unused applications to simplify the list of applications displayed in the console. For more information, see [Deploy applications](/sccm/apps/deploy-use/deploy-applications).  

### Cloud services

Helps you integrate with many cloud services, which enable modern management of your devices.

- **Assess co-management readiness**: Helps you understand what steps are needed to enable co-management. This rule has prerequisites. For more information, see [Co-management overview](/sccm/comanage/overview).  

- **Configure Azure services for use with Configuration Manager**: This rule helps you onboard Configuration Manager to Azure AD, which enables clients to authenticate with the site using Azure AD. For more information, see [Configure Azure services](/sccm/core/servers/deploy/configure/azure-services-wizard).  

- **Enable devices to be hybrid Azure Active Directory joined**: Azure AD-joined devices allow users to sign in with their domain credentials while ensuring devices meet the organization's security and compliance standards. For more information, see [Azure AD hybrid identity design considerations](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview).  

- **Update clients to the latest Windows 10 version**: Windows 10, version 1709 or above improves and modernizes the computing experience of your users. For more information, see [Key articles about adopting Windows as a service](/sccm/core/understand/configuration-manager-and-windows-as-service#key-articles-about-adopting-windows-as-a-service).  

### Collections

Insights that help simplify management by cleaning up and reconfiguring collections.

- **Empty Collections**: Lists collections in your environment that have no members. For more information, see [How to manage collections](/sccm/core/clients/manage/collections/manage-collections).  

Starting in version 1902, there are new rules with recommendations on managing collections.<!--3555752--> Use these insights to simplify management and improve performance:

- **Collections with no query rules and no direct members**: To simplify the list of collections in your hierarchy, delete these collections.  

- **Collections with the same re-evaluation start time**: These collections have the same re-evaluation time as other collections. Modify the re-evaluation time so they don't conflict.  

- **Collections with query time over two seconds**: Review the query rules for this collection. Consider modifying or deleting the collection.

- The following rules include configurations that potentially cause unnecessary load on the site. Review these collections, then either delete them, or disable rule evaluation:  

    - **Collections with no query rules and incremental updates enabled**  

    - **Collections with no query rules and enabled for scheduled or incremental evaluation**  

    - **Collections with no query rules and schedule full evaluation selected**  


### Proactive maintenance

<!--1352184-->
Starting in version 1806, the rules in this group highlight potential configuration issues to avoid through upkeep of Configuration Manager objects.

- **Boundary groups with no assigned site systems**: Without assigned site systems, boundary groups can only be used for site assignment. For more information, see [Configure boundary groups](/sccm/core/servers/deploy/configure/boundary-groups).  

- **Boundary groups with no members**: Boundary groups aren’t applicable for site assignment or content lookup if they don’t have any members. For more information, see [Configure boundary groups](/sccm/core/servers/deploy/configure/boundary-groups).  

- **Distribution points not serving content to clients**: Distribution points that haven't served content to clients in the past 30 days. This data is based on reports from clients of their download history. For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points).  

- **Enable WSUS Cleanup**: Verifies that you've enabled the option to run WSUS cleanup on the properties of the software update point component. This option helps to improve WSUS performance. For more information, see [Software update maintenance](/sccm/sum/deploy-use/software-updates-maintenance).  

- **Unused boot images**: Boot images not referenced for PXE boot or task sequence use. For more information, see [Manage boot images](/sccm/osd/get-started/manage-boot-images).  

- **Unused configuration items**: Configuration items that aren't part of a configuration baseline and are older than 30 days. For more information, see [Create configuration baselines](/sccm/compliance/deploy-use/create-configuration-baselines).  

- **Upgrade peer cache sources to the latest version of the Configuration Manager client**: Identify clients that serve as a peer cache source but haven't upgraded from a pre-1806 client version. Pre-1806 clients can't be used as a peer cache source for clients that run version 1806 or later. Select **Take action** to open a device view that displays the list of clients.<!--1358008-->  

### Security

Insights for improving the security of your infrastructure and devices.

- **NTLM fallback is enabled**:<!--4572953--> Starting in version 1906, this rule detects if you enabled the less secure NTLM authentication fallback method for the site. When using the client push method of installing the Configuration Manager client, the site can require Kerberos mutual authentication. This enhancement helps to secure the communication between the server and the client. For more information, see [How to install clients with client push](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).

- **Unsupported antimalware client versions**: More than 10% of clients are running versions of System Center Endpoint Protection that aren't supported. For more information, see [Endpoint Protection](/sccm/protect/deploy-use/endpoint-protection).  

### Simplified management

Insights that help you simplify the day-to-day management of your environment.

- **Connect the site to the Microsoft cloud for Configuration Manager updates**: This rule makes sure your Configuration Manager service connection point has connected to the Microsoft cloud within the past seven days. This connection is to download content for regular updates. Review DMPDownloader.log and hman.log. For more information, see [Internet access requirements](/sccm/core/plan-design/network/internet-endpoints#bkmk_scp-updates).

- **Non-CB Client Versions**: Lists all clients whose versions aren't a current branch (CB) build. For more information, see [Upgrade clients](/sccm/core/clients/manage/upgrade/upgrade-clients).  

- **Update clients to a supported Windows 10 version**: Starting in version 1902, this rule reports on clients that are running a version of Windows 10 that's no longer supported. It also includes clients with a Windows 10 version that's near end of service (three months).<!--3897268-->  


### Software Center

Insights for managing Software Center.

- **Direct users to Software Center instead of Application Catalog**: Check if users have installed or requested applications from the application catalog in the last 14 days. The primary functionality of application catalog is now included in Software Center. The application catalog is deprecated. For more information, see [Deprecated features](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures#deprecated-features).  

- **Use the new version of Software Center**: The previous version of Software Center is no longer supported. Set up clients to use the new Software Center by enabling the client setting **Use new Software Center** in the **Computer Agent** group. For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings#use-new-software-center).  

### Software Updates

- **Client settings aren't configured to allow clients to download delta content**: Some software updates synchronized in your environment include delta content. Enable the client setting, **Allow clients to download delta content when available**. If you don't enable this setting, when you deploy these updates, client will unnecessarily download more content than they require. For more information, see [Client settings - Software updates](/sccm/core/clients/deploy/about-client-settings#software-updates).

- **Enable the software updates product category 'Windows 10, version 1903 and later'**: There's a new software updates product category for Windows 10, version 1903 and later. If you synchronize Windows 10 updates and have Windows 10, version 1903 or later clients, select the **Windows 10, version 1903 and later** product category in the software update point component properties. For more information, see[Configure classifications and products to synchronize](/sccm/sum/get-started/configure-classifications-and-products).

### Windows 10

Insights related to the deployment and servicing of Windows 10. The Windows 10 management insight group is only available when more than half of clients are running Windows 7, Windows 8, or Windows 8.1.

- **Configure Windows telemetry and commercial ID key**: To use data from Upgrade Readiness, configure devices with a Commercial ID key and enable collection of diagnostic data. Set Windows 10 devices to **Enhanced (Limited)** level or higher. For more information, see [Configure clients to report data to Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics).  

- **Connect Configuration Manager to Upgrade Readiness**: Use Upgrade Readiness for your Windows 10 deployments before Windows 7 goes out of support. For more information, see [Integrate Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics).  

#### Windows 10 management insights rules

![Management insights- Rules for Windows 10](./media/Windows-10-insights-group.png)
