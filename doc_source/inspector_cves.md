# Common Vulnerabilities and Exposures<a name="inspector_cves"></a>

The rules in this package help verify whether the EC2 instances in your assessment targets are exposed to common vulnerabilities and exposures \(CVEs\)\. Attacks can exploit unpatched vulnerabilities to compromise the confidentiality, integrity, or availability of your service or data\. The CVE system provides a reference method for publicly known information security vulnerabilities and exposures\. For more information, go to [ https://cve\.mitre\.org/](https://cve.mitre.org/)\. 

If a particular CVE appears in a *finding* produced by an Amazon Inspector assessment, you can search [https://cve\.mitre\.org/](https://cve.mitre.org/) for the CVE's ID \(for example, **CVE\-2009\-0021**\)\. The search results can provide detailed information about this CVE, its severity, and how to mitigate it\.

The rules included in this package help you assess whether your EC2 instances are exposed to the CVEs in the following list: [https://s3\-us\-west\-2\.amazonaws\.com/rules\-engine/CVEList\.txt](https://s3-us-west-2.amazonaws.com/rules-engine/CVEList.txt)\. The CVE rules package is updated regularly; this list includes the CVEs that are included in assessments runs that occur at the same time that this list is retrieved\. 

For more information, see [Rules Packages Availability Across Supported Operating Systems](inspector_rule-packages_across_os.md)\.