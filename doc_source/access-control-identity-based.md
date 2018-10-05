# Using Identity\-based Policies \(IAM Policies\) for Amazon Inspector<a name="access-control-identity-based"></a>

This topic provides examples of identity\-based policies in which an account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\)\. 

**Important**  
 We recommend that you first review the introductory topics that explain the basic concepts and options available for you to manage access to your Amazon Inspector resources\. For more information, see [Overview of Managing Access Permissions to Your Amazon Inspector Resources](access-control-overview.md)\.

The sections in this topic cover the following:
+ [Permissions Required to Use the Amazon Inspector Console](#UsingWithInspector_IAM_RequiredPermissions_Console)
+ [AWS Managed \(Predefined\) Policies for Amazon Inspector](#UsingWithInspector_IAM_AccessControl_ManagedPolicies)
+ [Customer Managed Policy Examples](#IAMPolicyExamples_Inspector)

The following is an example of a permissions policy\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "inspector:ListFindings"
            ],
            "Resource": "*"
        }
    ]
}
```

This sample policy includes a statement that grants permission to list Amazon Inspector findings\. Amazon Inspector doesn't support permissions for this particular action at the resource level\. Therefore, the policy specifies a wildcard character \(\*\) as the `Resource` value\. 

## Permissions Required to Use the Amazon Inspector Console<a name="UsingWithInspector_IAM_RequiredPermissions_Console"></a>

To use the Amazon Inspector console, a user must have the permissions granted by the **AmazonInspectorFullAccess** or **AmazonInspectorReadOnlyAccess** policies described in [AWS Managed \(Predefined\) Policies for Amazon Inspector](#UsingWithInspector_IAM_AccessControl_ManagedPolicies)\. If you create an IAM policy that is more restrictive than the minimum required permissions described in either of these policies \(for instance, the preceding example policy\), the console won't function as intended for users with that IAM policy\. 

**Note**  
A user that has the preceding example policy attached can successfully list Amazon Inspector findings by calling the `ListFindings` API operation or the` list-findings` CLI command\.

## AWS Managed \(Predefined\) Policies for Amazon Inspector<a name="UsingWithInspector_IAM_AccessControl_ManagedPolicies"></a>

AWS addresses many common use cases by providing standalone IAM policies that are created and administered by AWS\. These *managed policies* grant necessary permissions for common use cases so that you can avoid having to investigate which permissions are needed\. For more information, see [AWS Managed Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

The following AWS managed policies, which you can attach to users in your account, are specific to Amazon Inspector:
+ **AmazonInspectorFullAccess ** – Provides full access to Amazon Inspector\.
+ **AmazonInspectorReadOnlyAccess ** – Provides read\-only access to Amazon Inspector\. 

You can also create custom IAM policies that allow users to access the required API actions and resources\. You can attach these custom policies to the IAM users or groups that require those permissions\.

## Customer Managed Policy Examples<a name="IAMPolicyExamples_Inspector"></a>

This section provides example user policies that grant permissions for various Amazon Inspector actions\. 

**Note**  
All examples use the US West \(Oregon\) Region \(`us-west-2`\) and contain fictitious account IDs\.

**Topics**
+ [Example 1: Allow a User to Perform Any Describe and List Actions on Any Amazon Inspector Resource](#IAMPolicyExamples_Inspector_perform_describe_and_list_action)
+ [Example 2: Allow a User to Perform Describe and List Actions Only on Amazon Inspector Findings](#IAMPolicyExamples_Inspector_perform_create_action)

### Example 1: Allow a User to Perform Any Describe and List Actions on Any Amazon Inspector Resource<a name="IAMPolicyExamples_Inspector_perform_describe_and_list_action"></a>

The following permissions policy grants a user permissions to run all of the actions that begin with `Describe` and `List`\. These actions show information about an Amazon Inspector resource, such as an assessment target or finding\. Note that the wildcard character \(\*\) in the `Resource` element indicates that the actions are allowed for all Amazon Inspector resources owned by the account\. 

```
 1. {
 2.    "Version":"2012-10-17",
 3.    "Statement":[
 4.       {
 5.          "Effect":"Allow",
 6.          "Action": [
 7.             "inspector:Describe*",
 8.             "inspector:List*"
 9.             ],
10.          "Resource":"*"
11.       }
12.    ]
13. }
```

### Example 2: Allow a User to Perform Describe and List Actions Only on Amazon Inspector Findings<a name="IAMPolicyExamples_Inspector_perform_create_action"></a>

The following permissions policy grants a user permissions to run only `ListFindings` and `DescribeFindings` operations\. These actions show information about Amazon Inspector findings\. Note that the wildcard character \(\*\) in the `Resource` element indicates that the actions are allowed for all of the Amazon Inspector resources owned by the account\. 

```
 1. {
 2.    "Version":"2012-10-17",
 3.    "Statement":[
 4.       {
 5.          "Effect":"Allow",
 6.          "Action": [
 7.                   "inspector:DescribeFindings",
 8.                   "inspector:ListFindings"
 9.          ],
10.          "Resource":"*"
11.       }
12.    ]
13. }
```