---
localization_priority: Critical
monikerRange: exchserver-2016 || exchserver-2019
description: 'Summary: Learn about the Windows operating system prerequisites for Exchange Server 2016 and Exchange Server 2019 and the Exchange Management Tools.'
ms.topic: conceptual
author: JoanneHendrickson
ms.author: jhendr
ms.assetid:
ms.reviewer: 
title: Exchange Server prerequisites, Exchange 2019 system requirements, Exchange 2019 requirements
ms.collection:
- Strat_EX_Admin
- exchange-server
f1.keywords:
- NOCSH
audience: ITPro
ms.prod: exchange-server-it-pro
manager: serdars

---

# Exchange Server prerequisites

This topic provides the steps for installing the necessary Windows Server operating system prerequisites for Exchange Server 2016 and Exchange Server 2019 Mailbox servers and Edge Transport servers, and also the Windows prerequisites for installing the Exchange Management Tools on Windows client computers.

After you've prepared your environment for Exchange Server, use the Exchange Deployment Assistant for the next steps in your actual deployment. For information on hybrid deployments, see [Exchange Server Hybrid Deployments](../../ExchangeHybrid/exchange-hybrid.md).

To actually install Exchange 2016 and Exchange 2019, see [Deploy new installations of Exchange](deploy-new-installations/deploy-new-installations.md).

