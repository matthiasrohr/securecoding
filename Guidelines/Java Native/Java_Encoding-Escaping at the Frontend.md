# Java: Encoding/Escaping at the Frontend (Preventing XSS)

## StringEscapeUtils (Apache Commons)

One of the most common ways to perform HTML Entity Encoding in Java is by using the Apache Commons StringEscapeUtils:

As an example, the following code is safe:

''js
<body><%= StringEscapeUtils.escapeHtml(bean.value1) %></body>
<button
 onclick="alert('<%=  StringEscapeUtils.escapeEcmaScript(bean.value1) %>');">
 click me</button>
<div style="width:<%=  StringEscapeUtils.escapeHtml(bean.value1) %>">
''

## Expression Language (EL)

Within JSP files you can use expression language to encode bean variables:

''js
<%@ taglib uri="http://java.sun.com/jsp/jstl/functions" prefix="fn"%>
...
<li><a class="current" href="#"><b>[${fn:escapeXml(name)}]</b></a></li>
''

## OWASP Java Encoding Project

The OWASP organization has implemented a JAVA API described in OWASP Java Encoding Project.

The following examples show how parameters can be handled securely for different output contexts:
