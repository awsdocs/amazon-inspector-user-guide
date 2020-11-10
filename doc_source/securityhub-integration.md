# Integration with AWS Security Hub<a name="securityhub-integration"></a>

[AWS Security Hub](https://docs.aws.amazon.com/securityhub/latest/userguide/what-is-securityhub.html) provides you with a comprehensive view of your security state in AWS and helps you to check your environment against security industry standards and best practices\. Security Hub collects security data from across AWS accounts, services, and supported third\-party partner products and helps you to analyze your security trends and identify the highest priority security issues\.

The Amazon Inspector integration with Security Hub enables you to send findings from Amazon Inspector to Security Hub\. Security Hub can then include those findings in its analysis of your security posture\.

**Contents**
+ [How Amazon Inspector sends findings to Security Hub](#securityhub-integration-sending-findings)
  + [Types of findings that Amazon Inspector sends](#securityhub-integration-finding-types)
  + [Latency for sending findings](#securityhub-integration-finding-latency)
  + [Retrying when Security Hub is not available](#securityhub-integration-retry-send)
  + [Updating existing findings in Security Hub](#securityhub-integration-finding-updates)
+ [Typical finding from Amazon Inspector](#securityhub-integration-finding-example)
+ [Enabling and configuring the integration](#securityhub-integration-enable)
+ [How to stop sending findings](#securityhub-integration-disable)

## How Amazon Inspector sends findings to Security Hub<a name="securityhub-integration-sending-findings"></a>

In Security Hub, security issues are tracked as findings\. Some findings come from issues that are detected by other AWS services or by third\-party partners\. Security Hub also has a set of rules that it uses to detect security issues and generate findings\.

Security Hub provides tools to manage findings from across all of these sources\. You can view and filter lists of findings and view details for a finding\. See [Viewing findings](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-viewing.html) in the *AWS Security Hub User Guide*\. You can also track the status of an investigation into a finding\. See [Taking action on findings](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-taking-action.html) in the *AWS Security Hub User Guide*\.

All findings in Security Hub use a standard JSON format called the AWS Security Finding Format \(ASFF\)\. The ASFF includes details about the source of the issue, the affected resources, and the current status of the finding\. See [AWS Security Finding Format \(ASFF\)](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.htm) in the *AWS Security Hub User Guide*\.

Amazon Inspector is one of the AWS services that sends findings to Security Hub\.

### Types of findings that Amazon Inspector sends<a name="securityhub-integration-finding-types"></a>

Amazon Inspector sends all of the findings it generates to Security Hub\.

Amazon Inspector sends the findings to Security Hub using the [AWS Security Finding Format \(ASFF\)](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html)\. In ASFF, the `Types` field provides the finding type\. Findings from Amazon Inspector can have the following values for `Types`\.
+ Software and Configuration Checks/Vulnerabilities/CVE 
+ Software and Configuration Checks/AWS Security Best Practices/Network Reachability
+ Software and Configuration Checks/Industry and Regulatory Standards/CIS Host Hardening Benchmarks

### Latency for sending findings<a name="securityhub-integration-finding-latency"></a>

When Amazon Inspector creates a new finding, it is usually sent to Security Hub within five minutes\.

### Retrying when Security Hub is not available<a name="securityhub-integration-retry-send"></a>

If Security Hub is not available, Amazon Inspector retries sending the findings until they are received\.

### Updating existing findings in Security Hub<a name="securityhub-integration-finding-updates"></a>

After it sends a finding to Security Hub, Amazon Inspector updates the finding to reflect additional observations of the finding activity\. This will result in fewer Amazon Inspector findings in Security Hub than in Amazon Inspector\.

## Typical finding from Amazon Inspector<a name="securityhub-integration-finding-example"></a>

Amazon Inspector sends findings to Security Hub using the [AWS Security Finding Format \(ASFF\)](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html)\.

Here is an example of a typical finding from Amazon Inspector\.

```
{
  "SchemaVersion": "2018-10-08",
  "Id": "inspector/us-east-1/111122223333/629ff13fbbb44c872f7bba3e7f79f60cb6d443d8",
  "ProductArn": "arn:aws:securityhub:us-east-1::product/aws/inspector",
  "GeneratorId": "arn:aws:inspector:us-east-1:316112463485:rulespackage/0-PmNV0Tcd",
  "AwsAccountId": "111122223333",
  "Types": [
    "Software and Configuration Checks/AWS Security Best Practices/Network Reachability - Recognized port reachable from internet"
  ],
  "CreatedAt": "2020-08-19T17:36:22.169Z",
  "UpdatedAt": "2020-11-04T16:36:06.064Z",
  "Severity": {
    "Label": "MEDIUM",
    "Normalized": 40,
    "Original": "6.0"
  },
  "Confidence": 10,
  "Title": "On instance i-0c10c2c7863d1a356, TCP port 22 which is associated with 'SSH' is reachable from the internet",
  "Description": "On this instance, TCP port 22, which is associated with SSH, is reachable from the internet. You can install the Inspector agent on this instance and re-run the assessment to check for any process listening on this port. The instance i-0c10c2c7863d1a356 is located in VPC vpc-a0c2d7c7 and has an attached ENI eni-078eac9d6ad9b20d1 which uses network ACL acl-154b8273. The port is reachable from the internet through Security Group sg-0af64c8a5eb30ca75 and IGW igw-e209d785",
  "Remediation": {
    "Recommendation": {
      "Text": "You can edit the Security Group sg-0af64c8a5eb30ca75 to remove access from the internet on port 22"
    }
  },
  "ProductFields": {
    "attributes/VPC": "vpc-a0c2d7c7",
    "aws/inspector/id": "Recognized port reachable from internet",
    "serviceAttributes/schemaVersion": "1",
    "aws/inspector/arn": "arn:aws:inspector:us-east-1:111122223333:target/0-8zh1cWkg/template/0-rqtRV0u0/run/0-Ck2F6tY9/finding/0-B458MQWe",
    "attributes/ACL": "acl-154b8273",
    "serviceAttributes/assessmentRunArn": "arn:aws:inspector:us-east-1:111122223333:target/0-8zh1cWkg/template/0-rqtRV0u0/run/0-Ck2F6tY9",
    "attributes/PROTOCOL": "TCP",
    "attributes/RULE_TYPE": "RecognizedPortNoAgent",
    "aws/inspector/RulesPackageName": "Network Reachability",
    "attributes/INSTANCE_ID": "i-0c10c2c7863d1a356",
    "attributes/PORT_GROUP_NAME": "SSH",
    "attributes/IGW": "igw-e209d785",
    "serviceAttributes/rulesPackageArn": "arn:aws:inspector:us-east-1:111122223333:rulespackage/0-PmNV0Tcd",
    "attributes/SECURITY_GROUP": "sg-0af64c8a5eb30ca75",
    "attributes/ENI": "eni-078eac9d6ad9b20d1",
    "attributes/REACHABILITY_TYPE": "Internet",
    "attributes/PORT": "22",
    "aws/securityhub/FindingId": "arn:aws:securityhub:us-east-1::product/aws/inspector/inspector/us-east-1/111122223333/629ff13fbbb44c872f7bba3e7f79f60cb6d443d8",
    "aws/securityhub/ProductName": "Inspector",
    "aws/securityhub/CompanyName": "Amazon"
  },
  "Resources": [
    {
      "Type": "AwsEc2Instance",
      "Id": "arn:aws:ec2:us-east-1:193043430472:instance/i-0c10c2c7863d1a356",
      "Partition": "aws",
      "Region": "us-east-1",
      "Tags": {
        "Name": "kubectl"
      },
      "Details": {
        "AwsEc2Instance": {
          "ImageId": "ami-02354e95b39ca8dec",
          "IpV4Addresses": [
            "172.31.43.6"
          ],
          "VpcId": "vpc-a0c2d7c7",
          "SubnetId": "subnet-4975b475"
        }
      }
    }
  ],
  "WorkflowState": "NEW",
  "Workflow": {
    "Status": "NEW"
  },
  "RecordState": "ACTIVE"
}
```

## Enabling and configuring the integration<a name="securityhub-integration-enable"></a>

To use the integration with Security Hub, you must enable Security Hub\. For information on how to enable Security Hub, see [Setting up Security Hub](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-settingup.html) in the *AWS Security Hub User Guide*\.

When you enable both Amazon Inspector and Security Hub, the integration is enabled automatically\. Amazon Inspector begins to send findings to Security Hub\.

## How to stop sending findings<a name="securityhub-integration-disable"></a>

To stop sending findings to Security Hub, you can use either the Security Hub console or the API\.

See [Disabling and enabling the flow of findings from an integration \(console\)](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-integrations-managing.html#securityhub-integration-findings-flow-console) or [Disabling the flow of findings from an integration \(Security Hub API, AWS CLI\)](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-integrations-managing.html#securityhub-integration-findings-flow-disable-api) in the *AWS Security Hub User Guide*\.