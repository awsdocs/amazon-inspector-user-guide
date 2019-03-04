# Amazon Inspector Supported Operating Systems and Regions<a name="inspector_supported_os_regions"></a>

This chapter provides information about the operating systems and AWS Regions that Amazon Inspector supports\.

**Important**  
Currently, Amazon Inspector assessment targets can consist only of EC2 instances\. You can run an agentless assessment with the [Network Reachability](inspector_network-reachability.md) rules package on any EC2 instances regardless of operating system\.

For information about the Amazon Inspector rules packages that are available across supported operating systems, see [Amazon Inspector Rules Packages for Supported Operating Systems](inspector_rule-packages_across_os.md)\.

**Topics**
+ [Supported Linux\-based Operating Systems for the Amazon Inspector Agent](#inspector_supported-linux-os)
+ [Supported Windows\-based Operating Systems for the Amazon Inspector Agent](#inspector_supported-win-os)
+ [Supported AWS Regions](#inspector_supported-regions)

## Supported Linux\-based Operating Systems for the Amazon Inspector Agent<a name="inspector_supported-linux-os"></a>

You can use the Amazon Inspector agent on EC2 instances that run the 64\-bit x86 and [Arm](https://aws.amazon.com/ec2/instance-types/a1/) versions of the following Linux\-based operating systems:
+ Amazon Linux 2 \(LTS, 2017\.12\)
+ Amazon Linux \(2018\.03, 2017\.09, 2017\.03, 2016\.09, 2016\.03, 2015\.09, 2015\.03, 2014\.09, 2014\.03, 2013\.09, 2013\.03, 2012\.09, 2012\.03\)
+ Ubuntu \(18\.04 LTS, 16\.04 LTS, 14\.04 LTS\)
+ Debian \(9\.0 \- 9\.5, 8\.0 \- 8\.7\)
+ Red Hat Enterprise Linux \(7\.2 \- 7\.6, 6\.2 \- 6\.9\)
+ CentOS \(7\.2 \- 7\.6, 6\.2 \- 6\.9\)

**Important**  
The following list contains all kernel versions that are compatible with an Amazon Inspector agent running on Linux, Ubuntu, Red Hat Enterprise Linux, and CentOS: [https://s3\.amazonaws\.com/aws\-agent\.us\-east\-1/linux/support/supported\_versions\.json](https://s3.amazonaws.com/aws-agent.us-east-1/linux/support/supported_versions.json)\.  
You can run a successful assessment of an EC2 instance with a Linux\-based OS using either the [CVE](inspector_cves.md), [CIS](inspector_cis.md), or [Security Best Practices](inspector_security-best-practices.md) rules packages\. The assessment is successful even if your instance doesn't have a kernel version that is included in this list\.  
To run a successful assessment of an EC2 instance with a Linux\-based OS using the [Runtime Behavior Analysis](inspector_runtime-behavior-analysis.md) rules package, your instance must have a kernel version that is included in this list\. If your instance has a kernel version that is not compatible with the agent, the Runtime Behavior Analysis rules package that assesses the EC2 instance results in only one finding\. The finding informs you that the kernel version of your EC2 instance is not supported\. 

## Supported Windows\-based Operating Systems for the Amazon Inspector Agent<a name="inspector_supported-win-os"></a>

You can use the Amazon Inspector agent only on EC2 instances that run the 64\-bit version of the following Windows\-based operating systems:
+ Windows Server 2008 R2
+ Windows Server 2012
+ Windows Server 2012 R2
+ Windows Server 2016 Base

## Supported AWS Regions<a name="inspector_supported-regions"></a>

Amazon Inspector is supported in the following AWS Regions:
+ Asia Pacific \(Mumbai\)
+ Asia Pacific \(Seoul\)
+ Asia Pacific \(Sydney\)
+ Asia Pacific \(Tokyo\)
+ EU \(Frankfurt\)
+ EU \(Ireland\)
+ US East \(Northern Virginia\)
+ US East \(Ohio\)
+ US West \(Northern California\)
+ US West \(Oregon\)
+ AWS GovCloud \(US\-East\)
+ AWS GovCloud \(US\-West\)

**Note**  
The [Network Reachability](inspector_network-reachability.md) rules package is not available in the AWS GovCloud \(US\) Regions\.