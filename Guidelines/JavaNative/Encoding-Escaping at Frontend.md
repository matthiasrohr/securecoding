# Java: Encoding/Escaping at the Frontend (Preventing XSS)

## StringEscapeUtils (Apache Commons)

One of the most common ways to perform HTML Entity Encoding in Java is by using the Apache Commons StringEscapeUtils:

As an example, the following code is safe:

```java
<body><%= StringEscapeUtils.escapeHtml(bean.value1) %></body>
<button
 onclick="alert('<%=  StringEscapeUtils.escapeEcmaScript(bean.value1) %>');">
 click me</button>
<div style="width:<%=  StringEscapeUtils.escapeHtml(bean.value1) %>">
```

## Expression Language (EL)

Within JSP files you can use expression language to encode bean variables:

```java
<%@ taglib uri="http://java.sun.com/jsp/jstl/functions" prefix="fn"%>
...
<li><a class="current" href="#"><b>[${fn:escapeXml(name)}]</b></a></li>
```

## OWASP Java Encoding Project

The OWASP organization has implemented a JAVA API described in OWASP Java Encoding Project.

The following examples show how parameters can be handled securely for different output contexts:

|  Context  | Example |
| ------------- | ------------- | 
| HTML | ```<body><%= Encode.forHtml(textValue) %></body>``` |
| HTML Attribute |  | 
| JavaScript Blocks |  | 
| JavaScript Variables |  |
| URLs |  |

## Secure Processing of HTML

In case an application needs to process untrusted HTML data (e.g. users can commit comments with markups), it is highly important that this markup is validated by a mature Java HTML sanitizer. Such an API sanitizes untrusted data and converts it to a safe form:

Example:

```java
PolicyFactory policy = new HtmlPolicyBuilder()
String safeHTML = policy.sanitize(untrustedHTML);
Die
 verwendete Policy lässt sich darüber hinaus weiter anpassen. Sollen 
Benutzern etwa auch die Möglichkeit besitzen bestimmte Links
einzugeben, so lässt sich die folgende Policy verwenden:
PolicyFactory policy = new HtmlPolicyBuilder()
.allowElements("a")
.allowUrlProtocols("https")
.allowAttributes("href").onElements("a")
.requireRelNofollowOnLinks()
.build();
String safeHTML = policy.sanitize(untrustedHTML);
```

#### Implementation via Bean Validation

Java Bean Validation provides the annotation @SafeHtml that too performs HTML validation:

Example:
```java
@SafeHtml
public String getHtml();
```

## References
* Java HTML Sanitizer: GitHub - OWASP/java-html-sanitizer: Takes third-party HTML and produces HTML that is safe to embed in your web application.  Fast and easy to configure. 
* Semgrep Coding Guideline on XSS prevention for Java + JSP: XSS prevention for Java + JSP | Semgrep 
