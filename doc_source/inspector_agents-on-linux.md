# Working with Amazon Inspector Agents on Linux\-based Operating Systems<a name="inspector_agents-on-linux"></a>

You can install, remove, verify, and modify the behavior of Amazon Inspector agents\. Sign in to your Amazon EC2 instance running a Linux\-based operating system, and run any of the following procedures\. For more information about the operating systems that are supported for Amazon Inspector, see [Amazon Inspector Supported Operating Systems and Regions](inspector_supported_os_regions.md)\.

**Note**  
The commands in this section function in all AWS Regions that are supported by Amazon Inspector\.

**Topics**
+ [Verifying That the Amazon Inspector Agent is Running](#verify-linux)
+ [Stopping the Amazon Inspector Agent](#stop-linux)
+ [Starting the Amazon Inspector Agent](#start-linux)
+ [Modifying Amazon Inspector Agent Settings](#inspector-agent-modify-settings-linux)
+ [Configuring Proxy Support for an Amazon Inspector Agent](#inspector-agent-proxy-linux)
+ [Uninstalling the Amazon Inspector Agent](#uninstall-linux)

## Verifying That the Amazon Inspector Agent is Running<a name="verify-linux"></a>
+ To verify that the agent is installed and running, sign in to your EC2 instance and run the following command:

  sudo /opt/aws/awsagent/bin/awsagent status

  This command returns the status of the currently running agent, or an error stating that the agent cannot be contacted\.

## Stopping the Amazon Inspector Agent<a name="stop-linux"></a>
+ To stop the agent, run the following command:

  sudo /etc/init\.d/awsagent stop

## Starting the Amazon Inspector Agent<a name="start-linux"></a>
+ To start the agent, run the following command:

  sudo /etc/init\.d/awsagent start

## Modifying Amazon Inspector Agent Settings<a name="inspector-agent-modify-settings-linux"></a>

After the Amazon Inspector agent is installed and running on your EC2 instance, you can modify the settings in the `agent.cfg` file to alter the agent's behavior\. On Linux\-based operating systems, the `agent.cfg` file is located in the `/opt/aws/awsagent/etc` directory\. After you modify and save the `agent.cfg` file, you must stop and start the agent for the changes to take effect\.

**Important**  
We highly recommend that you modify the `agent.cfg` file only with the guidance of AWS Support\.

## Configuring Proxy Support for an Amazon Inspector Agent<a name="inspector-agent-proxy-linux"></a>

To get proxy support for an agent on a Linux\-based operating system, use an agent\-specific configuration file with specific environment variables\. For more information, see [https://wiki\.archlinux\.org/index\.php/proxy\_settings](https://wiki.archlinux.org/index.php/proxy_settings)\.

Complete one of the following procedures:

**To install an agent on an EC2 instance that uses a proxy server**

1. Create a file called `awsagent.env` and save it in the `/etc/init.d/` directory\.

1. Edit `awsagent.env` to include these environment variables in the following format:
   + `export https_proxy=hostname:port`
   + `export http_proxy=hostname:port`
   + `export no_proxy=169.254.169.254`
**Note**  
Substitute values in the preceding examples with valid hostname and port number combinations only\. Specify the IP address of the instance metadata endpoint \(169\.254\.169\.254\) for the `no_proxy` variable\. 

1. Install the Amazon Inspector agent by completing the steps in the [Installing the Agent on a Linux\-based EC2 Instance](inspector_installing-uninstalling-agents.md#install-linux) procedure\.

**To configure proxy support on an EC2 instance with a running agent**

1. To configure proxy support, the version of the agent that is running on your EC2 instance must be 1\.0\.800\.1 or later\. If you enabled the auto\-update process for the agent, you can verify that your agent's version is 1\.0\.800\.1 or later by using the [Verifying That the Amazon Inspector Agent is Running](#verify-linux) procedure\. If you didn't enable the auto\-update process for the agent, you must install the agent on this EC2 instance again by following the [Installing the Agent on a Linux\-based EC2 Instance](inspector_installing-uninstalling-agents.md#install-linux) procedure\.

1. Create a file called `awsagent.env`, and save it in the `/etc/init.d/` directory\.

1. Edit `awsagent.env` to include these environment variables in the following format:
   + `export https_proxy=hostname:port`
   + `export http_proxy=hostname:port`
   + `export no_proxy=169.254.169.254`
**Note**  
Substitute values in the preceding examples with valid hostname and port number combinations only\. Specify the IP address of the instance metadata endpoint \(169\.254\.169\.254\) for the `no_proxy` variable\. 

1. Restart the agent by first stopping it using the following command:

   `sudo /etc/init.d/awsagent restart`

   Proxy settings are picked up and used by both the agent and the auto\-update process\.

## Uninstalling the Amazon Inspector Agent<a name="uninstall-linux"></a>

**To uninstall the agent**

1. Sign in to your EC2 instance running a Linux\-based operating system where you want to uninstall the agent\.
**Note**  
For more information about the operating systems that are supported for Amazon Inspector, see [Amazon Inspector Supported Operating Systems and Regions](inspector_supported_os_regions.md)\.

1. To uninstall the agent, use one of the following commands:
   + On Amazon Linux, CentOS, and Red Hat, run the following command:

     sudo yum remove 'AwsAgent\*'
   + On Ubuntu Server, run the following command:

     sudo apt\-get purge 'awsagent\*'