# Amazon Inspector supported operating systems and Regions<a name="inspector_supported_os_regions"></a>

This chapter provides information about the operating systems and AWS Regions that Amazon Inspector supports\.

**Important**  
Currently, Amazon Inspector assessment targets can consist only of EC2 instances\. You can run an agentless assessment with the [Network Reachability](inspector_network-reachability.md) rules package on any EC2 instances regardless of operating system\.

For information about the Amazon Inspector rules packages that are available across supported operating systems, see [Amazon Inspector rules packages for supported operating systems](inspector_rule-packages_across_os.md)\.

**Topics**
+ [Supported Linux\-based operating systems for the Amazon Inspector agent](#inspector_supported-linux-os)
+ [Supported Windows\-based operating systems for the Amazon Inspector agent](#inspector_supported-win-os)
+ [Supported AWS Regions](#inspector_supported-regions)

## Supported Linux\-based operating systems for the Amazon Inspector agent<a name="inspector_supported-linux-os"></a>

You can use the Amazon Inspector agent on 64\-bit x86 and [Arm](https://aws.amazon.com/ec2/instance-types/a1/) EC2 instances\. The agent is compatible with the following versions of Linux\-based operating systems:
+ **64\-bit x86 instances**
  + Amazon Linux 2
  + Amazon Linux \(2018\.03, 2017\.09, 2017\.03, 2016\.09, 2016\.03, 2015\.09, 2015\.03, 2014\.09, 2014\.03, 2013\.09, 2013\.03, 2012\.09, 2012\.03\)
  + Ubuntu \(20\.4 LTS, 18\.04 LTS, 16\.04 LTS, 14\.04 LTS\)
  + Debian \(10\.x, 9\.0 \- 9\.5, 8\.0 \- 8\.7\)
  + Red Hat Enterprise Linux \(8\.x, 7\.2 \- 7\.x, 6\.2 \- 6\.9\)
  + CentOS \(7\.2 \- 7\.x, 6\.2 \- 6\.9\)
+ **Arm instances**
  + Amazon Linux 2
  + Red Hat Enterprise Linux \(7\.6 \- 7\.x\)
  + Ubuntu \(18\.04 LTS, 16\.04 LTS\)

## Supported Windows\-based operating systems for the Amazon Inspector agent<a name="inspector_supported-win-os"></a>

You can use the Amazon Inspector agent only on EC2 instances that run the 64\-bit version of the following Windows\-based operating systems:
+ Windows Server 2019 Base
+ Windows Server 2016 Base
+ Windows Server 2012 R2
+ Windows Server 2012
+ Windows Server 2008 R2

## Supported AWS Regions<a name="inspector_supported-regions"></a>

Amazon Inspector is supported in the following AWS Regions:
+ US East \(Ohio\)
+ US East \(N\. Virginia\)
+ US West \(N\. California\)
+ US West \(Oregon\)
+ Asia Pacific \(Mumbai\)
+ Asia Pacific \(Seoul\)
+ Asia Pacific \(Sydney\)
+ Asia Pacific \(Tokyo\)
+ Europe \(Frankfurt\)
+ Europe \(Ireland\)
+ Europe \(London\)
+ Europe \(Stockholm\)
+ AWS GovCloud \(US\-East\)
+ AWS GovCloud \(US\-West\)

**Note**  
The [Network Reachability](inspector_network-reachability.md) rules package is not available in the AWS GovCloud \(US\) Regions\.