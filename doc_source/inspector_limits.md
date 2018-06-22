# Amazon Inspector Service Limits<a name="inspector_limits"></a>

 Amazon Inspector evaluates the security state of the resources that constitute the assessment target\. 

**Important**  
At this time, your Amazon Inspector assessment targets can consist only of EC2 instances\. 

The following are Amazon Inspector limits per AWS account: 


| Resource | Default Limit | Comments | 
| --- | --- | --- | 
| Agents per assessment | 500 | The maximum number of agents that can be included in the assessment target of an assessment run\. You can request a limit increase of agents per assessment by contacting AWS customer support\. | 
| Assessment runs | 50000 | The maximum number of assessment runs that you can create per AWS account\. You can have multiple assessment runs happening at the same time as long as the assessment targets used for these runs do not contain overlapping EC2 instances\. You can request a limit increase of assessment runs by contacting AWS customer support\. | 
| Assessment templates | 500 | The maximum number of assessment templates that you can have at any given time in an AWS account\. You can request a limit increase of assessment templates by contacting AWS customer support\. | 
| Assessment targets | 50 | The maximum number of assessment targets that you can have at any given time in an AWS account\. You can request a limit increase of assessment targets by contacting AWS customer support\. | 