> [!TIP]
>
> - Looking for Exchange 2013 prerequisites? See [Exchange 2013 prerequisites](../../ExchangeServer2013/exchange-2013-prerequisites-exchange-2013-help.md).
>
> - Remote Registry Service must be set to Automatic and cannot be Disabled. For recommended Security Guidelines, See [Security Guidelines regarding Remote Registry](/windows-server/security/windows-services/security-guidelines-for-disabling-system-services-in-windows-server#remote-registry).
>
> - Have you heard about the Exchange Server Deployment Assistant? It's a free online tool that helps you quickly deploy Exchange Server in your organization by asking you a few questions and creating a customized deployment checklist just for you. If you want to learn more about it, go to [Microsoft Exchange Server Deployment Assistant](https://assistants.microsoft.com/).

## What do you need to know before you begin?

::: moniker range="exchserver-2019"
- Verify that your Active Directory meets the requirements for Exchange 2019: [Exchange 2019 Network and directory servers](/exchange/plan-and-deploy/system-requirements?preserve-view=true&view=exchserver-2019#network-and-directory-server-requirements-for-exchange-2019).
::: moniker-end

::: moniker range="exchserver-2016"
- Verify that your Active Directory meets the requirements for Exchange 2016: [Exchange 2016 Network and directory servers](/exchange/plan-and-deploy/system-requirements?preserve-view=true&view=exchserver-2016#network-and-directory-server-requirements-for-exchange-2016).

- The full installation option of Windows Server 2012 and Windows Server 2012 R2 must be used for all servers running Exchange 2016 server roles or management tools.

- Some prerequisites require you to reboot the server to complete installation.

> [!NOTE]
> You can't upgrade Windows from one version to another, or from Standard to Datacenter, when Exchange is installed on the server.
::: moniker-end

- Verify the [Supported operating systems for Exchange 2019](./system-requirements.md?preserve-view=true&view=exchserver-2019#supported-operating-systems-for-exchange-2019) or [Supported operating systems for Exchange 2016](./system-requirements.md?preserve-view=true&view=exchserver-2016#supported-operating-systems-for-exchange-2016).

::: moniker range="exchserver-2019"
> [!NOTE]
> New to Exchange 2019 is the ability to upgrade your operating system to a newer version while Exchange is installed on Windows Server 2019 or later.
::: moniker-end

- Verify the computer is joined to the appropriate internal Active Directory domain.

- Install the latest Windows updates on your computer.

> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://social.technet.microsoft.com/forums/office/home?category=exchangeserver).

::: moniker range="exchserver-2019"

## Exchange 2019 prerequisites for preparing Active Directory

You can use any member of the Active Directory domain to prepare Active Directory for Exchange 2019.

1. The computer requires the following software:

   a. [.NET Framework 4.8](https://download.visualstudio.microsoft.com/download/pr/014120d7-d689-4305-befd-3cb711108212/0fd66638cde16859462a6243a4629a50/ndp48-x86-x64-allos-enu.exe)

      > [!NOTE]
      > When installing on Windows Server Core, you must use key "/q" for install this package. Optionaly you can use "/log [PATH]" for logging.

   b. [Visual C++ Redistributable Package for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=30679)

      > [!NOTE]
      >
      > - The system requirements for the Visual C++ Redistributable package do not mention support for Windows Server 2016 or Windows Server 2019, but the redistributable package is safe to install on these versions of Windows.
      >
      > - An overview of the latest supported versions is available at: [Visual C++ Redistributable versions](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads).
      >
      > - The Visual C++ redistributable package is required if you're using the Exchange Setup Wizard to prepare Active Directory. If you're using unattended Setup from the command line to prepare Active Directory, this package isn't required. For more information, see [Prepare Active Directory and domains](prepare-ad-and-domains.md).

2. Install the Remote Tools Administration Pack by running the following command in Windows PowerShell:

   ```PowerShell
   Install-WindowsFeature RSAT-ADDS
   ```

> [!NOTE]
> Using the Exchange Setup Wizard to prepare Active Directory requires the installation of the Management Tools Exchange role.

## Windows Server 2019 prerequisites for Exchange 2019

The requirements to install Exchange 2019 on Windows Server 2019 computers are described in the following sections. We recommend either of the following methods to install the Windows prerequisites for Exchange 2019:

- Use the /InstallWindowsComponents switch in unattended Setup mode.
- Select the check box in the Exchange Setup Wizard to install Windows prerequisites.

When you use one of these options, you don't need to restart the computer after the Windows components have been added.

### Exchange 2019 Mailbox servers on Windows Server 2019

1. Install the following software:

   a. [.NET Framework 4.8](https://download.visualstudio.microsoft.com/download/pr/014120d7-d689-4305-befd-3cb711108212/0fd66638cde16859462a6243a4629a50/ndp48-x86-x64-allos-enu.exe)

   b. [Visual C++ Redistributable Package for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=30679)

   c. [Visual C++ Redistributable Package for Visual Studio 2013](https://support.microsoft.com/help/4032938/update-for-visual-c-2013-redistributable-package)

      > [!NOTE]
      >
      > - The system requirements for the Visual C++ redistributable package do not mention support for Windows Server 2016 or Windows Server 2019, but the redistributable package is safe to install on these versions of Windows.
      >
      > - An overview of the latest supported versions is available at: [Visual C++ Redistributable versions](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads).

   d. [IIS URL Rewrite Module](https://www.iis.net/downloads/microsoft/url-rewrite)
   
      > [!NOTE]
      >
      > The IIS URL Rewrite Module is required with Cumulative Update 11 or later.

2. Add the required Lync Server or Skype for Business Server components:

   a. Install the Server Media Foundation windows feature by executing the following command in Windows PowerShell:

      ```PowerShell
      Install-WindowsFeature Server-Media-Foundation
      ```

   b. Install [Unified Communications Managed API 4.0](https://www.microsoft.com/download/details.aspx?id=34992). This package is available for download and in the \UCMARedist folder on the Exchange Server media.

      > [!NOTE]
      > Make sure to use the Unified Communications Managed API 4.0 until something else is communicated by the Exchange team.
      >
      > When installing on Windows Server Core, you must use the installation package located in \UCMARedist on distributed media.

3. If you aren't going to use Exchange Setup to install the required Windows components (in the wizard or from the command line), run the one of the following commands in Windows PowerShell:

   - **Desktop Experience**:

      ```PowerShell
      Install-WindowsFeature Server-Media-Foundation, NET-Framework-45-Features, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Clustering-CmdInterface, RSAT-Clustering-Mgmt, RSAT-Clustering-PowerShell, WAS-Process-Model, Web-Asp-Net45, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext45, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, Windows-Identity-Foundation, RSAT-ADDS
      ```

   - **Server Core**:

      ```PowerShell
      Install-WindowsFeature Server-Media-Foundation, NET-Framework-45-Features, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Clustering-CmdInterface, RSAT-Clustering-PowerShell, WAS-Process-Model, Web-Asp-Net45, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Metabase, Web-Mgmt-Service, Web-Net-Ext45, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, RSAT-ADDS
      ```

### Exchange 2019 Edge Transport servers on Windows Server 2019

1. Install the following software:

   a. [.NET Framework 4.8](https://download.visualstudio.microsoft.com/download/pr/014120d7-d689-4305-befd-3cb711108212/0fd66638cde16859462a6243a4629a50/ndp48-x86-x64-allos-enu.exe)

   b. [Visual C++ Redistributable Package for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=30679)

      > [!NOTE]
      >
      > - The system requirements for the Visual C++ redistributable package do not mention support for Windows Server 2016 or Windows Server 2019, but the redistributable package is safe to install on these versions of Windows.
      >
      > - An overview of the latest supported versions is available at: [Visual C++ Redistributable versions](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads).

2. If you aren't going to use Exchange Setup to install the required Windows components (in the wizard or from the command line), run the following command in Windows PowerShell:

   ```PowerShell
   Install-WindowsFeature ADLDS
   ```

## Windows 10 client prerequisites for the Exchange 2019 management tools

1. Install the [Visual C++ Redistributable Package for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=30679)

   > [!NOTE]
   >
   > - The system requirements for the Visual C++ redistributable package do not mention support for Windows Server 2016 or Windows Server 2019, but the redistributable package is safe to install on these versions of Windows.
   >
   > - An overview of the latest supported versions is available at: [Visual C++ Redistributable versions](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads).

2. If you aren't going to use Exchange Setup to install the required Windows components (in the wizard or from the command line), run the following command in Windows PowerShell:

   ```PowerShell
   Enable-WindowsOptionalFeature -Online -FeatureName IIS-ManagementScriptingTools,IIS-ManagementScriptingTools,IIS-IIS6ManagementCompatibility,IIS-LegacySnapIn,IIS-ManagementConsole,IIS-Metabase,IIS-WebServerManagementTools,IIS-WebServerRole
   ```

::: moniker-end

::: moniker range="exchserver-2016"

## Exchange 2016 prerequisites for preparing Active Directory

You can use any member of the Active Directory domain to prepare Active Directory for Exchange 2016.

1. The computer requires the following software:

   a. [.NET Framework 4.8](https://download.visualstudio.microsoft.com/download/pr/014120d7-d689-4305-befd-3cb711108212/0fd66638cde16859462a6243a4629a50/ndp48-x86-x64-allos-enu.exe)

   b. [Visual C++ Redistributable Package for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=30679)

      > [!NOTE]
      >
      > - The system requirements for the Visual C++ redistributable package do not mention support for Windows Server 2016 or Windows Server 2019, but the redistributable package is safe to install on these versions of Windows.
      >
      > - An overview of the latest supported versions is available at: [Visual C++ Redistributable versions](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads).

2. Install the Remote Tools Administration Pack by running the following command in Windows PowerShell:

   ```PowerShell
   Install-WindowsFeature RSAT-ADDS
   ```

After you've installed the Remote Tools Administration Pack you can use the computer to prepare Active Directory. For more information, see [Prepare Active Directory and domains](prepare-ad-and-domains.md).

## Windows Server 2016 prerequisites for Exchange 2016

The prerequisites that are needed to install Exchange 2016 on computers running Windows Server 2016 depends on which Exchange role you want to install. Read the section below that matches the role you want to install.

> [!IMPORTANT]
> Windows Server 2016 requires Exchange 2016 Cumulative Update 3 or later.

### Exchange 2016 Mailbox servers on Windows Server 2016

1. Run the following command in Windows PowerShell to install the required Windows components:

   ```PowerShell
   Install-WindowsFeature NET-Framework-45-Features, Server-Media-Foundation, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Clustering-CmdInterface, RSAT-Clustering-Mgmt, RSAT-Clustering-PowerShell, WAS-Process-Model, Web-Asp-Net45, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext45, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, Windows-Identity-Foundation, RSAT-ADDS, BITS, BITS-IIS-Ext
   ```

2. Install the following software in order:

   a. [.NET Framework 4.8](https://download.visualstudio.microsoft.com/download/pr/014120d7-d689-4305-befd-3cb711108212/0fd66638cde16859462a6243a4629a50/ndp48-x86-x64-allos-enu.exe)

   b. [December 13, 2016 (KB3206632) security update](https://support.microsoft.com/help/4004227)

      > [!NOTE]
      > You can only install this update if your Windows Server 2016 version is 14393.576 or earlier (circa December, 2016). You can check your Windows Server version by running the **winver** command. If your Windows Server 2016 version is greater than 14393.576, you don't need this update or its replacement [KB3213522](https://support.microsoft.com/help/3213522), which was released one week later. Exchange 2016 Setup looks for the installation of this update, won't allow you to continue if this update is missing, and will clearly inform you if you need it.

   c. [Visual C++ Redistributable Package for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=30679)

   d. [Visual C++ Redistributable Package for Visual Studio 2013](https://support.microsoft.com/help/4032938)

      > [!NOTE]
      >
      > - The system requirements for the Visual C++ redistributable package do not mention support for Windows Server 2016 or Windows Server 2019, but the redistributable package is safe to install on these versions of Windows.
      >
      > - An overview of the latest supported versions is available at: [Visual C++ Redistributable versions](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads).
      >
      > - Only the Mailbox role requires the Visual C++ Redistributable Packages for Visual Studio **2013**. Other Exchange installations (management tools and Edge Transport) only require the Visual C++ Redistributable Packages for Visual Studio **2012**.

   e. [IIS URL Rewrite Module](https://www.iis.net/downloads/microsoft/url-rewrite)
   
      > [!NOTE]
      >
      > The IIS URL Rewrite Module is required with Cumulative Update 22 or later.

   f. [Microsoft Unified Communications Managed API 4.0, Core Runtime 64-bit](https://www.microsoft.com/download/details.aspx?id=34992)

### Exchange 2016 Edge Transport servers on Windows Server 2016

1. Run the following command in Windows PowerShell to install the required Windows components:

   ```PowerShell
   Install-WindowsFeature ADLDS
   ```

2. Install the following software in order:

   a. [.NET Framework 4.8](https://download.visualstudio.microsoft.com/download/pr/014120d7-d689-4305-befd-3cb711108212/0fd66638cde16859462a6243a4629a50/ndp48-x86-x64-allos-enu.exe)

   b. [Visual C++ Redistributable Package for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=30679)

      > [!NOTE]
      >
      > - The system requirements for the Visual C++ redistributable package do not mention support for Windows Server 2016 or Windows Server 2019, but the redistributable package is safe to install on these versions of Windows.
      >
      > - An overview of the latest supported versions is available at: [Visual C++ Redistributable versions](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads).

## Windows Server 2012 and Windows Server 2012 R2 prerequisites for Exchange 2016

The prerequisites for Exchange 2016 on Windows Server 2012 or Windows Server 2012 R2 computers depend on the Exchange role that you're installing. Read the following section that matches the role you want to install.

### Exchange 2016 Mailbox servers on Windows Server 2012 or Windows Server 2012 R2

1. Run the following command in Windows Powershell to install the required Windows components:

   ```PowerShell
   Install-WindowsFeature AS-HTTP-Activation, Server-Media-Foundation, NET-Framework-45-Features, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Clustering-CmdInterface, RSAT-Clustering-Mgmt, RSAT-Clustering-PowerShell, WAS-Process-Model, Web-Asp-Net45, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext45, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, Windows-Identity-Foundation, RSAT-ADDS
   ```

2. Install the following software in order:

   a. [.NET Framework 4.8](https://download.visualstudio.microsoft.com/download/pr/014120d7-d689-4305-befd-3cb711108212/0fd66638cde16859462a6243a4629a50/ndp48-x86-x64-allos-enu.exe)

   b. [Visual C++ Redistributable Package for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=30679)

   c. [Visual C++ Redistributable Package for Visual Studio 2013](https://support.microsoft.com/help/4032938/update-for-visual-c-2013-redistributable-package)

      > [!NOTE]
      >
      > - The system requirements for the Visual C++ redistributable package do not mention support for Windows Server 2016 or Windows Server 2019, but the redistributable package is safe to install on these versions of Windows.
      >
      > - An overview of the latest supported versions is available at: [Visual C++ Redistributable versions](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads).
      >
      > - Only the Mailbox role requires the Visual C++ Redistributable Packages for Visual Studio **2013**. Installations of the Exchange management tools and Edge Transport servers only require the Visual C++ Redistributable Packages for Visual Studio **2012**.

   d. [IIS URL Rewrite Module](https://www.iis.net/downloads/microsoft/url-rewrite)
   
      > [!NOTE]
      >
      > The IIS URL Rewrite Module is required with Cumulative Update 22 or later.

   e. [Update for Universal C Runtime in Windows (KB2999226)](https://support.microsoft.com/topic/update-for-universal-c-runtime-in-windows-c0514201-7fe6-95a3-b0a5-287930f3560c)

      > [!NOTE]
      >
      > The Update for Universal C Runtime in Windows (KB2999226) is required on Server 2012 R2 with Cumulative Update 22 or later.

   f. [Microsoft Unified Communications Managed API 4.0, Core Runtime 64-bit](https://www.microsoft.com/download/details.aspx?id=34992)

### Exchange 2016 Edge Transport servers on Windows Server 2012 or Windows Server 2012 R2

1. Run the following command in Windows PowerShell to install the required Windows components:

   ```PowerShell
   Install-WindowsFeature ADLDS
   ```

2. Install the following software in order:

   a. [.NET Framework 4.8](https://download.visualstudio.microsoft.com/download/pr/014120d7-d689-4305-befd-3cb711108212/0fd66638cde16859462a6243a4629a50/ndp48-x86-x64-allos-enu.exe)

   b. [Visual C++ Redistributable Package for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=30679)

      > [!NOTE]
      >
      > - The system requirements for the Visual C++ redistributable package do not mention support for Windows Server 2016 or Windows Server 2019, but the redistributable package is safe to install on these versions of Windows.
      >
      > - An overview of the latest supported versions is available at: [Visual C++ Redistributable versions](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads).

## Windows client prerequisites for the Exchange 2016 management tools

### Exchange 2016 management tools on Windows 10

1. Install [Visual C++ Redistributable Package for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=30679)

   > [!NOTE]
   >
   > - The system requirements for the Visual C++ redistributable package do not mention support for Windows Server 2016 or Windows Server 2019, but the redistributable package is safe to install on these versions of Windows.
   >
   > - An overview of the latest supported versions is available at: [Visual C++ Redistributable versions](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads).

2. Run the following command in an elevated Windows PowerShell window (a Windows PowerShell window you open by selecting **Run as administrator**):

   ```PowerShell
   Enable-WindowsOptionalFeature -Online -FeatureName IIS-ManagementScriptingTools,IIS-ManagementScriptingTools,IIS-IIS6ManagementCompatibility,IIS-LegacySnapIn,IIS-ManagementConsole,IIS-Metabase,IIS-WebServerManagementTools,IIS-WebServerRole
   ```

### Exchange 2016 management tools on Windows 8.1

1. Install [.NET Framework 4.8](https://download.visualstudio.microsoft.com/download/pr/014120d7-d689-4305-befd-3cb711108212/0fd66638cde16859462a6243a4629a50/ndp48-x86-x64-allos-enu.exe)

2. Install [Visual C++ Redistributable Package for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=30679)

   > [!NOTE]
   >
   > - The system requirements for the Visual C++ redistributable package do not mention support for Windows Server 2016 or Windows Server 2019, but the redistributable package is safe to install on these versions of Windows.
   >
   > - An overview of the latest supported versions is available at: [Visual C++ Redistributable versions](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads).

3. Run the following command in an elevated Windows PowerShell window (a Windows PowerShell window you open by selecting **Run as administrator**):

   ```PowerShell
   Enable-WindowsOptionalFeature -Online -FeatureName IIS-ManagementScriptingTools,IIS-ManagementScriptingTools,IIS-IIS6ManagementCompatibility,IIS-LegacySnapIn,IIS-ManagementConsole,IIS-Metabase,IIS-WebServerManagementTools,IIS-WebServerRole
   ```

::: moniker-end
