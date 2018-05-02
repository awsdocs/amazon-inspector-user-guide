# Amazon Inspector Agents<a name="inspector_agents"></a>

To assess the security of the EC2 instances that make up your Amazon Inspector assessment targets, you must install the Amazon Inspector Agent on each instance\. The agent monitors the behavior \(including network, file system, and process activity\) of the EC2 instance on which it is installed, collects behavior and configuration data \(telemetry\), and then passes the data to the Amazon Inspector service\.

For more information about how to install, uninstall, and reinstall the Amazon Inspector Agent, how to verify whether the installed agent is running, and how to configure proxy support for the Amazon Inspector Agents, see [Working with Amazon Inspector Agents on Linux\-based Operating Systems](inspector_agents-on-linux.md) and [Working with Amazon Inspector Agents on Windows\-based Operating Systems](inspector_agents-on-win.md)\.

**Topics**
+ [Amazon Inspector Agent Privileges](#agent-privileges)
+ [Network and Amazon Inspector Agent Security](#agent-security)
+ [Amazon Inspector Agent Updates](#agent-updates)
+ [Telemetry Data Lifecycle](#telemetry-data-lifecycle)
+ [Access Control from Amazon Inspector into AWS Accounts](#access-control)
+ [Amazon Inspector Agent Limits](#agent-limits)
+ [Amazon Inspector Agent Public Licensing](#agent-license)
+ [Installing Amazon Inspector Agents](inspector_installing-uninstalling-agents.md)
+ [Working with Amazon Inspector Agents on Linux\-based Operating Systems](inspector_agents-on-linux.md)
+ [Working with Amazon Inspector Agents on Windows\-based Operating Systems](inspector_agents-on-win.md)
+ [\(Optional\) Verify the Signature of the Amazon Inspector Agent Installation Script on Linux\-based Operating Systems](inspector_verify-sig-agent-download-linux.md)
+ [\(Optional\) Verify the Signature of the Amazon Inspector Agent Installation Script on Windows\-based Operating Systems](inspector_verify-sig-agent-download-win.md)

## Amazon Inspector Agent Privileges<a name="agent-privileges"></a>

Administrative or root permissions are required to install the Amazon Inspector Agent\. On supported Linux\-based operating systems, the Amazon Inspector Agent consists of a user mode executable that runs with root access and a kernel module that is required for the agent to function\. On supported Windows\-based operating systems, the agent consists of an updater service and an agent service, each running in user mode with LocalSystem privileges, and a kernel mode driver that is required for the agent to function\.

**Important**  
The following list contains all kernel versions that are compatible with the Amazon Inspector Agent running on Linux, Ubuntu, Red Hat Enterprise Linux, and CentOS: [https://s3\.amazonaws\.com/aws\-agent\.us\-east\-1/linux/support/supported\_versions\.json](https://s3.amazonaws.com/aws-agent.us-east-1/linux/support/supported_versions.json)\.  
You can run a successful Amazon Inspector assessment of an EC2 instance with a Linux\-based OS using either the CVE, CIS, or Security Best Practices rules packages even if your instance does not have a kernel version that is included in this list\.  
To run a successful Amazon Inspector assessment of an EC2 instance with a Linux\-based OS using the [Runtime Behavior Analysis](inspector_runtime-behavior-analysis.md) rules package, your instance must have a kernel version that is included in this list\. If your instance has a kernel version that is not compatible with the Amazon Inspector Agent, the Runtime Behavior Analysis rules package assessing that EC2 instance results in only one informational finding informing you that the kernel version of your EC2 instance is not supported\. 

## Network and Amazon Inspector Agent Security<a name="agent-security"></a>

All communication between the Amazon Inspector Agent and Amazon Inspector is initiated by the Amazon Inspector Agent\. As such, the agent must have an outbound network path to the public endpoint for sending telemetry data from the Amazon Inspector Agent \(arsenal\.<region>\.amazonaws\.com\) and Amazon S3 services \(s3\.dualstack\.aws\-region\.amazonaws\.com\)\. \(Make sure to replace <region> with the actual AWS region where you have Amazon Inspector running\.\) For more information, see [AWS IP Address Ranges](http://docs.aws.amazon.com/general/latest/gr/aws-ip-ranges.html)\. Additionally, as all connections from the agent are established outbound, it is not necessary to open ports in your security groups to allow inbound communications to the agent from Amazon Inspector\. 

The Amazon Inspector Agent periodically communicates with Amazon Inspector over a TLS\-protected channel which is authenticated using either the AWS identity associated with the role of the EC2 instance, if present, or with the instance metadata document if no role is assigned to the instance\. Once authenticated, the agent sends heartbeat messages to the service and receives instructions from the service as responses to the heartbeat messages\. If an assessment has been scheduled, the agent receives the instructions for that assessment\. These instructions are structured JSON files and tell the agent to enable or disable specific pre\-configured sensors in the agent\. Each instruction action is pre\-defined within the agent and arbitrary instructions cannot be executed\. 

During an assessment, the agent gathers telemetry data from the system to send back to Amazon Inspector over a TLS\-protected channel\. The agent does not make changes to the system that it collects data from\. Once collected, the agent sends the telemetry data back to Amazon Inspector for processing\. Beyond the telemetry data that it generates, the agent is not capable of collecting or transmitting any other data about the system or assessment targets that it is assessing\. At present, there is no method exposed for intercepting and examining telemetry data at the agent\.

## Amazon Inspector Agent Updates<a name="agent-updates"></a>

As updates for the Amazon Inspector Agent become available, they are automatically downloaded from Amazon S3 and applied\. This will also update any required dependencies\. The auto\-update feature eliminates the need for you to track and manually maintain the versioning of the agents that you have installed on your EC2 instances\. All updates are subject to audited Amazon change control processes to ensure compliance with applicable security standards\. To further ensure the security of the agent, all communication between the agent and the auto\-update release site \(S3\) are performed over a TLS connection, and the server is authenticated\. All binaries involved in the auto\-update process are digitally signed and the signatures are verified by the updater prior to installation\. The auto\-update process is executed only during non\-assessment periods, and the update process has the ability to rollback and retry the update if any errors are detected\. Finally, the agent update process serves to only upgrade the agent capabilities, and none of your specific information is ever sent from the agent to Amazon Inspector as part of the update workflow\. The only information communicated as part of the update process is the basic installation success/fail telemetry and, if applicable, any update failure diagnostic information\. 

## Telemetry Data Lifecycle<a name="telemetry-data-lifecycle"></a>

The telemetry data generated by the Amazon Inspector Agent during assessment runs is formatted in JSON files and delivered in near\-real\-time over TLS to Amazon Inspector, where it is encrypted with a per\-assessment\-run, ephemeral KMS\-derived key and securely stored in an S3 bucket dedicated for Amazon Inspector\. The rules engine of Amazon Inspector's accesses the encrypted telemetry data in the S3 bucket, decrypts it in memory, and processes the data against the configured assessment rules to generate findings\. The telemetry data stored in S3 is retained only to allow for assistance with support requests and is not used or aggregated by Amazon for any other purpose\. After 30 days, telemetry data is permanently deleted per a standard Amazon Inspector\-dedicated S3 bucket lifecycle policy\. At present, Amazon Inspector does not provide an API or an S3 bucket access mechanism to collected telemetry\. 

## Access Control from Amazon Inspector into AWS Accounts<a name="access-control"></a>

As a security service, Amazon Inspector accesses your AWS accounts and resources only when it needs to find EC2 instances to assess by querying for tags\. It does this through standard IAM access by the role created during the initial setup of the Amazon Inspector service\. During an assessment, all communications with your environment are initiated by the Amazon Inspector Agent that is installed locally on EC2 instances\. The Amazon Inspector service objects that are created, such as assessment targets, assessment templates, and findings generated by the service, are stored in a database managed by and accessible only to Amazon Inspector\. 

## Amazon Inspector Agent Limits<a name="agent-limits"></a>

For information about Amazon Inspector Agent limits, see [Amazon Inspector Service Limits](inspector_limits.md)\.

## Amazon Inspector Agent Public Licensing<a name="agent-license"></a>

The Amazon Inspector Agent used in conjunction with Amazon Inspector, utilizes a Kernel module \(amznmon64\) as a component of the overall agent\. This Kernel module uses a general public license \([GPLv2](https://www.gnu.org/licenses/gpl-2.0.html)\)\. The module source code and licensing information are publicly available and can be accessed at: 
+ Source code: [https://s3\.amazonaws\.com/aws\-agent\.us\-east\-1/linux/support/AwsAgentKernelModule\.tar\.gz](https://s3.amazonaws.com/aws-agent.us-east-1/linux/support/AwsAgentKernelModule.tar.gz)
+ Signature file: [https://s3\.amazonaws\.com/aws\-agent\.us\-east\-1/linux/support/AwsAgentKernelModule\.tar\.gz\.sig](https://s3.amazonaws.com/aws-agent.us-east-1/linux/support/AwsAgentKernelModule.tar.gz.sig)