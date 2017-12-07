# Amazon Inspector Quickstart Walkthrough \- Amazon Linux<a name="inspector_quickstart"></a>

Before you follow the instructions in this walkthrough, we recommend that you get familiar with the [Amazon Inspector Terminology and Concepts](inspector_concepts.md)\.

This walkthrough is designed for a first\-time user and includes all the tasks, including prerequisite tasks, for creating an assessment target, assessment template, and assessment run\.

This walkthrough is designed to demonstrate how to use Amazon Inspector to analyze the behavior of the EC2 instances that run the Amazon Linux AMI 2016\.09\.1 operating system\.

+ [Set Up Amazon Inspector](#setupinspector)\. This is the first\-run experience, including completing all the pre\-requisite tasks via the Amazon Inspector console\.

+ [Prepare Your Assessment Target for the Assessment Run](#prepareapplication)

+ [Create an Assessment Target](#createassessmenttarget)

+ [Create and Run an Assessment Template](#createassessmenttemplate)

+ [Locate and Analyze Generated Findings](#analyzefinding)

+ [Apply the Recommended Fix to Your Assessment Target](#upgradeapplication)

## Set Up Amazon Inspector<a name="setupinspector"></a>

1. Sign in to the AWS Management Console and open the Amazon Inspector console at [https://console\.aws\.amazon\.com/inspector/](https://console.aws.amazon.com/inspector/)\.

1. Choose **Get started** to launch the **Get started** wizard, and on the **Step 1: Prerequisites** page, do the following:

   1. Tag the EC2 instances that you want to include in your Amazon Inspector assessment target\.

      For this walkthrough, create one EC2 instance running Amazon Linux AMI 2016\.09\.1 and tag it using the **Name** key and a value of **InspectorEC2InstanceLinux**\.
**Note**  
For more information about tagging EC2 instances, see [ Resources and Tags](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_Resources.html)\.

   1. Install the Amazon Inspector Agent on your tagged EC2 instance\. 
**Note**  
You can install the Amazon Inspector Agent on multiple instances \(both Linux\-based and Windows\-based with the same command\) at once using the Systems Manager Run Command\. To install the agent on all the instances in the assessment target, you can specify the same tags used for creating the assessment target\. Or you can install the Amazon Inspector Agent on your EC2 instance manually\. For more information, see [Installing Amazon Inspector Agents](inspector_installing-uninstalling-agents.md)\.
**Important**  
To skip the manual Amazon Inspector Agent installation on the Amazon Linux EC2 instances that you want to include in your assessment targets, you can use the ** Amazon Linux AMI with Amazon Inspector Agent**\. This AMI has the Amazon Inspector Agent pre\-installed and requires no additional steps to install or setup the agent\. To start using Amazon Inspector with these EC2 instances, simply tag them to match the desired assessment target\. The configuration of ** Amazon Linux AMI with Amazon Inspector Agent** enhances security by focusing on two main security goals: limiting access and reducing software vulnerabilities\.   
This is the only currently available EC2 instance AMI with the pre\-installed Amazon Inspector Agent\. For the EC2 instances running Ubuntu Server or Windows Server, you must complete the manual Amazon Inspector Agent installation steps\.  
The ** Amazon Linux AMI with Amazon Inspector Agent** is available in the EC2 console and also the [AWS Marketplace](https://aws.amazon.com/marketplace/pp/B077W1VR7G                                     )\.

   1. Choose **Next**\. 

**Note**  
At this point, a service\-linked role called `AWSServiceRoleForAmazonInspector` is created to grant Amazon Inspector access to your resources\. For more information, see [Auto\-create a service\-linked role to grant Amazon Inspector access your AWS account](inspector_settingup.md#CreateRole)\.

## Prepare Your Assessment Target for the Assessment Run<a name="prepareapplication"></a>

For this walkthrough, you modify your assessment target to expose it to the potential security issue CVE\-2015\-3276\. For more information, see [ https://cve\.mitre\.org/cgi\-bin/cvename\.cgi?name=CVE\-2015\-3276](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-3276)\. Also, for more information, see [Common Vulnerabilities and Exposures](inspector_cves.md)\. 

Connect to your instance **InspectorEC2InstanceLinux** that you created in the preceding section, and run the following command:

`sudo yum install openldap-2.4.40-12.29.amzn1`

## Create an Assessment Target<a name="createassessmenttarget"></a>

On the **Amazon Inspector \- Assessment Targets ** page, choose **Create** and then do the following:

1. For **Name**, type the name for your assessment target\.

   For this walkthrough, type **MyTargetLinux**\.

1. Use the **Tags** **Key** and **Value** fields to type the tag key name and key\-value pairs in order to select the EC2 instances that you want to include in this assessment target\.

   For this walkthrough, to use the EC2 instance that you created in the preceding step, type **Name** in the **Key** field and **InspectorEC2InstanceLinux** in the **Value** field, and then choose **Save**\.

## Create and Run an Assessment Template<a name="createassessmenttemplate"></a>

On the **Amazon Inspector \- Assessment Templates ** page, choose **Create** and then do the following:

1. For **Name**, type the name for your assessment template\. For this walkthrough, type **MyFirstTemplateLinux**\.

1. For **Target name**, choose the assessment target you created above \- **MyTargetLinux**\.

1. For **Rules packages**, use the pull\-down menu to select the rules packages that you want to use in this assessment template\.

   For this walkthrough, choose **Common Vulnerabilities and Exposures\-1\.1**\.

1. For **Duration**, specify the duration for your assessment template\.

   For this walkthrough, select **15 minutes**\.

1. Choose **Create and run**\.

## Locate and Analyze Generated Findings<a name="analyzefinding"></a>

A completed assessment run produces a set of findings, or potential security issues that Amazon Inspector discovered in your assessment target\. You can review the findings and follow the recommended steps to resolve the potential security issues\.

In this walkthrough, if you complete the preceding steps, your assessment run produces a finding against the common vulnerability CVE\-2015\-3276\.

1. Navigate to the **Amazon Inspector \- Assessment Runs** page in the Amazon Inspector console and verify that the status of run for the assessment template called **MyFirstTemplateLinux** that you created in the preceding step is set to **Collecting data**\. This indicates that the assessment run is currently in progress, and the telemetry data for your target is being collected and analyzed against the selected rules packages\.

1. You cannot view the findings generated by the assessment run while it is still in progress\. Let the assessment run complete its entire duration\. However, for this walkthrough, you can stop the run after several minutes\.

   Note that the status of **MyFirstTemplateLinux** changes first to **Stopping**, then in a few minutes to **Analyzing**, and then finally to **Analysis complete**\. To see this change in status, you can choose the **Refresh** icon\.

1. In the Amazon Inspector console, navigate to the **Amazon Inspector \- Findings** page\.

   You can see a new finding of High severity that reads "Instance InspectorEC2InstanceLinux is vulnerable to CVE\-2015\-3276"\.
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

## Apply the Recommended Fix to Your Assessment Target<a name="upgradeapplication"></a>

For this walkthrough, you modified your assessment target to expose it to a potential security issue CVE\-2015\-3276\. In this procedure, you can apply the recommended fix for this issue\.

1. Connect to your instance **InspectorEC2InstanceLinux** that you created in the preceding section, and run the following command: 

   `yum update openldap`

1. On the **Amazon Inspector \- Assessment Templates** page, select **MyFirstTemplateLinux**, and then choose **Run** to start a new assessment run using this template\. 

1. Follow the steps in [Locate and Analyze Generated Findings](#analyzefinding) to see the findings resulting from this subsequent run of the **MyFirstTemplateLinux** template\.

   Because you resolved the found CVE\-2015\-3276 security issue, you will no longer see a finding highlighting it\. 