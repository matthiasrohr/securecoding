#  SEC-C - Encoding/Escaping at the Frontend (Preventing XSS)

## Category

## Relevant Threats
* SEC-T - Cross-Site Scripting (XSS)
* SEC-T - Reflected File Download (RFD)
* SEC-T - AngularJS Strict Contextual Escaping (SCE) Disabled

### HTML Entity Encoding & Escaping
Cross-site Scripting (XSS) attacks can be prevented or made more difficult by several countermeasures. The principal one that fixes the root cause of this vulnerability is correct (= context-sensitive) is output encoding of all parameters/variables that can potentially be user-controlled. Each output context has a specific encoding technique that needs to be applied:

|  Context  | Method | Input | Output |
| ------------- | ------------- | ------------- | ------------- |
| HTML (Body / Attribute)  | HTML Entity Encoding  | '  "  >  <  | `&#x27;` `&#x22;` `&#x3E;` `&#x3C;` |
| JavaScript Variable  | JavaScript Escaping | ' | \' |
| GET Parameter | URL Encoding | & | %26 |
| CSS | CSS Escaping | | |
| HTML | HTML Sanitization (see below) | | |
| JSON | JSON Serialization | | |
| DOM | use safe JS APIs / Trusted Types (see below) | | |

### HTML Input Sanitization
See SEC-C - Restrictive Input Validation (HTML) for instructions on how to handle input safely, which is allowed to consist of certain markup.

### JavaScript Sanitization
When user-controlled input is written into the DOM using insecure APIs it needs to be sanitized as well. Details can be found in the implementation notes below. 

### Trusted Types
See SEC-C - Trusted Types.

### Content Security Policy (CSP)
The Content Security Policy (CSP) can provide additional protection against XSS attacks. See SEC-C - Content Security Policy (CSP).

## Vulnerable Code 
The following code snippet shows three ways to implement an XSS vulnerability in a JSP file:

```js
Value: ${bean.value1}
Value: <%= ${bean.value1} %>
<h:outputText value="#{bean.value2}" escape="false"/>

```

In the first two examples, the bean value "value1" is simply written into the view, which happens unvalidated (= not encoded). In the third example, we use <outputText>, a common JSF tag for writing output into the view. The standard behavior of this tag is that it automatically encodes all output.

However, since the developer used the attribute escape="false", this standard secure behavior is turned off and this tag is hence insecure. Similar ways to write output into the view can be found in almost all other languages and Web frameworks.

## Coding Guidelines


## References
* OWASP Encoder API: https://www.owasp.org/index.php/OWASP_Java_Encoder_Project
* XSS Prevention Cheat Sheet: https://www.owasp.org/index.php/XSS_%28Cross_Site_Scripting%29_Prevention_Cheat_Sheet
* CWE-79: http://cwe.mitre.org/data/definitions/79.html
