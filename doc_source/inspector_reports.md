# Assessment Reports<a name="inspector_reports"></a>

An assessment report is a document that details what is tested in the assessment run, and the results of the assessment\. The results of your assessment are formatted into standard reports, which can be generated to share results within your team for remediation actions, to enrich compliance audit data, or to store for future reference\. An Amazon Inspector assessment report can be generated for an assessment run once it has been successfully completed\. 

**Note**  
You can only generate reports for assessment runs that took place or will take place after 4/25/2017, which is when assessment reports in Amazon Inspector became available\.

You can view the following types of assessment reports:
+ **Findings report** \- this report contains the following information:
  + Executive summary of the assessment
  + EC2 instances evaluated during the assessment run
  + Rules packages included in the assessment run
  + Detailed information about each finding, including all EC2 instances that had the finding
+ **Full report** \- this report contains all the information that is included in a findings report, and additionally provides the list of rules that passed on all instances in the assessment target\.

**To generate an assessment report**

1. On the **Assessment runs** page, locate the assessment run for which you want to generate a report and make sure that its status is set to **Analysis complete**\.

1. Choose the reports icon under the **Reports** column for this assessment run\.
**Important**  
The reports icon is present in the **Reports** column only for those assessment runs that took place or will take place after 4/25/2017, which is when assessment reports in Amazon Inspector became available\.

1. In the **Assessment report** pop up window, select the type of report you want to view \(you can choose between a **Findings** or a **Full** report\) and the report format \(HTML or PDF\), and then choose **Generate report**\.

You can also generate assessment reports via the [GetAssessmentReport](http://docs.aws.amazon.com/inspector/latest/APIReference/API_GetAssessmentReport.html) API\.

To delete an assessment report, perform the following procedure:

**To delete an assessment report**
+ In the **Assessment runs** page, choose the run that the report that you want to delete is based on, and then choose **Delete**\. When prompted for confirmation, choose **Yes**\.
**Important**  
In Amazon Inspector, you cannot delete individual reports\. When you delete an assessment run, all versions of the report from that run and all findings are also deleted\.

  You can also delete an assessment run by using the [DeleteAssessmentRun](https://docs.aws.amazon.com/inspector/latest/APIReference/API_DeleteAssessmentRun.html) API\. 