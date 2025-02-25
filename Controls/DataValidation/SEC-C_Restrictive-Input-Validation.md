# SEC-C - Restrictive Input Validation (Generic)

## Category
Data Validation & Secure Data Processing

## Description
Since basically all attacks against web applications are conducted by some sort of crafted input data, restricting these inputs is generally a good approach to improve from a security perspective. Only a few vulnerabilities originate in insecure input validation (e.g. business logic flaws) though. In most cases, input validation is an additional measure that can prevent the exploitation of vulnerabilities (e.g. SQL Injection or Cross-site Scripting). Restrictive input validation means being as restrictive as it is allowed by the specification.

<details>
<summary>My top languages</summary>

| Rank | Languages |
|-----:|-----------|
|     1| JavaScript|
|     2| Python    |
|     3| SQL       |

</details>

> [!NOTE]
> Restrictive input validation is a secondary line of defense for most attacks. It can often prevent the exploitation of certain attacks without fixing the root cause.

Validation of application parameters is discussed at SEC-C - Ensure Application Integrity (Application Parameters).

## Relevant Threats
* SEC-T - Manipulation of Business Logic
* SEC-T - SQL/JPA/HQL Injection
* SEC-T - LDAP Injection
* SEC-T - Cross-Site Scripting (XSS)
* SEC-T - Log Forging (CRLF Injection)
* SEC-T - Server-Side Template Injection (SSTI)
* SEC-T - Server Side Include (SSI) Injection
* SEC-T - Remote Code Execution (RCE)
* SEC-T - Path Traveral
* SEC-T - OS Command Injection
* SEC-T - Remote Code Execution (RCE)
* SEC-T - IMAP/SMTP Injection
* SEC-T - Insecure Deserialization
* SEC-T - Insecure Autobinding (Mass Assignment)
* SEC-T - Application DoS

# Sub Pages
* SEC-C - Restrictive Input Validation (Paths and Filenames)
* SEC-C - Restrictive Input Validation (Files)
* SEC-C - Restrictive Input Validation (HTML)
* SEC-C - Restrictive Input Validation (JSON)
* SEC-C - Restrictive Input Validation (URLs)
* SEC-C - Restrictive Input Validation (XML)
* SEC-C - Restrictive Input Validation (ZIP Files)

# Details
## Principles
Principles
There are certain security principles that apply to input validation:
- *Validate on the server side*: Security-relevant input validation must be performed on the server side. In addition, you can, of course, perform input validation on the client side to improve the user experience.
- *Be as restrictive as possible:* Only allow input that is required according to the business requirement - and restrict it as much as possible
- *Validate known goods:* Whitelist validation (accepting only known good data) is a key to good security. Check the content of the data, the length, data type, etc.

## Regular Expressions
We distinguish different validation techniques such as value comparison, typecasting, sanitizing, or regular expressions. The latter is very handy since they provide a lot of flexibility for validating input:

| Expression  | Explanation |
| ------------- | ------------- |
| /^[a-zA-ZöÖäÄüÜ0-9 .\-=_?\[\](){}#*;:|\\$&§!%+#]+$/  | Only characters that are safe against most injection attacks |
| /^[a-zA-ZöÖäÄüÜ0-9]+$/  | Alphanumeric characters  |
| /^[0-9]{5}$/  | German postal codes  |
| /^(null|two|three)$/  | „null“, „two“ or „three“ |

The problem with Regular Expressions is, however, that they can be specified rather complex which makes it difficult to understand their logic and verify them.

## Typecasting
Also, make sure that you do not use "evil" regular expressions that may allow an attacker to carry out a denial of service attack (see SEC-C - Safe Regular Expressions).

> [!NOTE]
> Be careful with complex Regular Expressions and use multiple simple expressions or secure APIs instead.

# Coding Guidelines
TBD

# References
* OWASP Input Validation Cheat Sheet: https://www.owasp.org/index.php/Input_Validation_Cheat_Sheet
* OWASP Validation Regex Repository: https://www.owasp.org/index.php/OWASP_Validation_Regex_Repository
* Java EE 6 Tutorial about Bean Validation: http://docs.oracle.com/javaee/6/tutorial/doc/gircz.html
