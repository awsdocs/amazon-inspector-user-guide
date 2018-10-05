# Amazon Inspector Tutorial \- Ubuntu Server<a name="inspector_walkthrough_ubuntu"></a>

Before you follow the instructions in this tutorial, we recommend that you get familiar with the [Amazon Inspector Terminology and Concepts](inspector_concepts.md)\.

This tutorial is designed to demonstrate how to use Amazon Inspector to analyze the behavior of an EC2 instance that runs the Ubuntu Server 16\.04 LTS operating system\. It provides step\-by\-step instructions on how to navigate the Amazon Inspector workflow, from preparing Amazon EC2 instances, to running an assessment template, to performing the recommended security fixes generated in the assessment's findings\. If you are a first\-time user and would like to set up and run an Inspector assessment with one click, see [Creating a Basic Assessment](inspector_getting-started.md#inspector_basic-assessment)\.

**Topics**
+ [Step 1: Set Up an Amazon EC2 Instance to Use With Amazon Inspector](#setupinspector_ubuntu)
+ [Step 2: Modify Your Amazon EC2 Instance](#prepareapplication_ubuntu)
+ [Step 3: Create an Assessment Target and Install an Amazon Inspector Agent on the EC2 Instance](#createassessmenttarget_ubuntu)
+ [Step 4: Create and Run Your Assessment Template](#createassessmenttemplate_ubuntu)
+ [Step 5: Locate and Analyze Generated Findings](#analyzefinding_ubuntu)
+ [Step 6: Apply the Recommended Fix to Your Assessment Target](#upgradeapplication_ubuntu)

## Step 1: Set Up an Amazon EC2 Instance to Use With Amazon Inspector<a name="setupinspector_ubuntu"></a>
+ For this tutorial, create one EC2 instance running Ubuntu Server 16\.04 LTS and tag it using the **Name** key and a value of **InspectorEC2InstanceUbuntu**\.
**Note**  
For more information about tagging EC2 instances, see [ Resources and Tags](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_Resources.html)\.

## Step 2: Modify Your Amazon EC2 Instance<a name="prepareapplication_ubuntu"></a>

For this tutorial, you modify your target EC2 instance to expose it to the potential security issue CVE\-2017\-6507\. For more information, see [ https://cve\.mitre\.org/cgi\-bin/cvename\.cgi?name=CVE\-2017\-6507](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-6507) and [Common Vulnerabilities and Exposures](inspector_cves.md)\. 

Connect to your instance **InspectorEC2InstanceUbuntu** that you created in the preceding section, and run the following command:

`sudo apt-get install apparmor=2.10.95-0ubuntu2.5`

## Step 3: Create an Assessment Target and Install an Amazon Inspector Agent on the EC2 Instance<a name="createassessmenttarget_ubuntu"></a>

Amazon Inspector uses assessment targets to designate the AWS resources to evaluate\.

**To create an assessment target and install an agent on an EC2 instance**

1. Sign in to the AWS Management Console and open the Amazon Inspector console at [https://console\.aws\.amazon\.com/inspector/](https://console.aws.amazon.com/inspector/)\.

1. Choose **Assessment targets** on the navigation pane, and then choose **Create**\.

   Do the following:

   1. For **Name**, enter the name for your assessment target\.

      For this tutorial, type **MyTargetUbuntu**\.

   1. For **Use Tags**, choose the EC2 instances that you want to include in this assessment target by entering values for the **Key** and **Value** fields\.

      For this tutorial, choose the EC2 instance that you created in the preceding step by entering **Name** in the **Key** field and **InspectorEC2InstanceUbuntu** in the **Value** field\. 

      To include all EC2 instances in your AWS account and Region in the assessment target, select the **All Instances** box\.

   1. Install an Amazon Inspector Agent on your tagged EC2 instance\. To install an agent on all EC2 instances included in an assessment target, select the **Install Agents** box\.
**Note**  
You can also install the Amazon Inspector Agent using the Systems Manager Run Command\. To install the agent on all instances in the assessment target, you can specify the same tags used for creating the assessment target\. Or you can install the Amazon Inspector Agent on your EC2 instance manually\. For more information, see [Installing Amazon Inspector Agents](inspector_installing-uninstalling-agents.md)\.

   1. Choose **Save**\.

**Note**  
At this point, a service\-linked role called `AWSServiceRoleForAmazonInspector` is created to grant Amazon Inspector access to your resources\. For more information, see [Creating a Service\-Linked Role for Amazon Inspector](inspector_slr.md#create-slr)\.

## Step 4: Create and Run Your Assessment Template<a name="createassessmenttemplate_ubuntu"></a>

If you are using **Advanced setup**, you will be directed to the **Define an assessment template** page\. If you are using the Inspector console, navigate to the **Assessment templates** page and choose **Create**\.

Do the following:

1. For **Name**, type the name for your assessment template\. For this tutorial, type **MyFirstTemplateUbuntu**\.

1. For **Target name**, choose the assessment target you created above \- **MyTargetUbuntu**\.

1. For **Rules packages**, use the pull\-down menu to select the rules packages that you want to use in this assessment template\.

   For this tutorial, choose **Common Vulnerabilities and Exposures\-1\.1**\.

1. For **Duration**, specify the duration for your assessment template\.

   For this tutorial, select **15 minutes**\.

1. If you are using **Advanced setup**, choose **Next**\. On the following **Review** page, choose **Create**\. If you are using the Inspector console, choose **Create and run**\.

## Step 5: Locate and Analyze Generated Findings<a name="analyzefinding_ubuntu"></a>

A completed assessment run produces a set of findings, or potential security issues that Amazon Inspector discovered in your assessment target\. You can review the findings and follow the recommended steps to resolve the potential security issues\.

In this tutorial, if you complete the preceding steps, your assessment run produces a finding against the common vulnerability CVE\-2017\-6507\.

1. Navigate to the **Amazon Inspector \- Assessment Runs** page in the Amazon Inspector console and verify that the status of run for the assessment template called **MyFirstTemplateUbuntu** that you created in the preceding step is set to **Collecting data**\. This indicates that the assessment run is currently in progress, and the telemetry data for your target is being collected and analyzed against the selected rules packages\.

1. You cannot view the findings generated by the assessment run while it is still in progress\. Let the assessment run complete its entire duration\. 

   Note that the status of **MyFirstTemplateUbuntu** changes first to **Stopping**, then in a few minutes to **Analyzing**, and then finally to **Analysis complete**\. To see this change in status, you can choose the **Refresh** icon\.

1. In the Amazon Inspector console, navigate to the **Findings** page\.

   You can see a new finding of **High** severity that reads "Instance InspectorEC2InstanceUbuntu is vulnerable to CVE\-2017\-6507"\.
**Note**  
If you do not see the new finding, choose the **Refresh** icon\.

   To expand the view and see the details of this finding, choose the arrow to the left of the finding\. The details of the finding include the following:
   + The ARN of the finding
   + The name of the assessment run that produced this finding
   + The name of the assessment target that produced this finding
   + The name of the assessment template that produced this finding
   + The assessment run start time
   + The assessment run end time
   + The assessment run status
   + The name of the rules package that includes the rule that triggered this finding
   + The Amazon Inspector Agent ID
   + The name of the finding
   + The severity of the finding
   + The description of the finding
   + The recommended remediation steps that you can complete to fix the potential security issue described by the finding

## Step 6: Apply the Recommended Fix to Your Assessment Target<a name="upgradeapplication_ubuntu"></a>

For this tutorial, you modified your assessment target to expose it to a potential security issue CVE\-2017\-6507\. In this procedure, you can apply the recommended fix for this issue\.

1. Connect to your instance **InspectorEC2InstanceUbuntu**and run the following command: 

   `sudo apt-get install apparmor=2.10.95-0ubuntu2.6`

1. On the **Assessment templates** page, select **MyFirstTemplateUbuntu**, and then choose **Run** to start a new assessment run using this template\. 

1. Follow the steps in [Step 5: Locate and Analyze Generated Findings](#analyzefinding_ubuntu) to see the findings resulting from this subsequent run of the **MyFirstTemplateUbuntu** template\.

   Because you resolved the found CVE\-2017\-6507 security issue, you will no longer see a finding highlighting it\. 