# Runtime Behavior Analysis<a name="inspector_runtime-behavior-analysis"></a>

These rules analyze the behavior of your instances during an assessment run, and provide guidance about how to make your EC2 instances more secure\.

For more information, see [Rules Packages Availability Across Supported Operating Systems](inspector_rule-packages_across_os.md)\.


+ [Insecure Client Protocols \(Login\)](#insecure-client-protocols-login)
+ [Insecure Client Protocols \(General\)](#insecure-client-protocols-general)
+ [Unused Listening TCP Ports](#unused-tcp-ports)
+ [Insecure Server Protocols](#insecure-protocols)
+ [Software Without DEP](#dep-os)
+ [Software Without Stack Cookies](#stack-cookies-enabled)
+ [Root Process with Insecure Permissions](#root-process-with-insecure-permissions)

## Insecure Client Protocols \(Login\)<a name="insecure-client-protocols-login"></a>

This rule detects a client's use of insecure protocols to log in to remote machines\.

**Important**  
In this release of Amazon Inspector, you can include in your assessment targets EC2 instances that are running either Linux\-based or Windows\-based operating systems\.   
This rule generates findings for the EC2 instances that are running either Linux\-based or Windows\-based operating systems\.

### Severity: Medium<a name="insecure-client-protocols-login-severity"></a>

### Finding<a name="insecure-client-protocols-login-finding"></a>

An EC2 instance in your assessment target uses insecure protocols to connect to a remote host for login\. These protocols pass credentials in the clear, increasing the risk of credential theft\.

### Resolution<a name="insecure-client-protocols-login-resolution"></a>

It is recommended that you replace these insecure protocols with secure protocols, such as SSH\.

## Insecure Client Protocols \(General\)<a name="insecure-client-protocols-general"></a>

This rule detects a client's use of insecure protocols\.

**Important**  
In this release of Amazon Inspector, you can include in your assessment targets EC2 instances that are running either Linux\-based or Windows\-based operating systems\.   
This rule generates findings for the EC2 instances that are running either Linux\-based or Windows\-based operating systems\.

### Severity: Low<a name="insecure-client-protocols-general-severity"></a>

### Finding<a name="insecure-client-protocols-general-finding"></a>

An EC2 instance in your assessment target uses insecure protocols to connect to a remote host\. These protocols pass traffic in the clear, increasing the risk of a successful traffic interception attack\. 

### Resolution<a name="insecure-client-protocols-general-resolution"></a>

It is recommended that you replace these insecure protocols with encrypted versions\.

## Unused Listening TCP Ports<a name="unused-tcp-ports"></a>

This rule detects listening TCP ports that may not be required by the assessment target\.

**Important**  
In this release of Amazon Inspector, you can include in your assessment targets EC2 instances that are running either Linux\-based or Windows\-based operating systems\.   
This rule generates findings for the EC2 instances that are running either Linux\-based or Windows\-based operating systems\.

### Severity: Informational<a name="unused-tcp-ports-severity"></a>

### Finding<a name="unused-tcp-ports-finding"></a>

An EC2 instance in your assessment target is listening on TCP ports but no traffic to these ports was seen during the assessment run\.

### Resolution<a name="unused-tcp-ports-resolution"></a>

To reduce the attack surface area of your deployments, we recommend that you disable network services that you do not use\. Where network services are required, we recommend that you employ network control mechanisms such as VPC ACLs, EC2 security groups, and firewalls to limit exposure of that service\.

## Insecure Server Protocols<a name="insecure-protocols"></a>

This rule helps determine whether your EC2 instances allow support for insecure and unencrypted ports/services such as FTP, Telnet, HTTP, IMAP, POP version 3, SMTP, SNMP versions 1 and 2, rsh, and rlogin\.

**Important**  
In this release of Amazon Inspector, you can include in your assessment targets EC2 instances that are running either Linux\-based or Windows\-based operating systems\.   
This rule generates findings for the EC2 instances that are running either Linux\-based or Windows\-based operating systems\.

### Severity: Informational<a name="insecure-protocols-severity"></a>

### Finding<a name="insecure-protocols-finding"></a>

An EC2 instance in your assessment target is configured to support insecure protocols\.

### Resolution<a name="insecure-protocols-resolution"></a>

We recommend that you disable insecure protocols that are supported on an EC2 instance in your assessment target and replace them with secure alternatives as listed below:

+ Disable Telnet, rsh, and rlogin and replace them with SSH\. Where this is not possible, you should ensure that the insecure service is protected by appropriate network access controls such as VPC network ACLs and EC2 security groups\.

+ Replace FTP with SCP or SFTP where possible\. Where this is not possible, you should ensure that the FTP server is protected by appropriate network access controls such as VPC network ACLs and EC2 security groups\.

+ Replace HTTP with HTTPS where possible\. For more information specific to the web server in question, see http://nginx\.org/en/docs/http/configuring\_https\_servers\.html and http://httpd\.apache\.org/docs/2\.4/ssl/ssl\_howto\.html\.

+ Disable IMAP, POP3, and SMTP services if not required\. If required, we recommend that these email protocols are used with encrypted protocols such as TLS\.

+ Disable SNMP service if not required\. If required, replace SNMP v1and v2 with the more secure SNMP v3, which uses encrypted communication\.

## Software Without DEP<a name="dep-os"></a>

This rule detects the presence of third\-party software that is compiled without support for Data Execution Prevention \(DEP\)\. DEP increases system security by defending against stack\-based buffer overflow and other memory corruption attacks\.

**Important**  
In this release of Amazon Inspector, you can include in your assessment targets EC2 instances that are running either Linux\-based or Windows\-based operating systems\.   
During an assessment run, this rule generates findings **only** for the EC2 instances that are running Linux\-based operating systems\. This rule does NOT generate findings for EC2 instances that are running Windows\-based operating systems\.

### Severity: Medium<a name="dep-os-severity"></a>

### Finding<a name="dep-os-finding"></a>

There are executable files on an EC2 instance in your assessment target that do not support DEP\.

### Resolution<a name="dep-os-resolution"></a>

It is recommended that you uninstall this software from your assessment target if you are not using it, or contact the vendor to get an updated version of this software with DEP enabled\.

## Software Without Stack Cookies<a name="stack-cookies-enabled"></a>

This rule detects the presence of third\-party software that is compiled without support for stack cookies\. Stack cookies increase system security by defending against stack\-based buffer overflow and other memory corruption attacks\.

**Important**  
In this release of Amazon Inspector, you can include in your assessment targets EC2 instances that are running either Linux\-based or Windows\-based operating systems\.   
During an assessment run, this rule generates findings **only** for the EC2 instances that are running Linux\-based operating systems\. This rule does NOT generate findings for EC2 instances that are running Windows\-based operating systems\.

### Severity: Medium<a name="stack-cookies-enabled-severity"></a>

### Finding<a name="stack-cookies-enabled-finding"></a>

There are executable files running on your EC2 instance that do not support stack cookies\.

### Resolution<a name="stack-cookies-enabled-resolution"></a>

It is recommended that you uninstall this software from your assessment target if you are not using it, or contact the vendor to get an updated version of this software with stack cookies enabled\.

## Root Process with Insecure Permissions<a name="root-process-with-insecure-permissions"></a>

This rule helps detect root processes that load modules that can be modified by unauthorized users\.

**Important**  
In this release of Amazon Inspector, you can include in your assessment targets EC2 instances that are running either Linux\-based or Windows\-based operating systems\.   
During an assessment run, this rule generates findings **only** for the EC2 instances that are running Linux\-based operating systems\. This rule does NOT generate findings for EC2 instances that are running Windows\-based operating systems\.

### Severity: High<a name="root-process-with-insecure-permissions-severity"></a>

### Finding<a name="root-process-with-insecure-permissions-finding"></a>

There is an instance in your assessment target with one or more root\-owned processes that make use of shared objects that are vulnerable to unauthorized modification\. These shared objects have inappropriate permissions/ownership and are therefore vulnerable to tampering\.

### Resolution<a name="root-process-with-insecure-permissions-resolution"></a>

To improve the security of your assessment target, it is recommended that you correct the permissions on the relevant modules to ensure that they are writable only by root\.