# Security Best Practices for Amazon Inspector<a name="inspector_security-best-practices"></a>

Use Amazon Inspector rules to help determine whether your systems are configured securely\.

**Important**  
Currently, you can include in your assessment targets EC2 instances that are running either Linux\-based or Windows\-based operating systems\.   
During an assessment run, the rules described in this section generate findings **only** for the EC2 instances that are running Linux\-based operating systems\. The rules do not generate findings for EC2 instances that are running Windows\-based operating systems\.  
For more information, see [Amazon Inspector Rules Packages for Supported Operating Systems](inspector_rule-packages_across_os.md)\.

**Topics**
+ [Disable Root Login over SSH](#disable-root-login-over-SSH)
+ [Support SSH Version 2 Only](#support-ssh-v2-only)
+ [Disable Password Authentication Over SSH](#disable-password-authentication-over-ssh)
+ [Configure Password Maximum Age](#password-maximum-age)
+ [Configure Password Minimum Length](#password-minimum-length)
+ [Configure Password Complexity](#password-complexity)
+ [Enable ASLR](#ASLR)
+ [Enable DEP](#DEP-OS)
+ [Configure Permissions for System Directories](#permissions-for-system-directories)

## Disable Root Login over SSH<a name="disable-root-login-over-SSH"></a>

This rule helps determine whether the SSH daemon is configured to permit logging in to your EC2 instance as [root ](http://docs.aws.amazon.com/general/latest/gr/root-vs-iam.html)\.

### Severity: [Medium](inspector_rule-packages.md#SeverityLevels)<a name="disable-root-login-over-SSH-severity"></a>

### Finding<a name="disable-root-login-over-SSH-finding"></a>

There is an EC2 instance in your assessment target that is configured to allow users to log in with root credentials over SSH\. This increases the likelihood of a successful brute\-force attack\. 

### Resolution<a name="disable-root-login-over-SSH-resolution"></a>

We recommend that you configure your EC2 instance to prevent root account logins over SSH\. Instead, log in as a non\-root user and use `sudo` to escalate privileges when necessary\. To disable SSH root account logins, set `PermitRootLogin` to `no` in the `/etc/ssh/sshd_config` file, and then restart `sshd`\.

## Support SSH Version 2 Only<a name="support-ssh-v2-only"></a>

This rule helps determine whether your EC2 instances are configured to support SSH protocol version 1\. 

### Severity: [Medium](inspector_rule-packages.md#SeverityLevels)<a name="support-ssh-v2-only-severity"></a>

### Finding<a name="support-ssh-v2-only-finding"></a>

An EC2 instance in your assessment target is configured to support SSH\-1, which contains inherent design flaws that greatly reduce its security\. 

### Resolution<a name="support-ssh-v2-only-resolution"></a>

We recommend that you configure EC2 instances in your assessment target to support only SSH\-2 and later\. For OpenSSH, you can achieve this by setting `Protocol 2` in the `/etc/ssh/sshd_config` file\. For more information, see `man sshd_config`\.

## Disable Password Authentication Over SSH<a name="disable-password-authentication-over-ssh"></a>

This rule helps determine whether your EC2 instances are configured to support password authentication over the SSH protocol\.

### Severity: [Medium](inspector_rule-packages.md#SeverityLevels)<a name="disable-password-authentication-over-ssh-severity"></a>

### Finding<a name="disable-password-authentication-over-ssh-finding"></a>

An EC2 instance in your assessment target is configured to support password authentication over SSH\. Password authentication is susceptible to brute\-force attacks and should be disabled in favor of key\-based authentication where possible\.

### Resolution<a name="disable-password-authentication-over-ssh-resolution"></a>

We recommend that you disable password authentication over SSH on your EC2 instances and enable support for key\-based authentication instead\. This significantly reduces the likelihood of a successful brute\-force attack\. For more information, see [https://aws\.amazon\.com/articles/1233/](https://aws.amazon.com/articles/1233/)\. If password authentication is supported, it is important to restrict access to the SSH server to trusted IP addresses\.

## Configure Password Maximum Age<a name="password-maximum-age"></a>

This rule helps determine whether the maximum age for passwords is configured on your EC2 instances\.

### Severity \- [Medium](inspector_rule-packages.md#SeverityLevels)<a name="password-maximum-age-severity"></a>

### Finding<a name="password-maximum-age-finding"></a>

An EC2 instance in your assessment target is not configured for a maximum age for passwords\.

### Resolution<a name="password-maximum-age-resolution"></a>

If you are using passwords, we recommend that you configure a maximum age for passwords on all EC2 instances in your assessment target\. This requires users to regularly change their passwords and reduces the chances of a successful password guessing attack\. To fix this issue for existing users, use the chage command\. To configure a maximum age for passwords for all future users, edit the `PASS_MAX_DAYS` field in the `/etc/login.defs` file\. 

## Configure Password Minimum Length<a name="password-minimum-length"></a>

This rule helps determine whether a minimum length for passwords is configured on your EC2 instances\.

### Severity: [Medium](inspector_rule-packages.md#SeverityLevels)<a name="password-minimum-length-severity"></a>

### Finding<a name="password-minimum-length-finding"></a>

An EC2 instance in your assessment target is not configured for a minimum length for passwords\. 

### Resolution<a name="password-minimum-length-resolution"></a>

If you are using passwords, we recommend that you configure a minimum length for passwords on all EC2 instances in your assessment target\. Enforcing a minimum password length reduces the risk of a successful password guessing attack\. To enforce minimum password lengths, set the `minlen` parameter of `pam_cracklib.so` in your PAM configuration\. For more information, see `man pam_cracklib`\.

## Configure Password Complexity<a name="password-complexity"></a>

This rule helps determine whether a password complexity mechanism is configured on your EC2 instances\. 

### Severity: [Medium](inspector_rule-packages.md#SeverityLevels)<a name="password-complexity-severity"></a>

### Finding<a name="password-complexity-finding"></a>

No password complexity mechanism or restrictions are configured on EC2 instances in your assessment target\. This allows users to set simple passwords, which increases the chances of unauthorized users gaining access and misusing accounts\. 

### Resolution<a name="password-complexity-resolution"></a>

If you are using passwords, we recommend that you configure all EC2 instances in your assessment target to require a level of password complexity\. You can do this by using the following options in the `pwquality.conf` file: `lcredit`, `ucredit`, `dcredit`, and `ocredit`\. For more information, see [https://linux\.die\.net/man/5/pwquality\.conf](https://linux.die.net/man/5/pwquality.conf) \. If `pwquality.conf` is not available on your instance, you can set the `lcredit`, `ucredit`, `dcredit`, and `ocredit` options using the `pam_cracklib.so` module\. For more information, see `man pam_cracklib`\. 

## Enable ASLR<a name="ASLR"></a>

This rule helps determine whether address space layout randomization \(ASLR\) is enabled on the operating systems of the EC2 instances in your assessment target\.

### Severity: [Medium](inspector_rule-packages.md#SeverityLevels)<a name="ASLR-severity"></a>

### Finding<a name="ASLR-finding"></a>

An EC2 instance in your assessment target does not have ASLR enabled\.

### Resolution<a name="ASLR-resolution"></a>

To improve the security of your assessment target, we recommend that you enable ASLR on the operating systems of all EC2 instances in your target by running echo 2 \| sudo tee /proc/sys/kernel/randomize\_va\_space\.

## Enable DEP<a name="DEP-OS"></a>

This rule helps determine whether Data Execution Prevention \(DEP\) is enabled on the operating systems of the EC2 instances in your assessment target\.

### Severity: [Medium](inspector_rule-packages.md#SeverityLevels)<a name="DEP-OS-severity"></a>

### Finding<a name="DEP-OS-finding"></a>

An EC2 instance in your assessment target does not have DEP enabled\.

### Resolution<a name="DEP-OS-resolution"></a>

We recommend that you enable DEP on the operating systems of all EC2 instances in your assessment target\. Enabling DEP protects your instances from security compromises using buffer\-overflow techniques\.

## Configure Permissions for System Directories<a name="permissions-for-system-directories"></a>

This rule checks permissions on system directories that contain binaries and system configuration information\. It checks that only the root user \(a user who logs in by using root account credentials\) has write permissions for these directories\.

### Severity: [High](inspector_rule-packages.md#SeverityLevels)<a name="permissions-for-system-directories-severity"></a>

### Finding<a name="permissions-for-system-directories-finding"></a>

An EC2 instance in your assessment target contains a system directory that is writable by non\-root users\.

### Resolution<a name="permissions-for-system-directories-resolution"></a>

To improve the security of your assessment target and to prevent privilege escalation by malicious local users, configure all system directories on all EC2 instances in your target to be writable only by users who log in by using root account credentials\.