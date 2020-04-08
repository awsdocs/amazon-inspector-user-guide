# \(Optional\) Verify the signature of the Amazon Inspector agent installation script on Windows\-based operating systems<a name="inspector_verify-sig-agent-download-win"></a>

This topic describes the recommended process of verifying the validity of the Amazon Inspector agent's installations script for Windows\-based operating systems\. 

Whenever you download an application from the internet, we recommend that you authenticate the identity of the software publisher and check that the application is not altered or corrupted since it was published\. This protects you from installing a version of the application that contains a virus or other malicious code\.

If after running the steps in this topic, you determine that the software for the Amazon Inspector agent is altered or corrupted, do NOT run the installation file\. Instead, contact AWS Support\.

To verify the validity of the downloaded agent installation script on Windows\-based operating systems, make sure that the thumbprint of its Amazon Services LLC signer certificate is equal to this value:

**5C 2C B5 5A 9A B9 B1 D6 3F F4 1B 0D A2 76 F2 A9 2B 09 A8 6A**

To verify this value, perform the following procedure: 

1. Right\-click the downloaded `AWSAgentInstall.exe`, and open the **Properties** window\.

1. Choose the **Digital Signatures** tab\.

1. From the **Signature List**, choose **Amazon Services LLC**, and then choose **Details**\.

1. Choose the **General** tab, if not already selected, and then choose **View Certificate**\.

1. Choose the **Details** tab, and then choose **All** in the **Show** dropdown list, if not already selected\.

1. Scroll down until you see the **Thumbprint** field and then choose **Thumbprint**\. This displays the entire thumbprint value in the lower window\.
   + If the thumbprint value in the lower window is identical to the following value:

     **5C 2C B5 5A 9A B9 B1 D6 3F F4 1B 0D A2 76 F2 A9 2B 09 A8 6A**

     then your downloaded agent installation script is authentic and can be safely installed\.
   + If the thumbprint value in the lower details window is not identical to the value above, do not run `AWSAgentInstall.exe`\. 