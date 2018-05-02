# Amazon Inspector Supported Operating Systems and Regions<a name="inspector_supported_os_regions"></a>

 Amazon Inspector evaluates the security state of the resources that constitute the assessment target\. 

**Important**  
At this time, your Amazon Inspector assessment targets can consist only of EC2 instances\. 

**Note**  
For information on how Amazon Inspector rules packages are available across supported operating systems that you can run on the EC2 instances included in your assessment targets, see [Rules Packages Availability Across Supported Operating Systems](inspector_rule-packages_across_os.md)\.

**Topics**
+ [Supported Linux\-based Operating Systems](#inspector_supported-linux-os)
+ [Supported Windows\-based Operating Systems](#inspector_supported-win-os)
+ [Supported Regions](#inspector_supported-regions)

## Supported Linux\-based Operating Systems<a name="inspector_supported-linux-os"></a>

In this release of Amazon Inspector, your assessment targets can consist only of EC2 instances that run the 64\-bit version of the following Linux\-based operating systems:
+ Amazon Linux \(2015\.03, 2015\.09, 2016\.03, 2016\.09, 2017\.03, 2017\.09\)
+ Amazon Linux 2 \(2017\.12\)
+ Ubuntu \(14\.04 LTS, 16\.04 LTS\)
+ Red Hat Enterprise Linux \(6\.2 \- 6\.9, 7\.2 \- 7\.4\)
+ CentOS \(6\.2 \- 6\.9, 7\.2 \- 7\.4\)

**Important**  
The following list contains all kernel versions that are compatible with the Amazon Inspector Agent running on Linux, Ubuntu, Red Hat Enterprise Linux, and CentOS: [https://s3\.amazonaws\.com/aws\-agent\.us\-east\-1/linux/support/supported\_versions\.json](https://s3.amazonaws.com/aws-agent.us-east-1/linux/support/supported_versions.json)\.  
You can run a successful Amazon Inspector assessment of an EC2 instance with a Linux\-based OS using either the CVE, CIS, or Security Best Practices rules packages even if your instance does not have a kernel version that is included in this list\.  
To run a successful Amazon Inspector assessment of an EC2 instance with a Linux\-based OS using the [Runtime Behavior Analysis](inspector_runtime-behavior-analysis.md) rules package, your instance must have a kernel version that is included in this list\. If your instance has a kernel version that is not compatible with the Amazon Inspector Agent, the Runtime Behavior Analysis rules package assessing that EC2 instance results in only one informational finding informing you that the kernel version of your EC2 instance is not supported\. 

## Supported Windows\-based Operating Systems<a name="inspector_supported-win-os"></a>

In this release of Amazon Inspector, your assessment targets can consist only of EC2 instances that run the 64\-bit version of the following Windows\-based operating systems:
+ Windows Server 2008 R2
+ Windows Server 2012
+ Windows Server 2012 R2
+ Windows Server 2016 Base

## Supported Regions<a name="inspector_supported-regions"></a>
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