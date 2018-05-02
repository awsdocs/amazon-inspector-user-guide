# Overview of Managing Access Permissions to Your Amazon Inspector Resources<a name="access-control-overview"></a>

Every AWS resource is owned by an AWS account, and permissions to create or access a resource are governed by permissions policies\. An account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\), and some services \(such as AWS Lambda\) also support attaching permissions policies to resources\.

**Note**  
An *account administrator* \(or administrator user\) is a user with administrator privileges\. For more information, see [IAM Best Practices](http://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) in the *IAM User Guide*\.

When granting permissions, you decide who is getting the permissions, the resources they get permissions for, and the specific actions that you want to allow on those resources\.

**Topics**
+ [Amazon Inspector Resources and Operations](#access-control-resources)
+ [Understanding Resource Ownership](#access-control-resource-ownership)
+ [Managing Access to Resources](#access-control-manage-access-intro)
+ [Specifying Policy Elements: Actions, Effects, Resources, and Principals](#access-control-specify-inspector-actions)
+ [Specifying Conditions in a Policy](#specifying-conditions)

## Amazon Inspector Resources and Operations<a name="access-control-resources"></a>

 In Amazon Inspector, the primary resources are resource groups, assessment targets, assessment templates, assessment runs, and findings\. These resources have unique Amazon Resource Names \(ARNs\) associated with them as shown in the following table\. 


****  

| Resource Type | ARN Format  | 
| --- | --- | 
| Resource group |  arn:aws:inspector:*region*:*account\-id*:resourcegroup/*ID*  | 
| Assessment target |   arn:aws:inspector:*region*:*account\-id*:target/*ID*   | 
| Assessment template |   arn:aws:inspector:*region*:*account\-id*:target/*ID*:template:*ID*  | 
| Assessment run |   arn:aws:inspector:*region*:*account\-id*:target/*ID*/template/*ID*/run/*ID*  | 
| Finding |   arn:aws:inspector:*region*:*account\-id*:target/*ID*/template/*ID*/run/*ID*/finding/*ID*  | 

Amazon Inspector provides a set of operations to work with the Amazon Inspector resources\. For a list of available operations, see [Actions](http://docs.aws.amazon.com/inspector/latest/APIReference/API_Operations.html)\.

## Understanding Resource Ownership<a name="access-control-resource-ownership"></a>

A *resource owner* is the AWS account that created the resource\. That is, the resource owner is the AWS account of the *principal entity* \(the root account, an IAM user, or an IAM role\) that authenticates the request that creates the resource\. The following examples illustrate how this works:
+ If you use the root account credentials of your AWS account to create an Amazon Inspector assessment target, your AWS account is the owner of this resource\. 
+ If you create an IAM user in your AWS account and grant permissions to create an Amazon Inspector assessment target to that user, the user can create an Amazon Inspector assessment target\. However, your AWS account, to which the user belongs, owns the Amazon Inspector assessment target resource\.
+ If you create an IAM role in your AWS account with permissions to create an Amazon Inspector assessment target, anyone who can assume the role can create an Amazon Inspector assessment target\. Your AWS account, to which the role belongs, owns the Amazon Inspector assessment target resource\. 

## Managing Access to Resources<a name="access-control-manage-access-intro"></a>

A *permissions policy* describes who has access to what\. The following section explains the available options for creating permissions policies\.

**Note**  
This section discusses using IAM in the context of Amazon Inspector\. It doesn't provide detailed information about the IAM service\. For complete IAM documentation, see [What Is IAM?](http://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) in the *IAM User Guide*\. For information about IAM policy syntax and descriptions, see [AWS IAM Policy Reference](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

Policies attached to an IAM identity are referred to as *identity\-based* policies \(IAM polices\)\. Policies attached to a resource are referred to as *resource\-based* policies\. Amazon Inspector supports only identity\-based policies\.

**Topics**
+ [Identity\-Based Policies \(IAM Policies\)](#access-control-manage-access-identity-based)
+ [id="access\-control\-manage\-access\-resource\-based\.title">Resource\-Based Policies](#access-control-manage-access-resource-based)

### Identity\-Based Policies \(IAM Policies\)<a name="access-control-manage-access-identity-based"></a>

You can attach policies to IAM identities\. For example, you can do the following: 
+ **Attach a permissions policy to a user or a group in your account** – An account administrator can use a permissions policy that is associated with a particular user to grant permissions for that user to create an Amazon Inspector assessment target\. 
+ **Attach a permissions policy to a role \(grant cross\-account permissions\)** – You can attach an identity\-based permissions policy to an IAM role to grant cross\-account permissions\. For example, the administrator in Account A can create a role to grant cross\-account permissions to another AWS account \(for example, Account B\) or an AWS service as follows:
  + Account A administrator creates an IAM role and attaches a permissions policy to the role that grants permissions on resources in Account A\.
  + Account A administrator attaches a trust policy to the role identifying Account B as the principal who can assume the role\. 
  + Account B administrator can then delegate permissions to assume the role to any users in Account B\. Doing this allows users in Account B to create or access resources in Account A\. If you want to grant an AWS service permissions to assume the role, he principal in the trust policy can also be an AWS service principal\.

   For more information about using IAM to delegate permissions, see [Access Management](http://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) in the *IAM User Guide*\. 

The following is an example policy that grants permissions for the `inspector:ListFindings` action on all resources\. 

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

For more information about using identity\-based policies with Amazon Inspector, see [Using Identity\-based Policies \(IAM Policies\) for Amazon Inspector](access-control-identity-based.md)\. For more information about users, groups, roles, and permissions, see [Identities \(Users, Groups, and Roles\)](http://docs.aws.amazon.com/IAM/latest/UserGuide/id.html) in the *IAM User Guide*\. 

### id="access\-control\-manage\-access\-resource\-based\.title">Resource\-Based Policies<a name="access-control-manage-access-resource-based"></a>

Other services, such as Amazon S3, also support resource\-based permissions policies\. For example, you can attach a policy to an S3 bucket to manage access permissions to that bucket\. Amazon Inspector doesn't support resource\-based policies\. 

## Specifying Policy Elements: Actions, Effects, Resources, and Principals<a name="access-control-specify-inspector-actions"></a>

For each Amazon Inspector resource \(see [Amazon Inspector Resources and Operations](#access-control-resources)\), the service defines a set of API operations \(see [Actions](http://docs.aws.amazon.com/inspector/latest/APIReference/API_Operations.html)\)\. To grant permissions for these API operations, Amazon Inspector defines a set of actions that you can specify in a policy\. Note that performing an API operation can require permissions for more than one action\. When granting permissions for specific actions, you also identify the resource on which the actions are allowed or denied\.

The following are the most basic policy elements:
+ **Resource** – In a policy, you use an Amazon Resource Name \(ARN\) to identify the resource to which the policy applies\. For more information, see [Amazon Inspector Resources and Operations](#access-control-resources)\. 
+ **Action** – You use action keywords to identify resource operations that you want to allow or deny\. For example, the `inspector:ListFindings` permission allows the user permissions to perform the Amazon Inspector `ListFindings` operation\. 
+ **Effect** – You specify the effect when the user requests the specific action—this can be either allow or deny\. If you don't explicitly grant access to \(allow\) a resource, access is implicitly denied\. You can also explicitly deny access to a resource, which you might do to make sure that a user cannot access it, even if a different policy grants access\.
+ **Principal** – In identity\-based policies \(IAM policies\), the user that the policy is attached to is the implicit principal\.

To learn more about IAM policy syntax and descriptions, see [AWS IAM Policy Reference](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

For a table showing all of the Amazon Inspector API actions and the resources that they apply to, see [Amazon Inspector API Permissions: Actions, Resources, and Conditions Reference](inspector-api-permissions-ref.md)\. 

## Specifying Conditions in a Policy<a name="specifying-conditions"></a>

When you grant permissions, you can use the IAM policy language to specify the conditions that need to be met for a policy to take effect\. For example, you might want a policy to be applied only after a specific date\. For more information about specifying conditions in a policy's language, see [Condition](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#Condition) in the *IAM User Guide*\.

To express conditions, you use predefined condition keys\. There are no condition keys specific to Amazon Inspector\. However, there are AWS\-wide condition keys that you can use as appropriate\. For a complete list of AWS\-wide keys, see [Available Keys for Conditions](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\.