# Setting up Amazon Inspector<a name="inspector_settingup"></a>

When you sign up for Amazon Web Services \(AWS\), your AWS account is automatically signed up for all services in AWS, including Amazon Inspector\. If you don't have an AWS account, use the following procedure to create one\.

**To sign up for AWS**

1. Open [https://aws\.amazon\.com/](https://aws.amazon.com/), and then choose **Create an AWS Account**\.
**Note**  
This might be unavailable in your browser if you previously signed into the AWS Management Console\. In that case, choose **Sign in to a different account**, and then choose **Create a new AWS account**\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a PIN using the phone keypad\.

When you launch the Amazon Inspector console for the first time, choose **Get Started** and complete the following prerequisite tasks\. You must complete these tasks before you can create, start, and complete an Amazon Inspector assessment run:
+ [Tag all EC2 instances that you want to include in your assessment target](#TagEC2Instances)
+ [Install the Amazon Inspector Agent on all EC2 instances that you want to include in your assessment target](#InstallAgent)

**Important**  
Amazon Inspector is granted access to your resources through an IAM service\-linked role called `AWSServiceRoleForAmazonInspector`\. For more information, see [Auto\-create a service\-linked role to grant Amazon Inspector access your AWS account](#CreateRole)\.

## Create Assessment Targets with EC2 instance Tags<a name="TagEC2Instances"></a>

Amazon Inspector evaluates whether your assessment targets \(collections of AWS resources\) have potential security issues\. 

**Important**  
In this release of Amazon Inspector, your assessment targets can consist only of EC2 instances that run on a number of supported operating systems\. For more information about supported Linux\-based and Windows\-based operating systems, and supported AWS regions, see [Amazon Inspector Supported Operating Systems and Regions](inspector_supported_os_regions.md)\.   
For more information about launching EC2 instances, see [ Amazon Elastic Compute Cloud Documentation](https://aws.amazon.com/documentation/ec2/)\. 

Amazon Inspector uses the tags applied to your EC2 instances to target those resources as part of your defined assessment template\. When configuring your assessment targets, you can utilize the tags you already have defined on your EC2 instances, or create entirely new tags specifically for your assessments\. For more information about tagging, see [ Working with Tag Editor](http://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html) and [ Tagging Your Amazon EC2 Resources\.](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Using_Tags.html) 

For more information about tagging EC2 instances to be included in Amazon Inspector assessment targets, see [Amazon Inspector Assessment Targets](inspector_applications.md)\.

## Install the Amazon Inspector Agent<a name="InstallAgent"></a>

You must install the Amazon Inspector Agent on each EC2 instance in your assessment target\. The agent monitors the behavior of the EC2 instances on which it is installed, including network, file system, and process activity, and collects a wide set of behavior and configuration data \(telemetry\), which it then passes to the Amazon Inspector service\. For more information about Amazon Inspector Agent privileges, security, updates, telemetry data, and access control, see [Amazon Inspector Agents](inspector_agents.md)\. 

For more information about how to install the Amazon Inspector Agent, see [Installing Amazon Inspector Agents](inspector_installing-uninstalling-agents.md)\. For more information about how to uninstall the agent or verify whether the installed agent is running, see [Working with Amazon Inspector Agents on Linux\-based Operating Systems](inspector_agents-on-linux.md) and [Working with Amazon Inspector Agents on Windows\-based Operating Systems](inspector_agents-on-win.md)\.

**Important**  
To skip the manual Amazon Inspector Agent installation on the Amazon Linux EC2 instances that you want to include in your assessment targets, you can use the ** Amazon Linux AMI with Amazon Inspector Agent**\. This AMI has the Amazon Inspector Agent pre\-installed and requires no additional steps to install or setup the agent\. To start using Amazon Inspector with these EC2 instances, simply tag them to match the desired assessment target\. The configuration of ** Amazon Linux AMI with Amazon Inspector Agent** enhances security by focusing on two main security goals: limiting access and reducing software vulnerabilities\.   
This is the only currently available EC2 instance AMI with the pre\-installed Amazon Inspector Agent\. For the EC2 instances running Ubuntu Server or Windows Server, you must complete the manual Amazon Inspector Agent installation steps\.  
The ** Amazon Linux AMI with Amazon Inspector Agent** is available in the EC2 console and also the [AWS Marketplace](https://aws.amazon.com/marketplace/pp/B077W1VR7G                     )\.

## Auto\-create a service\-linked role to grant Amazon Inspector access your AWS account<a name="CreateRole"></a>

Amazon Inspector needs to enumerate your EC2 instances and tags to identify the EC2 instances specified in the assessment targets\. Amazon Inspector gets access to these resources in your AWS account through a service\-linked role called `AWSServiceRoleForAmazonInspector`\. A service\-linked role is a unique type of IAM role that is linked directly to an AWS service \(in this case, Amazon Inspector\)\. Service\-linked roles are predefined by the service and include all the permissions that the service requires to call other AWS services on your behalf\. The linked service \(in this case, Amazon Inspector\) also defines how you create, modify, and delete a service\-linked role\. For more information about service\-linked roles, see [Using Service\-Linked Roles for Amazon Inspector](inspector_slr.md) and [Using Service\-Linked Roles](http://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html)\.

For the `AWSServiceRoleForAmazonInspector` service\-linked role to be successfully created, the IAM identity \(user, role, group\) with which you use Amazon Inspector, must have the required permissions\. To grant the required permissions, attach the **AmazonInspectorFullAccess** managed policy to this IAM user, group, or role\. For more information, see [AWS Managed \(Predefined\) Policies for Amazon Inspector](access-control-identity-based.md#UsingWithInspector_IAM_AccessControl_ManagedPolicies)\.

The `AWSServiceRoleForAmazonInspector` service\-linked role is created automatically\. The following sections describe the details of auto\-generating and using the `AWSServiceRoleForAmazonInspector` service\-linked role when you get started with Amazon Inspector for the first time or when you already have Amazon Inspector running in your AWS account\. 

### If you are getting started with Amazon Inspector for the first time<a name="CreateRoleFirstRun"></a>
+ The `AWSServiceRoleForAmazonInspector` service\-linked role is created automatically when you go through the **Get Started with Amazon Inspector** wizard in the console or when you run the [CreateAssessmentTarget](http://docs.aws.amazon.com/inspector/latest/APIReference/API_CreateAssessmentTarget.html) API operation\.
+ The `AWSServiceRoleForAmazonInspector` service\-linked role is created for your AWS account only in the region to which you are currently signed in\. It grants Amazon Inspector access to the resources in your AWS account only in this region\. If you then use the same AWS account to go through the **Get Started with Amazon Inspector** console wizard or run the [CreateAssessmentTarget](http://docs.aws.amazon.com/inspector/latest/APIReference/API_CreateAssessmentTarget.html) API operation in other regions, the same service\-linked role that is already created in your AWS account is applied in these other regions and grants Amazon Inspector access to the resources in your AWS account in these other regions\. 

### If you already have Amazon Inspector running in your AWS account<a name="CreateRoleExisting"></a>
+ If you already have Amazon Inspector running in your AWS account, the IAM role that grants Amazon Inspector access to your resources already exists in your AWS account\. In this case, the `AWSServiceRoleForAmazonInspector` service\-linked role is auto\-created when you create a new assessment target or a new assessment template \(either through the Amazon Inspector console or the API operations\)\. This newly created service\-linked role replaces the previously created IAM role that up until now granted Amazon Inspector access to your resources\.

  You can also create the `AWSServiceRoleForAmazonInspector` service\-linked role manually by choosing the **Manage Amazon Inspector service\-linked role** link in the **Accounts Setting** section in the Inspector's **Dashboard** page\. This newly created service\-linked role replaces the previously created IAM role that up until now granted Amazon Inspector access to your resources\.
**Note**  
This previously created IAM role is not deleted\. It remains intact, but it is no longer used to grant Amazon Inspector access to your resources\. You can use the IAM console to further manage or delete this IAM role\.
+ The `AWSServiceRoleForAmazonInspector` service\-linked role is created for your AWS account only in the region to which you are currently signed in\. It grants Amazon Inspector access to the resources in your AWS account only in this region\. If you then use the same AWS account to create a new assessment target or a new assessment template for your Amazon Inspector service running in other regions, the same service\-linked role that is already created in your AWS account is applied and grants Amazon Inspector access to the resources in your AWS account in these other regions\. 

To delete the `AWSServiceRoleForAmazonInspector` service\-linked role, you must first delete your assessment targets for this AWS account in all the regions where you have Amazon Inspector running\. You can delete the `AWSServiceRoleForAmazonInspector` service\-linked role through the IAM console\. For more information, see [Using Service\-Linked Roles](http://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html)\.