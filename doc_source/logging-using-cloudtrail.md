# Logging Amazon Inspector API Calls with AWS CloudTrail<a name="logging-using-cloudtrail"></a>

Amazon Inspector is integrated with CloudTrail, a service that captures all the Amazon InspectorAPI calls and delivers the log files to an Amazon S3 bucket that you specify\. CloudTrail captures API calls from the Amazon Inspector console or from your code to the Amazon Inspector APIs\. Using the information collected by CloudTrail, you can determine the request that was made to Amazon Inspector, the source IP address from which the request was made, who made the request, when it was made, and so on\. 

To learn more about CloudTrail, including how to configure and enable it, see the [AWS CloudTrail User Guide](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/)\.

## Amazon Inspector Information in CloudTrail<a name="service-name-info-in-cloudtrail"></a>

When CloudTrail logging is enabled in your AWS account, API calls made to Amazon Inspector actions are tracked in CloudTrail log files, where they are written with other AWS service records\. CloudTrail determines when to create and write to a new file based on a time period and file size\.

All Amazon Inspector actions are logged by CloudTrail and are documented in the [Amazon Inspector API Reference](http://docs.aws.amazon.com/inspector/latest/APIReference/)\. 

For example, calls to the **CreateAssessmentTarget**, **CreateAssessmentTemplate** and **StartAssessmentRun** sections generate entries in the CloudTrail log files\. 

**Note**  
For the Amazon Inspector integration with CloudTrail, for the List\* and Describe\* APIs, for example, ListAssessmentTargets or `DescribeAssessmentTargets`, only the request information is logged; for the Create\*, Start\*, Stop\*, and all other APIs, for example, `CreateResourceGroup`, both the request and response information is logged\.

Every log entry contains information about who generated the request\. The user identity information in the log entry helps you determine the following: 

+ Whether the request was made with root or IAM user credentials

+ Whether the request was made with temporary security credentials for a role or federated user

+ Whether the request was made by another AWS service

For more information, see the [CloudTrail userIdentity Element](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html)\.

You can store your log files in your Amazon S3 bucket for as long as you want, but you can also define Amazon S3 lifecycle rules to archive or delete log files automatically\. By default, your log files are encrypted with Amazon S3 server\-side encryption \(SSE\)\.

If you want to be notified upon log file delivery, you can configure CloudTrail to publish Amazon SNS notifications when new log files are delivered\. For more information, see [Configuring Amazon SNS Notifications for CloudTrail](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/getting_notifications_top_level.html)\.

You can also aggregate Amazon Inspector log files from multiple AWS regions and multiple AWS accounts into a single Amazon S3 bucket\. 

For more information, see [Receiving CloudTrail Log Files from Multiple Regions](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-receive-logs-from-multiple-accounts.html) and [Receiving CloudTrail Log Files from Multiple Accounts](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-receive-logs-from-multiple-accounts.html)\.

## Understanding Amazon Inspector Log File Entries<a name="understanding-service-name-entries"></a>

CloudTrail log files can contain one or more log entries\. Each entry lists multiple JSON\-formatted events\. A log entry represents a single request from any source and includes information about the requested action, the date and time of the action, request parameters, and so on\. Log entries are not an ordered stack trace of the public API calls, so they do not appear in any specific order\. 

The following example shows a CloudTrail log entry that demonstrates the Amazon Inspector `CreateResourceGroup` action:

```
    {
    "eventVersion": "1.03",
    "userIdentity": {
        "type": "AssumedRole",
        "principalId": "AIDACKCEVSQ6C2EXAMPLE",
        "arn": "arn:aws:iam::444455556666:user/Alice",
        "accountId": "444455556666",
        "accessKeyId": "AKIAI44QH8DHBEXAMPLE",
        "sessionContext": {
            "attributes": {
                "mfaAuthenticated": "false",
                "creationDate": "2016-04-14T17:05:54Z"
            },
            "sessionIssuer": {
                "type": "Role",
                "principalId": "AIDACKCEVSQ6C2EXAMPLE",
                "arn": "arn:aws:iam::444455556666:user/Alice",
                "accountId": "444455556666",
                "userName": "Alice"
            }
        }
    },
    "eventTime": "2016-04-14T17:12:34Z",
    "eventSource": "inspector.amazonaws.com",
    "eventName": "CreateResourceGroup",
    "awsRegion": "us-west-2",
    "sourceIPAddress": "205.251.233.179",
    "userAgent": "console.amazonaws.com",
    "requestParameters": {
        "resourceGroupTags": [
            {
                "key": "Name",
                "value": "ExampleEC2Instance"
            }
        ]
    },
    "responseElements": {
        "resourceGroupArn": "arn:aws:inspector:us-west-2:444455556666:resourcegroup/0-oclRMp8B"
    },
    "requestID": "148256d2-0264-11e6-a9b5-b98a7d3b840f",
    "eventID": "e5ea533e-eede-46cc-94f6-0d08e6306ff0",
    "eventType": "AwsApiCall",
    "apiVersion": "v20160216",
    "recipientAccountId": "444455556666"
}
```

From this event information, you can determine that the request was made to create a new resource group \(using the Amazon Inspector `CreateResourceGroup` API\) with the tag key\-value pair of `Name` and `ExampleEC2Instance` to identify the EC2 instance to be included in the new resource group\. You can also see that the request was made by an IAM user named `Alice` on April 14, 2016\.

The following example shows a CloudTrail log entry that demonstrates the Amazon Inspector `DescribeAssessmentTargets` action:

```
    {
    "eventVersion": "1.03",
    "userIdentity": {
        "type": "AssumedRole",
        "principalId": "AIDACKCEVSQ6C2EXAMPLE",
        "arn": "arn:aws:iam::444455556666:user/Alice",
        "accountId": "444455556666",
        "accessKeyId": "AKIAI44QH8DHBEXAMPLE",
        "sessionContext": {
            "attributes": {
                "mfaAuthenticated": "false",
                "creationDate": "2016-04-14T17:05:54Z"
            },
            "sessionIssuer": {
                "type": "Role",
                "principalId": "AIDACKCEVSQ6C2EXAMPLE",
                "arn": "arn:aws:iam::444455556666:user/Alice",
                "accountId": "444455556666",
                "userName": "Alice"
            }
        }
    },
      "eventTime": "2016-04-14T17:30:49Z",
      "eventSource": "inspector.amazonaws.com",
      "eventName": "DescribeAssessmentTargets",
      "awsRegion": "us-west-2",
      "sourceIPAddress": "205.251.233.179",
      "userAgent": "console.amazonaws.com",
      "requestParameters": {
        "assessmentTargetArns": [
          "arn:aws:inspector:us-west-2:444455556666:target/0-ABcQzlXc",
          "arn:aws:inspector:us-west-2:444455556666:target/0-nvgVhaxX"
        ]
      },
      "responseElements": null,
      "requestID": "a103f654-0266-11e6-93e6-890abdd45f56",
      "eventID": "bd7de684-2b2f-4d45-8cef-d22bf17bcb13",
      "eventType": "AwsApiCall",
      "apiVersion": "v20160216",
      "recipientAccountId": "444455556666"
    },
```

From this event information, you can determine that the request was made to describe two assessment targets with corresponding ARNs of arn:aws:inspector:us\-west\-2:444455556666:target/0\-ABcQzlXc and arn:aws:inspector:us\-west\-2:444455556666:target/0\-nvgVhaxX \(using the Amazon Inspector `DescribeAssessmentTargets` API\)\. You can also see that the request was made by an IAM user named `Alice` on April 14, 2016\. Note that per the Amazon Inspector implementation of the integration with CloudTrail, because this is a List\* API, only the request information is logged \(the ARNs to specify the assessment targets to be described\)\. The list of response elements is not logged and left null\.