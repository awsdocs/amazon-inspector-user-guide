# Working with Amazon Inspector Agents on Windows\-based Operating Systems<a name="inspector_agents-on-win"></a>

Sign in to your EC2 instance running a Windows\-based operating system and run any of the following procedures\. For more information about operating systems supported for Amazon Inspector see [Amazon Inspector Supported Operating Systems and Regions](inspector_supported_os_regions.md)\.

**Note**  
The following commands are functional in all regions that are supported by Amazon Inspector\.

**Topics**
+ [To stop or start the Amazon Inspector Agent or verify that the Amazon Inspector Agent is running](#stop-start-windows)
+ [To modify Amazon Inspector Agent settings](#inspector-agent-modify-settings)
+ [To configure proxy support for Amazon Inspector Agents](#inspector-agent-proxy)
+ [To uninstall the Amazon Inspector Agent](#uninstall-windows)

## To stop or start the Amazon Inspector Agent or verify that the Amazon Inspector Agent is running<a name="stop-start-windows"></a>

1. On your EC2 instance, choose **Start**, then **Run**, and then type **services\.msc**\.

1. If the agent is successfully running, two services are listed with their status set to **Started** or **Running** in the Services Window: **AWS Agent Service** and **AWS Agent Updater Service**\.

1. To start the agent, right\-click **AWS Agent Service** and then choose **Start**\. If the service is successfully started, the status is updated to **Started** or **Running**\.

1. To stop the agent, right\-click **AWS Agent Service** and choose **Stop**\. If the service is successfully stopped, the status is cleared \( appears as blank\)\. We do not recommend stopping the **AWS Agent Updater Service** as it will disable the installation of all future enhancements and fixes to the Amazon Inspector Agent\.

1. To verify that the Amazon Inspector Agent is installed and running, sign in to your EC2 instance, open a command prompt with Administrative permissions, navigate to C:/Program Files/Amazon Web Services/AWS Agent, and then run the following command:

   AWSAgentStatus\.exe

   This command returns the status of the currently running agent, or an error stating that the agent cannot be contacted\.

## To modify Amazon Inspector Agent settings<a name="inspector-agent-modify-settings"></a>

Once the Amazon Inspector Agent is installed and running on your EC2 instance, you can modify the settings in the **agent\.cfg file** to alter the agent's behavior\. The **agent\.cfg** file is located in the **/opt/aws/awsagent/etc** directory on Linux\-based operating systems and in the **C:\\ProgramData\\Amazon Web Services\\AWS Agent** directory on Windows\-based operating systems After you modify and save the **agent\.cfg file**, you must stop and start the agent in order for the changes to take effect\.

**Important**  
We highly recommend that you modify the **agent\.cfg** file only with the guidance of AWS Support\.

## To configure proxy support for Amazon Inspector Agents<a name="inspector-agent-proxy"></a>

Proxy support for Amazon Inspector Agents is achieved through the use of the WinHTTP proxy\. To set up WinHTTP proxy using the `netsh` utility see: [https://technet\.microsoft\.com/en\-us/library/cc731131%28v=ws\.10%29\.aspx](https://technet.microsoft.com/en-us/library/cc731131%28v=ws.10%29.aspx)\.

Complete one of the following procedures:

**To install an Amazon Inspector Agent on an EC2 instance that uses a proxy server**

1. Download the following \.exe file: `https://d1wk0tztpsntt1.cloudfront.net/windows/installer/latest/AWSAgentInstall.exe`

1. Open a command prompt window or PowerShell window \(with Administrative permissions\), navigate to the location where you saved the downloaded AWSAgentInstall\.exe, and run the following command:

   `./AWSAgentInstall.exe \install USEPROXY=1`

**To configure proxy support on an EC2 instance with a running Amazon Inspector Agent**

1. In order to configure proxy support, the version of the Amazon Inspector Agent that is running on your EC2 instance must be 1\.0\.0\.59 or higher\. If you have the auto\-update process for the Amazon Inspector Agent enabled, you can verify that your Amazon Inspector Agent's version is 1\.0\.0\.59 or higher by using the [To stop or start the Amazon Inspector Agent or verify that the Amazon Inspector Agent is running](#stop-start-windows) procedure\. If you don't have the auto\-update process for the Amazon Inspector Agent enabled, you must install the agent on this EC2 instance again by following the [To install the Amazon Inspector Agent on a Windows\-based EC2 instance](inspector_installing-uninstalling-agents.md#install-windows) procedure\.

1. Open the registry editor \(regedit\.exe\)\.

1. Navigate to the following Registry key `"HKEY_LOCAL_MACHINE/SOFTWARE/Amazon Web Services/AWS Agent Updater"`\.

1. Inside this registry key, create a registry DWORD\(32bit\) value called `"UseProxy"`\.

1. Double click on the value and set the value to 1\.

1. Type `services.msc`, locate the **AWS Agent Service** and the **AWS Agent Updater Service** in the Services Window, and restart each process\. After both processes have successfully restarted, run `AWSAgentStatus.exe` \(see Step 5 in [To stop or start the Amazon Inspector Agent or verify that the Amazon Inspector Agent is running](#stop-start-windows)\) to view the status of your Amazon Inspector Agent and verify that it is using the configured proxy\.

## To uninstall the Amazon Inspector Agent<a name="uninstall-windows"></a>

1. Sign in to your EC2 instance running a Windows\-based operating system where you want to uninstall the Amazon Inspector Agent\.
**Note**  
For more information about operating systems supported for Amazon Inspector see [Amazon Inspector Supported Operating Systems and Regions](inspector_supported_os_regions.md)\.

1. On your EC2 instance, navigate to **Control Panel**, **Add/Remove Programs\.**

1. In the list of installed programs, choose **AWS Agent**, and then choose **Uninstall**\.