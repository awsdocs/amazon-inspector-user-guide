# Amazon Inspector Tutorial \- Red Hat Enterprise Linux<a name="inspector_walkthrough"></a>

Before you follow the instructions in this tutorial, we recommend that you get familiar with the [Amazon Inspector Terminology and Concepts](inspector_concepts.md)\.

This tutorial demonstrates how to use Amazon Inspector to analyze the behavior of an EC2 instance that runs the Red Hat Enterprise Linux 7\.5 operating system\. It provides step\-by\-step instructions on how to navigate the Amazon Inspector workflow\. The workflow includes preparing Amazon EC2 instances, running an assessment template, and performing the recommended security fixes generated in the assessment's findings\. If you are a first\-time user and would like to set up and run an Amazon Inspector assessment with one click, see [Creating a Basic Assessment](inspector_getting-started.md#inspector_basic-assessment)\.

**Topics**
+ [Step 1: Set Up an Amazon EC2 Instance to Use With Amazon Inspector](#setupinspector)
+ [Step 2: Modify Your Amazon EC2 Instance](#prepareapplication)
+ [Step 3: Create an Assessment Target and Install an Amazon Inspector Agent on the EC2 Instance](#createassessmenttarget)
+ [Step 4: Create and Run Your Assessment Template](#createassessmenttemplate)
+ [Step 5: Locate and Analyze Generated Findings](#analyzefinding)
+ [Step 6: Apply the Recommended Fix to Your Assessment Target](#upgradeapplication)

## Step 1: Set Up an Amazon EC2 Instance to Use With Amazon Inspector<a name="setupinspector"></a>

For this tutorial, create one EC2 instance that runs Red Hat Enterprise Linux 7\.5, and tag it using the **Name** key and a value of **InspectorEC2InstanceLinux**\.

**Note**  
For more information about tagging EC2 instances, see [Resources and Tags](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_Resources.html)\.

## Step 2: Modify Your Amazon EC2 Instance<a name="prepareapplication"></a>

For this tutorial, you modify your target EC2 instance to expose it to the potential security issue CVE\-2018\-1111\. For more information, see [ https://cve\.mitre\.org/cgi\-bin/cvename\.cgi?name=CVE\-2018\-1111](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-1111) and [Common Vulnerabilities and Exposures](inspector_cves.md)\. 

Connect to your instance, **InspectorEC2InstanceLinux**, and run the following command:

`sudo yum install dhclient-12:4.2.5-68.el7 `

For instructions on how to connect to an EC2 instance, see [Connect to Your Instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html#ec2-connect-to-instance-linux) in the Amazon EC2 User Guide\.

## Step 3: Create an Assessment Target and Install an Amazon Inspector Agent on the EC2 Instance<a name="createassessmenttarget"></a>

Amazon Inspector uses assessment targets to designate the AWS resources that you want to evaluate\.

**To create an assessment target and install an agent on an EC2 instance**

1. Sign in to the AWS Management Console and open the Amazon Inspector console at [https://console\.aws\.amazon\.com/inspector/](https://console.aws.amazon.com/inspector/)\.

1. Choose **Assessment targets** on the navigation pane, and then choose **Create**\.

   Do the following:

   1. For **Name**, enter the name for your assessment target\.

      For this tutorial, enter **MyTargetLinux**\.

   1. For **Use Tags**, choose the EC2 instances that you want to include in this assessment target by entering values for the **Key** and **Value** fields\.

      For this tutorial, choose the EC2 instance that you created in the preceding step by entering **Name** in the **Key** field and **InspectorEC2InstanceLinux** in the **Value** field\. 

      To include all EC2 instances in your AWS account and Region in the assessment target, select the **All Instances** box\.

   1. Choose **Save**\. 

   1. Install an Amazon Inspector agent on your tagged EC2 instance\. To install an agent on all EC2 instances included in an assessment target, select the **Install Agents** box\.
**Note**  
You can also install the Amazon Inspector agent using the AWS Systems Manager Run Command\. To install the agent on all instances in the assessment target, you can specify the same tags that are used for creating the assessment target\. Or you can install the Amazon Inspector agent on your EC2 instance manually\. For more information, see [Installing Amazon Inspector Agents](inspector_installing-uninstalling-agents.md)\.

   1. Choose **Save**\.

**Note**  
At this point, a service\-linked role called `AWSServiceRoleForAmazonInspector` is created to grant Amazon Inspector access to your resources\. For more information, see [Creating a Service\-Linked Role for Amazon Inspector](inspector_slr.md#create-slr)\.

## Step 4: Create and Run Your Assessment Template<a name="createassessmenttemplate"></a>

Choose **Assessment templates** on the navigation pane, and then choose **Create**\.

Do the following:

1. For **Name**, enter the name for your assessment template\. For this tutorial, enter **MyFirstTemplateLinux**\.

1. For **Target name**, choose the assessment target that you created above, **MyTargetLinux**\.

1. For **Rules packages**, choose the rules packages that you want to use in this assessment template\.

   For this tutorial, choose **Common Vulnerabilities and Exposures\-1\.1**\.

1. For **Duration**, specify the duration for your assessment template\.

   For this tutorial, select **15 minutes**\.

1. Choose **Create and run**\.

## Step 5: Locate and Analyze Generated Findings<a name="analyzefinding"></a>

A completed assessment run produces a set of findings, or potential security issues that Amazon Inspector discovers in your assessment target\. You can review the findings and follow the recommended steps to resolve the potential security issues\.

In this tutorial, if you complete the preceding steps, your assessment run produces a finding against the common vulnerability [CVE\-2018\-1111](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-1111)\.

1. On the navigation pane, choose **Assessment runs**\. Verify that the status of the run for the assessment template called **MyFirstTemplateLinux** is set to **Collecting data**\. This indicates that the assessment run is currently in progress, and the telemetry data for your target is being collected and analyzed against the selected rules packages\.

1. You can't view the findings generated by the assessment run while it is still in progress\. Let the assessment run complete its entire duration\. However, for this tutorial, you can stop the run after several minutes\.

   The status of **MyFirstTemplateLinux** changes first to **Stopping**, then in a few minutes to **Analyzing**, and then finally to **Analysis complete**\. To see this change in status, choose the **Refresh** icon\.

1. In the navigation pane, choose **Findings**\.

   You can see a new finding of **High** severity that reads "Instance InspectorEC2InstanceLinux is vulnerable to CVE\-2018\-1111"\.
**Note**  
If you don't see the new finding, choose the **Refresh** icon\.

   To expand the view and see the details of this finding, choose the arrow to the left of the finding\. The details of the finding include the following:
   + The ARN of the finding
   + The name of the assessment run that produced this finding
   + The name of the assessment target that produced this finding
   + The name of the assessment template that produced this finding
   + The assessment run start time
   + The assessment run end time
   + The assessment run status
   + The name of the rules package that includes the rule that triggered this finding
   + The Amazon Inspector agent ID
   + The name of the finding
   + The severity of the finding
   + The description of the finding
   + The recommended remediation steps that you can complete to fix the potential security issue described by the finding

## Step 6: Apply the Recommended Fix to Your Assessment Target<a name="upgradeapplication"></a>

For this tutorial, you modified your assessment target to expose it to a potential security issue CVE\-2018\-1111\. In this procedure, you apply the recommended fix for this issue\.

1. Connect to your instance **InspectorEC2InstanceLinux** that you created in the preceding section, and run the following command: 

   `sudo yum update dhclient-12:4.2.5-68.el7`

1. On the **Assessment templates** page, choose **MyFirstTemplateLinux**, and then choose **Run** to start a new assessment run using this template\. 

1. Follow the steps in [Step 5: Locate and Analyze Generated Findings](#analyzefinding) to see the findings that result from this subsequent run of the **MyFirstTemplateLinux** template\.

   Because you resolved the found CVE\-2018\-1111 security issue, you no longer see a finding that highlights it\. 