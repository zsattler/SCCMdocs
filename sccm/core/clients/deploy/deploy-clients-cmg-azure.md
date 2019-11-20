---
title: Install the client with Azure AD
titleSuffix: Configuration Manager
description: Install and assign the Configuration Manager client on Windows 10 devices using Azure Active Directory for authentication
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Install and assign Configuration Manager Windows 10 clients using Azure AD for authentication

To install the Configuration Manager client on Windows 10 devices using Azure AD authentication, integrate Configuration Manager with Azure Active Directory (Azure AD). Clients can be on the intranet communicating directly with an HTTPS-enabled management point or any management point in a site enabled for Enhanced HTTP. They can also be internet-based communicating through the CMG or with an Internet-based management point. This process uses Azure AD to authenticate clients to the Configuration Manager site. Azure AD replaces the need to configure and use client authentication certificates.

Setting up Azure AD may be easier for some customers than setting up a public key infrastructure for certificate-based authentication. There are features that require you onboard the site to Azure AD, but don't necessarily require the clients to be Azure AD-joined.<!-- SCCMDocs issue 1259 --> For more information, see the following articles:
- [Plan for Azure Active Directory](/sccm/core/plan-design/security/plan-for-security#bkmk_planazuread)
- [Use Azure AD for co-management](/sccm/comanage/quickstart-hybrid-aad)



## Before you begin

- An Azure AD tenant is a prerequisite  

- Device requirements:  

    - Windows 10  

    - Joined to Azure AD, either pure cloud domain-joined, or hybrid Azure AD-joined  

- User requirements:  

    - The logged on user must be an Azure AD identity.   

    - If the user is a federated or synchronized identity, you must use Configuration Manager [Active Directory user discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser) as well as [Azure AD user discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc). For more information about hybrid identities, see [Define a hybrid identity adoption strategy](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->  

- In addition to the [existing prerequisites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012MPpreq) for the management point site system role, also enable **ASP.NET 4.5** on this server. Include any other options that are automatically selected when enabling ASP.NET 4.5.  

- Determine whether your management point needs HTTPS. For more information, see [Enable management point for HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps).  

- Optionally set up a [cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) (CMG) to deploy internet-based clients. For on-premises clients that authenticate with Azure AD, you don't need a CMG.  


## Configure Azure Services for Cloud Management

Connect your Configuration Manager site to Azure AD as the first step. For details of this process, see [Configure Azure services](/sccm/core/servers/deploy/configure/azure-services-wizard). Create a connection to the **Cloud Management** service.

Enable [Azure AD User Discovery](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc) as part of onboarding to **Cloud Management**. 

After you complete these actions, your Configuration Manager site is connected to Azure AD. 



## Configure client settings

These client settings help join Windows 10 devices with Azure AD. They also enable internet-based clients to use the CMG and cloud distribution point.

1. Configure the following client settings in the **Cloud Services** section using the information in [How to configure client settings](/sccm/core/clients/deploy/configure-client-settings).  

    - **Allow access to cloud distribution point**: Enable this setting to help internet-based devices get the required content to install the Configuration Manager client. If the content isn't available on the cloud distribution point, devices can retrieve the content from the CMG. The client installation bootstrap retries the cloud distribution point for four hours before it falls back to the CMG.<!--495533-->  

    - **Automatically register new Windows 10 domain joined devices with Azure Active Directory**: Set to **Yes** or **No**. The default setting is **Yes**. This behavior is also the default in Windows 10, version 1709.

    - **Enable clients to use a cloud management gateway** – Set to **Yes** (default), or **No**.  

2. Deploy the client settings to the required collection of devices. Do not deploy these settings to user collections.

To confirm the device is joined to Azure AD, run `dsregcmd.exe /status` in a command prompt. The **AzureAdjoined** field in the results shows **YES** if the device is Azure AD-joined.



## Install and register the client using Azure AD identity

To manually install the client using Azure AD identity, first review the general process on [How to install clients manually](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual). 

 > [!Note]  
 > The device needs access to the internet to contact Azure AD, but doesn't need to be internet-based. 

The following example shows the general structure of the command line:
`ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSiteCode=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`

For more information, see [Client installation properties](/sccm/core/clients/deploy/about-client-installation-properties).

The /mp and CCMHOSTNAME properties specify one of the following, depending upon the scenario:
- On-premises management point. Only specify the /mp property. The CCMHOSTNAME isn't required.
- Cloud management gateway
- Internet-based management point
The SMSMP property specifies either the on-premises or internet-based management point.

This example uses a cloud management gateway. It substitutes sample values for each property:
`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`

Starting in version 1810, the site publishes additional Azure AD information to the cloud management gateway (CMG). An Azure AD-joined client gets this information from the CMG during the ccmsetup process, using the same tenant to which it's joined. This behavior further simplifies installing the client in an environment with more than one Azure AD tenant. Now the only two required ccmsetup properties are **CCMHOSTNAME** and **SMSSiteCode**.<!--3607731-->

To automate the client install using Azure AD identity via Microsoft Intune, see [How to prepare internet-based devices for co-management](/sccm/comanage/how-to-prepare-win10#install-the-configuration-manager-client).



## Next steps

Once complete, you can continue to [monitor and manage clients](/sccm/core/clients/manage/monitor-clients).
