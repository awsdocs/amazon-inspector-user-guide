# Amazon Inspector Assessment Targets<a name="inspector_applications"></a>

You can use Amazon Inspector to evaluate whether your AWS assessment targets \(your collections of AWS resources\) have potential security issues that you need to address\. 

**Important**  
In this release of Amazon Inspector, your assessment targets can consist only of EC2 instances that run on a number of supported operating systems\. For more information about supported Linux\-based and Windows\-based operating systems, and supported AWS regions, see [Amazon Inspector Service Limits](inspector_limits.md)\. 

**Note**  
For more information about launching EC2 instances, see [ Amazon Elastic Compute Cloud Documentation](https://aws.amazon.com/documentation/ec2/)\. 

**Topics**
+ [Tagging Resources to Create an Assessment Target](#tagging)
+ [Amazon Inspector Assessment Targets Limits](#inspector-application-limits)
+ [Creating an Assessment Target \(Console\)](#create_application_via_console)
+ [Deleting an Assessment Target \(Console\)](#delete_assessment_target_via_console)

## Tagging Resources to Create an Assessment Target<a name="tagging"></a>

To create an assessment target for Amazon Inspector to assess, you start by tagging the EC2 instances that you want to include in your target\. Tags are words or phrases that act as metadata for identifying and organizing your instances and other AWS resources\. Amazon Inspector uses the tags that you create to identify the instances that belong to your target\. 

Every AWS tag consists of a key and value pair of your choice\. For example, you might choose to name your key "Name" and your value "MyFirstInstance"\. After you tag your instances, you use the Amazon Inspector console to add the instances to your assessment target\. It is not necessary that any instance match more than one tag key\-value pair\.

When you tag your EC2 instances to build assessment targets for Amazon Inspector to assess, you can create your own custom tag keys or use tag keys created by others in the same AWS account\. You also can use the tag keys that AWS automatically creates, for example, the **Name** tag key that is automatically created for the EC2 instances that you launch\.

You can add tags to EC2 instances when you create them or add, change, or remove those tags one at a time within each EC2 instance's console page\. You can also add tags to multiple EC2 instances at once using the Tag Editor\.

For more information, see [ Tag Editor](http://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\. For more information about tagging EC2 instances, see [Resources and Tags](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_Resources.html)\.

## Amazon Inspector Assessment Targets Limits<a name="inspector-application-limits"></a>

You can create up to 50 assessment targets per AWS account\. For more information, see [Amazon Inspector Service Limits](inspector_limits.md)\. 

## Creating an Assessment Target \(Console\)<a name="create_application_via_console"></a>

 You can use the Amazon Inspector console to create assessment targets\.

**To create an assessment target**

1. Sign in to the AWS Management Console and open the Amazon Inspector console at [https://console\.aws\.amazon\.com/inspector/](https://console.aws.amazon.com/inspector/)\.

1. In the navigation pane, choose **Assessment Targets**, and then choose **Create**\.

1. For **Name**, type a name for your assessment target\.

1. Use the **Tags**' **Key** and **Value** fields to type the tag key name and key\-value pairs in order to select the EC2 instances that you want to include in this assessment target\.

1. \(Optional\) While creating a new target, you can check the checkbox to install the Amazon Inspector Agent on all EC2 instances in this target\. To use this option, your EC2 instances must have the SSM Agent installed and an IAM role that allows Run Command\. The SSM Agent is installed, by default, on Amazon EC2 Windows instances and Amazon Linux instances\. Amazon EC2 Systems Manager requires an IAM role for EC2 instances that will process commands and a separate role for users executing commands\. For more information, see [Installing and Configuring SSM Agent](http://docs.aws.amazon.com/systems-manager/latest/userguide/ssm-agent.html) and [Configuring Security Roles for System Manager](http://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-access.html)\. 
**Important**  
If an EC2 instance already has an agent running on it, using this option replaces the agent currently running on the instance with the latest agent version\.
**Note**  
For your existing assessment targets, you can select the **Install Agents with Run Command button** to install the Amazon Inspector Agent on all EC2 instances in this target\.
**Note**  
You can also install the Amazon Inspector Agent on multiple EC2 instances \(both Linux\-based and Windows\-based instances with the same command\) remotely by using the Systems Manager Run Command\. For more information, see [To install the Amazon Inspector Agent on multiple EC2 instances using the Systems Manager Run Command](inspector_installing-uninstalling-agents.md#install-run-command)\. 

1. Choose **Save**\.

**Note**  
For your existing assessment targets, you can use the **Preview Target** button on the **Assessment Targets** page to review all EC2 instances that are currently included in the assessment targets\. For every EC2 instance listed, you can review the hostname, instance ID, IP address, and the status of the Amazon Inspector Agent that is running on the EC2 instance\. The agent status can have the following values: **HEALTHY**, **UNHEALTHY** \(displayed when the agent is reporting that it is not in a healthy state\), and **UNKNOWN** \(displayed when Amazon Inspector is unable to determine whether there is an Amazon Inspector Agent running on the EC2 instance\)\. 

## Deleting an Assessment Target \(Console\)<a name="delete_assessment_target_via_console"></a>

To delete an assessment target, perform the following procedure:
+ In the **Assessment targets** page, choose the target you want to delete, and then choose **Delete**\. When prompted for confirmation, choose **Yes**\.
**Important**  
When you delete an assessment target, all assessment templates, assessment runs, findings and versions of the reports associated with the target are also deleted\.

You can also delete an assessment target by using the [DeleteAssessmentTarget](https://docs.aws.amazon.com/inspector/latest/APIReference/API_DeleteAssessmentTarget.html) API\. 