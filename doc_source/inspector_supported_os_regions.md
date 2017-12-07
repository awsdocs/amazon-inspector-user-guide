# Amazon Inspector Supported Operating Systems and Regions<a name="inspector_supported_os_regions"></a>

 Amazon Inspector evaluates the security state of the resources that constitute the assessment target\. 

**Important**  
At this time, your Amazon Inspector assessment targets can consist only of EC2 instances\. 

**Note**  
For information on how Amazon Inspector rules packages are available across supported operating systems that you can run on the EC2 instances included in your assessment targets, see [Rules Packages Availability Across Supported Operating Systems](inspector_rule-packages_across_os.md)\.


+ [Supported Linux\-based Operating Systems](#inspector_supported-linux-os)
+ [Supported Windows\-based Operating Systems](#inspector_supported-win-os)
+ [Supported Regions](#inspector_supported-regions)

## Supported Linux\-based Operating Systems<a name="inspector_supported-linux-os"></a>

In this release of Amazon Inspector, your assessment targets can consist only of EC2 instances that run the 64\-bit version of the following Linux\-based operating systems:

+ Amazon Linux \(2015\.03, 2015\.09, 2016\.03, 2016\.09, 2017\.03, 2017\.09\)

+ Ubuntu \(14\.04 LTS, 16\.04 LTS\)

+ Red Hat Enterprise Linux \(6\.2 \- 6\.9, 7\.2 \- 7\.4\)

+ CentOS \(6\.2 \- 6\.9, 7\.2 \- 7\.4\)

**Important**  
Follow this link to view a list of kernel versions that are compatible with the Amazon Inspector Agent running on Amazon Linux, Ubuntu, Red Hat Enterprise Linux, and CentOS: [https://s3\.amazonaws\.com/aws\-agent\.us\-east\-1/linux/support/supported\_versions\.json](https://s3.amazonaws.com/aws-agent.us-east-1/linux/support/supported_versions.json)\. 

## Supported Windows\-based Operating Systems<a name="inspector_supported-win-os"></a>

In this release of Amazon Inspector, your assessment targets can consist only of EC2 instances that run the 64\-bit version of the following Windows\-based operating systems:

+ Windows Server 2008 R2

+ Windows Server 2012

+ Windows Server 2012 R2

## Supported Regions<a name="inspector_supported-regions"></a>

At this time, Amazon Inspector supports assessment services for EC2 instances in only the following AWS regions:

+ Asia Pacific \(Mumbai\)

+ Asia Pacific \(Seoul\)

+ Asia Pacific \(Sydney\)

+ Asia Pacific \(Tokyo\)

+ EU \(Ireland\)

+ US East \(Northern Virginia\)

+ US West \(Northern California\)

+ US West \(Oregon\)

Amazon Inspector is hosted within AWS regions behind a public endpoint\. All regions are isolated from each other, and the telemetry and findings for all assessments performed within a region remain in that region and are not distributed by the service to other Amazon Inspector locations\. 