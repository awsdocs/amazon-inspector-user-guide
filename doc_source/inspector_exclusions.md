# Exclusions in Amazon Inspector<a name="inspector_exclusions"></a>

Exclusions are an output of Amazon Inspector assessment runs\. Exclusions show which of your security checks can't be completed and how to resolve those errors\. These issues can be caused by such reasons as the absence of an Amazon Inspector agent on the specified target's EC2 instances, the use of an unsupported operating system, or unexpected errors\. You can view exclusions on the **Assessment runs** page of the console\. For more information, see [Viewing Post\-Assessment Exclusions](#exclusions-post-assessment)\.

To avoid incurring unnecessary AWS fees, Amazon Inspector allows you to preview exclusions before running an assessment\. You can find exclusion previews on the **Assessment templates** page of the console\. For more information, see [Previewing Exclusions](#exclusions-pre-assessment)\.

**Note**  
You can only generate post\-assessment exclusions assessment runs that took place or will take place after 6/25/2018, which is when exclusions in Amazon Inspector became available\. However, exclusions previews are available for all assessment templates regardless of creation date\.

**Topics**
+ [Exclusion Types](#exclusion_types)
+ [Previewing Exclusions](#exclusions-pre-assessment)
+ [Viewing Post\-Assessment Exclusions](#exclusions-post-assessment)

## Exclusion Types<a name="exclusion_types"></a>

Amazon Inspector can produce the following assessment exclusion types\.


| Exclusions Type | Description | Recommendation | 
| --- | --- | --- | 
|  No instances in target  |  There are no EC2 instances with the tags specified in the assessment target\.  |  Check that the tags in your assessment target match the tags of your target EC2 instance\.  | 
|  Agent is already running  |  An assessment run is already in progress on the target EC2 instance\.  | Wait until the current assessment run on the target EC2 instance has completed\. | 
|  Agent not found  |   An Amazon Inspector agent was not found on the target EC2 instance\.  |  Install or reinstall an Amazon Inspector agent on the target EC2 instance\. For more information, see [Installing Amazon Inspector Agents](inspector_installing-uninstalling-agents.md)   | 
|  Agent is unhealthy  |  The Amazon Inspector agent on the target EC2 instance is in an unhealthy state\.  |  Assure that your Amazon EC2 instances are running properly and try starting and stopping or reinstalling the Amazon Inspector agent\. If the problem persists, contact [AWS Support](https://console.aws.amazon.com/support/home)\.  | 
|  Kernel module unavailable  |  The kernel module is unavailable for the Amazon Inspector agent on the target EC2 instance\.  |  For a list of supported kernel versions, see [Amazon Inspector Supported Operating Systems and Regions](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_supported_os_regions.html)\.  | 
|  Unsupported OS version  | The target EC2 instance's operating system is not supported for Amazon Inspector assessments\. |  Remove the target EC2 instance from the assessment target, or create an assessment target that does not include this instance\. For a list of supported operating systems, see [Amazon Inspector Supported Operating Systems and Regions](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_supported_os_regions.html)\.  | 
|  Deprecated rules package  |  The assessment template includes a deprecated rules package\.  |  Create an assessment template without the deprecated rules package and use it for future assessment runs\.  | 
|  Rules package not supported by OS  |  The operating system of the target EC2 instance is not supported by a rules package included in the assessment template\.  |  Create an assessment template without the conflicting rules packages or remove the target EC2 instance from the assessment template\. For a list of rules package support by operating system, see [Rules Package Availability Across Supported Operating Systems](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_rule-packages_across_os.html)\.   | 
|  Rules evaluation error for single instance  |  An internal error has caused rules evaluation to fail for this instance\.  |  Attempt to run your assessment again\.  | 
|  Rules evaluation error  |  An internal error has caused rules evaluation to fail for your assessment\.  | Attempt to run the assessment again\. | 

## Previewing Exclusions<a name="exclusions-pre-assessment"></a>

Amazon Inspector allows you to preview potential exclusions before running an assessment\.

**To preview assessment exclusions**

1. Sign in to the AWS Management Console and open the Amazon Inspector console at [https://console\.aws\.amazon\.com/inspector/](https://console.aws.amazon.com/inspector/)\.

1. In the navigation pane, choose **Assessment templates**\. 

1. Expand an assessment template, and in the **Assessment templates** section, choose **Preview exclusions**\.

1. Review the descriptions of all detected exclusions and the recommendations for addressing them\.

   You can also list and describe exclusions by using the [https://docs.aws.amazon.com/inspector/latest/APIReference/API_ListExclusions.html](https://docs.aws.amazon.com/inspector/latest/APIReference/API_ListExclusions.html) and [https://docs.aws.amazon.com/inspector/latest/APIReference/API_DescribeExclusions.html](https://docs.aws.amazon.com/inspector/latest/APIReference/API_DescribeExclusions.html)operations respectively\.

## Viewing Post\-Assessment Exclusions<a name="exclusions-post-assessment"></a>

After an assessment run, you can view exclusions details\.

**To view post\-assessment exclusions**

1. Sign in to the AWS Management Console and open the Amazon Inspector console at [https://console\.aws\.amazon\.com/inspector/](https://console.aws.amazon.com/inspector/)\.

1. In the navigation pane, choose **Assessment runs**\.

1.  the **Exclusions** column, choose the active link that is associated with an assessment run\.

1. Review the descriptions of all detected exclusions and the recommendations for addressing them\.

   You can also list and describe exclusions by using the [https://docs.aws.amazon.com/inspector/latest/APIReference/API_ListExclusions.html](https://docs.aws.amazon.com/inspector/latest/APIReference/API_ListExclusions.html) and [https://docs.aws.amazon.com/inspector/latest/APIReference/API_DescribeExclusions.html](https://docs.aws.amazon.com/inspector/latest/APIReference/API_DescribeExclusions.html)operations respectively\. 