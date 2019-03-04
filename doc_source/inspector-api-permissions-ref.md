# Amazon Inspector API Permissions: Actions, Resources, and Conditions Reference<a name="inspector-api-permissions-ref"></a>

The following table lists each Amazon Inspector API operation\. It also lists the corresponding action that you use to grant permissions to perform the action, and the AWS resource for which you can grant the permissions\. Use it as a reference when setting up [Access Control](inspector-auth-and-access-control.md#access-control1) and writing permissions policies that you can attach to an IAM identity \(identity\-based policies\)\. You specify the actions in the policy's `Action` field, and the resource value in the policy's `Resource` field\. 

You can use AWS condition keys in your Amazon Inspector policies to express conditions\. For a complete list of AWS keys, see [Available Keys for Conditions](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\. 

**Note**  
To specify an action, use the `inspector:` prefix followed by the API operation name, for example, `inspector:CreateResourceGroup`\. 


**Amazon Inspector API and Required Permissions for Actions**  

| Amazon Inspector API Operation | Required Permission \(API Action\) | Resources | 
| --- | --- | --- | 
| AddAttributesToFindings | inspector:AddAttributesToFindings | \* | 
| CreateAssessmentTarget | inspector:CreateAssessmentTarget | \* | 
| CreateAssessmentTemplate | inspector:CreateAssessmentTemplate | \* | 
| CreateResourceGroup | inspector:CreateResourceGroup | \* | 
| DeleteAssessmentRun | inspector:DeleteAssessmentRun | \* | 
| DeleteAssessmentTarget | inspector:DeleteAssessmentTarget | \* | 
| DeleteAssessmentTemplate | inspector:DeleteAssessmentTemplate | \* | 
| DescribeAssessmentRuns | inspector:DescribeAssessmentRuns | \* | 
| DescribeAssessmentTargets | inspector:DescribeAssessmentTargets | \* | 
| DescribeAssessmentTemplates | inspector:DescribeAssessmentTemplates | \* | 
| DescribeCrossAccountAccessRole | inspector:DescribeCrossAccountAccessRole | \* | 
| DescribeFindings | inspector:DescribeFindings | \* | 
| DescribeResourceGroups | inspector:DescribeResourceGroups | \* | 
| DescribeRulesPackages | inspector:DescribeRulesPackages | \* | 
| GetAssessmentReport | inspector:GetAssessmentReport | \* | 
| GetTelemetryMetadata | inspector:GetTelemetryMetadata | \* | 
| ListAssessmentRunAgents | inspector:ListAssessmentRunAgents | \* | 
| ListAssessmentRuns | inspector:ListAssessmentRuns | \* | 
| ListAssessmentTargets | inspector:ListAssessmentTargets | \* | 
| ListAssessmentTemplates | inspector:ListAssessmentTemplates | \* | 
| ListEventSubscriptions | inspector:ListEventSubscriptions | \* | 
| ListFindings | inspector:ListFindings | \* | 
| ListRulesPackages | inspector:ListRulesPackages | \* | 
| ListTagsForResource | inspector:ListTagsForResource | \* | 
| PreviewAgents | inspector:PreviewAgents | \* | 
| RegisterCrossAccountAccessRole | inspector:RegisterCrossAccountAccessRole | \* | 
| RemoveAttributesFromFindings | inspector:RemoveAttributesFromFindings | \* | 
| SetTagsForResource | inspector:SetTagsForResource | \* | 
| StartAssessmentRun | inspector:StartAssessmentRun | \* | 
| StopAssessmentRun | inspector:StopAssessmentRun | \* | 
| SubscribeToEvent | inspector:SubscribeToEvent | \* | 
| UnsubscribeFromEvent | inspector:UnsubscribeFromEvent | \* | 
| UpdateAssessmentTarget | inspector:UpdateAssessmentTarget | \* | 