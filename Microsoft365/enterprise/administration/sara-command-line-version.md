---
title: SaRA command-line version
description: Describes the command-line version of Microsoft Support and Recovery Assistant.
author: MaryQiu1987
ms.author: v-maqiu
manager: dcscontentpm
audience: ITPro
ms.topic: troubleshooting
localization_priority: Normal
ms.custom: 
  - CI 148047
  - CSSTroubleshoot
ms.reviewer: zebamehdi; brandisi
appliesto: 
  - Office 365
search.appverid: MET150
ms.date: 3/31/2022
---
# Command-line version of Microsoft Support and Recovery Assistant

The command-line version of Microsoft Support and Recovery Assistant (SaRA) is self-contained and scriptable (run at a command line or in a PowerShell script). This version is an enterprise-ready diagnostic tool for specific client issues. It is useful in situations in which administrators have to remotely run a diagnostic tool on computers in their organization.

## Download and run the command-line version of SaRA

1. Download SaRA by using the following link: [https://aka.ms/SaRA_CommandLineVersionFiles](https://aka.ms/SaRA_CommandLineVersionFiles)
1. In the downloaded file, extract the files in the *DONE* folder to a folder that you can access from the user's computer on which you will run SaRA.
1. On the user's computer, select **Start**, enter `cmd`, and then press Enter to open a Command Prompt window.

    **Note:** See the table in the "[Supported switches](#supported-switches)" section to determine whether an elevated Command Prompt window is required to run SaRA for the user's scenario.

1. In the Command Prompt window, navigate to the folder in which you extracted the files from step 2.
1. Run the command-line version of SaRA by using one or more switches that are discussed in the "[Supported switches](#supported-switches)" section.

   > [!IMPORTANT]
   > Updates to the command-line version of SaRA will be released on a regular basis. To make sure that you're using the latest version that has the most features and highest stability, each build of the application will stop working 90 days after the listed **Created** date for SaRAcmd.exe. Use the link provided in step 1 to download the latest version.

## Supported switches

The following switches are available to control SaRAcmd.exe.

**Note:** The switches aren't case-sensitive.

1. `-S <scenarioname>`

   Use the `-S` switch to specify the scenario that you want to run. The switch cannot be run on its own. It must be followed by `-AcceptEula`. For example, to run the scenario that removes the currently installed version of Office, enter `-S OfficeScrubScenario -AcceptEula`, and then press Enter.

   Currently, the following scenarios are supported through the command line.

   |*Scenarioname* value|Scenario entry point in the full (UI) version of SaRA|Elevated Command Prompt window required|
   |---|---|---|
   |`ExpertExperienceAdminTask`|Advanced Diagnostics \ Outlook|No|
   |`OfficeScrubScenario`|Office \ I have Office installed, but I'm having trouble uninstalling it|Yes|
   |`TeamsAddinScenario`|Teams \ The Teams Meeting option isn't shown, or the Teams Meeting add-in doesn't load in Outlook|No|
   |`OfficeActivationScenario`|Office \ I've installed a subscription version of Office, but I can't activate it|Yes|
   |`OutlookCalendarCheckTask`|Advance Diagnostics \ Outlook \ Create a detailed scan of my Outlook Calendar to identify and resolve issues|No|
   |`OfficeSharedComputerScenario`|Office \ I want to setup Office with shared computer activation on a computer or server in my organization|Yes|
   
   **Note:** To open an elevated Command Prompt window, select **Start**, enter `cmd`, right-click **Command Prompt** in the results, and then select **Run as administrator**.

2. `-CloseOutlook`

   The `-CloseOutlook` switch is required to run the TeamsAddinScenario.
   
   **Note**: If Outlook is running, this switch closes Outlook.
   
   ```console
   SaRAcmd.exe -S TeamsAddinScenario -AcceptEula -CloseOutlook
   ```

3. `-CloseOffice`

   The `-CloseOffice` switch is required to run the OfficeActivationScenario and OfficeSharedComputerScenario scenarios.
 
   **Note**: The `-CloseOffice` switch closes Office applications.
   
   ```console
   SaRAcmd.exe -S OfficeActivationScenario -AcceptEula -CloseOffice
   ```

4. `-AcceptEula`

   The End User License Agreement (EULA) must be accepted before a scenario can be run. If you're using `-AcceptEULA`, you must also use `-S <scenarioname>` to specify    the scenario that you want to run. For example, to uninstall Office, run the following command from an elevated Command Prompt window:

   ```console
   SaRAcmd.exe -S OfficeScrubScenario -AcceptEula
   ```

   If you want to run the Advanced Diagnostic scenario for Outlook, run the following command:

   ```console
   SaRAcmd.exe -S ExpertExperienceAdminTask -AcceptEula
   ```

5. `-DisplayEULA`

   Use the `-DisplayEULA` switch to display the EULA. To save the EULA text to a file, run a command that resembles the following example:

   ```console
   SaRAcmd.exe -DisplayEULA > c:\temp\SaRAEula.txt
   ```
   
6. `-LogFolder <Output Path>`

   The `-LogFolder` switch is optional for the ExpertExperienceAdminTask and OutlookCalendarCheckTask scenarios. If the `-LogFolder` switch is used, it forces SaraCmd.exe to output scenario-specific logs to the folder that's specified by \<Output Path\>.
  
7. `-P <Profile Name>`
  
   The `-P` switch is optional for the OutlookCalendarCheckTask scenario. \<Profile name\> is the Outlook profile that's scanned by the OutlookCalendarCheckTask scenario.
  
8. `RemoveSCA`
  
   The `-RemoveSCA` switch is optional for OfficeActivationScenario and OfficeSharedComputerScenario. This switch removes Shared Computer Activation (SCA) and configures non-SCA activation for Office.
  
9. `-HideProgress`
  
   The `-HideProgress` switch is optional and only works with the ExpertExperienceTask and OutlookCalendarCheckTask scenarios. The default feature is to always show progress. When this switch is used, it hides the progress display for the ExpertExperienceTask and OutlookCalendarCheckTask scenarios.
  
10. `-OfflineScan`
  
    The `-OfflineScan` switch is optional and only works with the ExpertExperienceAdminTask scenario. This switch forces the scan of Outlook to be an Offline scan when the Outlook application is running. 
  
11. `-OfficeVersion`
  
    The `-OfficeVersion` switch is optional and works only with the OfficeScrubScenario scenario. Using this switch only removes the Office version that's defined in   the parameter. If you use **All** as a parameter, it removes all Office versions from your machine. For example, to uninstall only Office 2016 version, run the following command from an elevated Command Prompt window:
  
  ```console
  SaRAcmd.exe -S OfficeScrubScenario -AcceptEula -Officeversion 2016
  ```
  
 To uninstall all Office versions,  run the following command from an elevated Command Prompt window:
 
 ```console
 SaRAcmd.exe -S OfficeScrubScenario -AcceptEula -Officeversion All
  ```
   
12. `-Help`

    The `-Help` switch displays a link to online content for additional information. If you use `-Help` together with other switches, `-Help` will override all the other  switches except the `-?` switch.

13. `-?`

    Use the `-?` switch to display the functions of all the switches that are available for SaRAcmd.exe. If you use `-?` together with other switches, `-?` will override the other switches.

## Conditions addressed by the command-line scenarios

When you run a scenario by using the command-line version of SaRA, you receive no prompts. This is a different experience from the full version of SaRA. The following table describes the actions that the command-line version of SaRA takes, and the output that the tool displays for each condition within a scenario.

- `ExpertExperienceAdminTask`

  |Condition|Action taken by the command-line version|Output in the Command Prompt window|
  |---|---|---|
  |Outlook isn't running|Run an Offline scan of Outlook|*01:* An Offline scan was performed because Outlook is either not running or it is running elevated (as Administrator). See \<filename> in *%localappdata%\saralogs\UploadLogs*.|
  |Outlook is running|Run a full scan of Outlook|*02:* A Full scan was performed. See \<filename> in *%localappdata%\saralogs\UploadLogs*.|
  |More than one Outlook version is detected|Run a scan of the latest version of Outlook|(Depending on the situation, this output could be *01*, *02*, *04*, or *05*)|
  |Outlook and the Command Prompt window are both elevated|Run a full scan of Outlook|*02:* A Full scan was performed. See \<filename> in *%localappdata%\saralogs\UploadLogs*.|
  |Outlook is running as elevated; the SaRA Command Prompt window isn't elevated|Run an Offline scan of Outlook|*01:* An Offline scan was performed because Outlook is either not running or it is running elevated (as Administrator). See \<filename> in *%localappdata%\saralogs\UploadLogs*.|
  |Outlook isn't running as elevated; the SaRA Command Prompt window is elevated|None|*04:* Outlook isn't running elevated. Don't use an elevated command-prompt.|
  |Failure to run a scan (for any reason); for example:<ol><li>Outlook isn't installed</li><li>Only one Outlook version is detected, and that version is earlier than 2007</li><li>An exception occurs during the scan</li></ol>|Scan initiated but not completed|*05:* An error occurred while performing a scan of Outlook. You might be able to perform an Offline scan if you exit Outlook and rerun this scenario. You can also try using the full SaRA version.|

- `OfficeScrubScenario`

  |Condition|Action taken by the command-line version|Output shown in the command-prompt window|
  |---|---|---|
  |Office removed successfully|None|*00:* Successfully completed this scenario.</br></br>**Note:** We recommend you restart the computer to finish any remaining cleanup tasks.|
  |Office program found .exe files running:</br></br>lync, winword, excel, msaccess, mstore, infopath, setlang, msouc, ois, onenote, outlook, powerpnt, mspub, groove, visio, winproj, graph, teams|Exit the scenario|*06:* Office programs are running. Please close all open Office programs and then rerun this scenario.|
  |No Office products found|Exit the scenario|*07:* No installed Office versions were found. Please use the full SaRA version.|
  |Multiple Office products found|Exit the scenario|*08:* Multiple Office versions were found. Please use the full SaRA version.|
  |Failure to remove Office|Exit the scenario|*09:* Failure to remove Office. Please use the full SaRA version.|
  |SaRA isn't elevated|Exit the scenario|*10:* SaRA needs to run elevated for this scenario. Please use an elevated command-prompt.|
  
- `TeamsAddinScenario`

  |Condition|Action taken by the command-line version|Output shown in the command-prompt window|
  |---|---|---|
  |Scan completed successfully|None|*00:* Scenario completed successfully. Please exit and restart Outlook.|
  |User doesn't include the `-CloseOutlook` switch|Exit the scenario|*01:* This scenario requires the -CloseOutlook switch. Note, if Outlook is running, the -CloseOutlook switch closes Outlook. For additional information, please visit [https://aka.ms/SaRA_CommandLineVersion](https://aka.ms/SaRA_CommandLineVersion)|
  |User doesn't include the `-AcceptEula` switch|Exit the scenario|*01:* Please provide -AcceptEula to continue with this scenario. For additional information, please visit [https://aka.ms/SaRA_CommandLineVersion](https://aka.ms/SaRA_CommandLineVersion)|
  |Teams isn't installed|Exit the scenario|*20:* Could not find an installed version of Teams. Please see [https://support.office.com/article/how-do-i-get-access-to-microsoft-teams-fc7f1634-abd3-4f26-a597-9df16e4ca65b](https://support.office.com/article/how-do-i-get-access-to-microsoft-teams-fc7f1634-abd3-4f26-a597-9df16e4ca65b)|
  |Outlook 2013 or later isn't installed|Exit the scenario|*21:* Could not find an installed version of Outlook 2013, or later. See [https://go.microsoft.com/fwlink/?linkid=2129032](https://go.microsoft.com/fwlink/?linkid=2129032)|
  |Windows 7 users don't have the [Update for Universal C Runtime in Windows](https://support.microsoft.com/help/2999226/update-for-universal-c-runtime-in-windows) installed|Exit the scenario|*22:* Pre-requisites not met. Update from KB2999226 needs to be installed. See [https://go.microsoft.com/fwlink/?linkid=2129032](https://go.microsoft.com/fwlink/?linkid=2129032)|
  |Registry issues detected: <br/><br/>LoadBehavior<>3 or add-in listed under the `DisabledItems` key or TeamsAddin.Connect <> 1 under the `DoNotDisableAddinList` key|Run the registry recovery action, and then exit the scenario.|*23:* The registry was updated to address missing or incorrect values. Please exit and restart Outlook.</br></br>*17:* An error occurred while running this scenario. You can also try using the full SaRA version.|
  |None of the above conditions were detected|Run the re-register dll recovery action, and then exit the scenario.|*24:* The Microsoft.Teams.AddinLoader.dll was re-registered. Please exit and restart Teams. Then, exit and restart Outlook.|
  |Failure to complete the scenario (for any reason)|Exit the scenario|*17:* An error occurred while running this scenario. You can also try using the full SaRA version.|
  
## SaRA command-line version history

Throughout the year, a new build of SaRA is available through the download link that is provided at the beginning of this article. Because each build stops working after 90 days, we recommend that you keep SaRA updated by replacing the files you have with the latest version.

The following table provides the versions of SaRA that were made available on the specified date.

|Release date|SaRACmd.exe version|
|--------|--------|
|Apr 7, 2022|17.00.8256.000|
|Feb 8, 2022|17.00.7971.000|
|Nov 9, 2021|17.00.7513.000|
|May 26, 2021|17.00.6665.000|

For more information about the full version of SaRA, see [About the Microsoft Support and Recovery Assistant](https://aka.ms/sara_home).
