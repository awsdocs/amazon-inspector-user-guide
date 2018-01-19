# Working with Amazon Inspector Agents on Linux\-based Operating Systems<a name="inspector_agents-on-linux"></a>

Sign in to your EC2 instance running a Linux\-based operating system, and run any of the following procedures\. For more information about operating systems supported for Amazon Inspector see [Amazon Inspector Supported Operating Systems and Regions](inspector_supported_os_regions.md)\.

**Note**  
The following commands are functional in all regions that are supported by Amazon Inspector\.


+ [To verify that the Amazon Inspector Agent is running](#verify-linux)
+ [To stop the Amazon Inspector Agent](#stop-linux)
+ [To start the Amazon Inspector Agent](#start-linux)
+ [To configure proxy support for Amazon Inspector Agents](#inspector-agent-proxy-linux)
+ [To uninstall the Amazon Inspector Agent](#uninstall-linux)

## To verify that the Amazon Inspector Agent is running<a name="verify-linux"></a>

+ To verify that the Amazon Inspector Agent is installed and running, sign in to your EC2 instance, and run the following command:

  sudo /opt/aws/awsagent/bin/awsagent status

  This command returns the status of the currently running agent, or an error stating that the agent cannot be contacted\.

## To stop the Amazon Inspector Agent<a name="stop-linux"></a>

+ To stop the agent, run sudo /etc/init\.d/awsagent stop

## To start the Amazon Inspector Agent<a name="start-linux"></a>

+ To start the agent, run sudo /etc/init\.d/awsagent start

## To configure proxy support for Amazon Inspector Agents<a name="inspector-agent-proxy-linux"></a>

Proxy support for Amazon Inspector Agents on Linux\-based operating systems is achieved by using an Amazon Inspector Agent specific configuration file with specific environment variables\. For more information, see [https://wiki\.archlinux\.org/index\.php/proxy\_settings](https://wiki.archlinux.org/index.php/proxy_settings)\.

Complete one of the following procedures:

**To install an Amazon Inspector Agent on an EC2 instance that uses a proxy server**

1. Create a file called `awsagent.env` and save it in the `/etc/init.d/` directory\.

1. Edit awsagent\.env to include these environment variables in the following format:

   + export https\_proxy=https://hostname:port

   + export http\_proxy=http://hostname:port

   + export no\_proxy=169\.254\.169\.254
**Note**  
Substitute example values above with valid URLs for `https_proxy` and `http_proxy` only\. You must specify the IP address of the instance metadata endpoint \(169\.254\.169\.254\) for the `no_proxy` variable\. 

1. Install the Amazon Inspector Agent by completing the steps in the [To install the Amazon Inspector Agent on a Linux\-based EC2 instance](inspector_installing-uninstalling-agents.md#install-linux) procedure\.

**To configure proxy support on an EC2 instance with a running Amazon Inspector Agent**

1. In order to configure proxy support, the version of the Amazon Inspector Agent that is running on your EC2 instance must be 1\.0\.800\.1 or higher\. If you have the auto\-update process for the Amazon Inspector Agent enabled, you can verify that your Amazon Inspector Agent's version is 1\.0\.800\.1 or higher by using the [To verify that the Amazon Inspector Agent is running](#verify-linux) procedure\. If you don't have the auto\-update process for the Amazon Inspector Agent enabled, you must install the agent on this EC2 instance again by following the [To install the Amazon Inspector Agent on a Linux\-based EC2 instance](inspector_installing-uninstalling-agents.md#install-linux) procedure\.

1. Create a file called `awsagent.env` and save it in the `/etc/init.d/` directory\.

1. Edit awsagent\.env to include these environment variables in the following format:

   + export https\_proxy=https://hostname:port

   + export http\_proxy=http://hostname:port

   + export no\_proxy=169\.254\.169\.254
**Note**  
Substitute example values above with valid URLs for `https_proxy` and `http_proxy` only\. You must specify the IP address of the instance metadata endpoint \(169\.254\.169\.254\) for the `no_proxy` variable\. 

1. Restart the Amazon Inspector Agent by first stopping it using `sudo /etc/init.d/awsagent restart`\.

   Proxy settings are picked up and used by both the Amazon Inspector Agent and the auto\-update process\.

## To uninstall the Amazon Inspector Agent<a name="uninstall-linux"></a>

1. Sign in to your EC2 instance running a Linux\-based operating system where you want to uninstall the Amazon Inspector Agent\.
**Note**  
For more information about operating systems supported for Amazon Inspector see [Amazon Inspector Supported Operating Systems and Regions](inspector_supported_os_regions.md)\.

1. To uninstall the agent, use one of the following commands:

   + On Amazon Linux, CentOS, and Red Hat, run sudo yum remove 'AwsAgent\*'

   + On Ubuntu Server, run sudo apt\-get purge 'awsagent\*'