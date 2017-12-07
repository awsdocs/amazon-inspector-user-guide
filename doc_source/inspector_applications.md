# Amazon Inspector Assessment Targets<a name="inspector_applications"></a>

You can use Amazon Inspector to evaluate whether your AWS assessment targets \(your collections of AWS resources\) have potential security issues that you need to address\. 

**Important**  
In this release of Amazon Inspector, your assessment targets can consist only of EC2 instances that run on a number of supported operating systems\. For more information about supported Linux\-based and Windows\-based operating systems, and supported AWS regions, see [Amazon Inspector Service Limits](inspector_limits.md)\. 

**Note**  
For more information about launching EC2 instances, see [ Amazon Elastic Compute Cloud Documentation](https://aws.amazon.com/documentation/ec2/)\. 


+ [Tagging Resources to Create an Assessment Target](#tagging)
+ [Amazon Inspector Assessment Targets Limits](#inspector-application-limits)
+ [Creating an Assessment Target \(Console\)](#create_application_via_console)

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

1. Choose **Save**\.