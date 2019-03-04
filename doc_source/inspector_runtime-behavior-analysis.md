# Runtime Behavior Analysis<a name="inspector_runtime-behavior-analysis"></a>

The rules in the Runtime Behavior Analysis rules package analyze the behavior of your instances during an assessment run\. They also provide guidance about how to make your EC2 instances more secure\.

For more information, see [Amazon Inspector Rules Packages for Supported Operating Systems](inspector_rule-packages_across_os.md)\.

**Topics**
+ [Non\-Secure Client Protocols \(Login\)](#insecure-client-protocols-login)
+ [Non\-Secure Client Protocols \(General\)](#insecure-client-protocols-general)
+ [Unused Listening TCP Ports](#unused-tcp-ports)
+ [Non\-Secure Server Protocols](#insecure-protocols)
+ [Software Without Data Execution Prevention \(DEP\)](#dep-os)
+ [Root Process with Non\-Secure Permissions](#root-process-with-insecure-permissions)

## Non\-Secure Client Protocols \(Login\)<a name="insecure-client-protocols-login"></a>

This rule detects a client's use of insecure protocols to log in to remote machines\.

**Important**  
Currently, you can include in your assessment targets EC2 instances that are running either Linux\-based or Windows\-based operating systems\.   
This rule generates findings for the EC2 instances that are running either Linux\-based or Windows\-based operating systems\.

### Severity: [Medium](inspector_rule-packages.md#SeverityLevels)<a name="insecure-client-protocols-login-severity"></a>

### Finding<a name="insecure-client-protocols-login-finding"></a>

An EC2 instance in your assessment target uses insecure protocols to connect to a remote host for login\. These protocols do not secure credentials in the clear, increasing the risk of credential theft\.

### Resolution<a name="insecure-client-protocols-login-resolution"></a>

It is recommended that you replace these insecure protocols with secure protocols, such as SSH\.

## Non\-Secure Client Protocols \(General\)<a name="insecure-client-protocols-general"></a>

This rule detects a client's use of non\-secure protocols\.

**Important**  
Currently, you can include in your assessment targets EC2 instances that are running either Linux\-based or Windows\-based operating systems\.   
This rule generates findings for the EC2 instances that are running either Linux\-based or Windows\-based operating systems\.

### Severity: [Low](inspector_rule-packages.md#SeverityLevels)<a name="insecure-client-protocols-general-severity"></a>

### Finding<a name="insecure-client-protocols-general-finding"></a>

An EC2 instance in your assessment target uses non\-secure protocols to connect to a remote host\. These protocols do not secure traffic, increasing the risk of a successful traffic interception attack\. 

### Resolution<a name="insecure-client-protocols-general-resolution"></a>

It is recommended that you replace these non\-secure protocols with encrypted versions\.

## Unused Listening TCP Ports<a name="unused-tcp-ports"></a>

This rule detects listening TCP ports that might not be required by the assessment target\.

**Important**  
Currently, you can include in your assessment targets EC2 instances that are running either Linux\-based or Windows\-based operating systems\.   
This rule generates findings for the EC2 instances that are running either Linux\-based or Windows\-based operating systems\.

### Severity: [Informational](inspector_rule-packages.md#SeverityLevels)<a name="unused-tcp-ports-severity"></a>

### Finding<a name="unused-tcp-ports-finding"></a>

An EC2 instance in your assessment target is listening on TCP ports, but Amazon Inspector didn't discover any traffic to these ports during the assessment run\.

### Resolution<a name="unused-tcp-ports-resolution"></a>

To reduce the attack surface area of your deployments, we recommend that you disable network services that you do not use\. Where network services are required, we recommend that you employ network control mechanisms such as VPC ACLs, EC2 security groups, and firewalls to limit exposure of that service\.

## Non\-Secure Server Protocols<a name="insecure-protocols"></a>

This rule helps determine whether your EC2 instances allow support for non\-secure and unencrypted ports or services such as FTP, Telnet, HTTP, IMAP, POP version 3, SMTP, SNMP versions 1 and 2, RSH, and `rlogin`\.

**Important**  
Currently, you can include in your assessment targets EC2 instances that are running either Linux\-based or Windows\-based operating systems\.   
This rule generates findings for the EC2 instances that are running either Linux\-based or Windows\-based operating systems\.

### Severity: [Informational](inspector_rule-packages.md#SeverityLevels)<a name="insecure-protocols-severity"></a>

### Finding<a name="insecure-protocols-finding"></a>

An EC2 instance in your assessment target is configured to support insecure protocols\.

### Resolution<a name="insecure-protocols-resolution"></a>

We recommend that you disable non\-secure protocols that are supported on an EC2 instance in your assessment target, and replace them with more secure alternatives as listed below:
+ Disable Telnet, RSH, and `rlogin` and replace them with SSH\. Where this is not possible, you should ensure that the non\-secure service is protected by appropriate network access controls such as VPC network ACLs and EC2 security groups\.
+ Replace FTP with SCP or SFTP where possible\. Where this is not possible, you should ensure that the FTP server is protected by appropriate network access controls such as VPC network ACLs and EC2 security groups\.
+ Replace HTTP with HTTPS where possible\. For more information specific to the web server in question, see `http://nginx.org/en/docs/http/configuring_https_servers.html` and `http://httpd.apache.org/docs/2.4/ssl/ssl_howto.html`\.
+ Disable IMAP, POP3, and SMTP services if not required\. If required, we recommend that these email protocols are used with encrypted protocols such as TLS\.
+ Disable SNMP service if not required\. If required, replace SNMP v1and v2 with the more secure SNMP v3, which uses encrypted communication\.

## Software Without Data Execution Prevention \(DEP\)<a name="dep-os"></a>

This rule detects the presence of third\-party software that is compiled without support for Data Execution Prevention \(DEP\)\. DEP increases system security by defending against stack\-based buffer overflow and other memory corruption attacks\.

**Important**  
Currently, you can include in your assessment targets EC2 instances that are running either Linux\-based or Windows\-based operating systems\.   
During an assessment run, this rule generates findings **only** for the EC2 instances that are running Linux\-based operating systems\. This rule does NOT generate findings for EC2 instances that are running Windows\-based operating systems\.

### Severity: [Medium](inspector_rule-packages.md#SeverityLevels)<a name="dep-os-severity"></a>

### Finding<a name="dep-os-finding"></a>

There are executable files on an EC2 instance in your assessment target that do not support DEP\.

### Resolution<a name="dep-os-resolution"></a>

We recommend that you uninstall this software from your assessment target if you are not using it, or contact the vendor to get an updated version of this software with DEP enabled\.

## Root Process with Non\-Secure Permissions<a name="root-process-with-insecure-permissions"></a>

This rule helps detect root processes that load modules that can be modified by unauthorized users\.

**Important**  
Currently, you can include in your assessment targets EC2 instances that are running either Linux\-based or Windows\-based operating systems\.   
During an assessment run, this rule generates findings **only** for the EC2 instances that are running Linux\-based operating systems\. This rule does NOT generate findings for EC2 instances that are running Windows\-based operating systems\.

### Severity: [High](inspector_rule-packages.md#SeverityLevels)<a name="root-process-with-insecure-permissions-severity"></a>

### Finding<a name="root-process-with-insecure-permissions-finding"></a>

There is an instance in your assessment target with one or more root\-owned processes that make use of shared objects that are vulnerable to unauthorized modification\. These shared objects have inappropriate permissions/ownership and are therefore vulnerable to tampering\.

### Resolution<a name="root-process-with-insecure-permissions-resolution"></a>

To improve the security of your assessment target, we recommend that you correct the permissions on the relevant modules to ensure that they are writable only by the root user\.