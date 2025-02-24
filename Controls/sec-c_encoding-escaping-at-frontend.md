---
toc: true
toc_label: "Table of Contents"
toc_icon: "cog"
toc_sticky: true
---

# SEC-C - Encoding/Escaping at the Frontend (Preventing XSS)

## Category

## Relevant Threats

ä Details

### HTML Entity Encoding & Escaping

### HTML Sanitization

### JavaScript Sanitization

### Trusted Types

### Content Security Policy (CSP)

## Vulnerable Code 
The following code snippet shows three ways to implement an XSS vulnerability in a JSP file:

```js
Value: ${bean.value1}
Value: <%= ${bean.value1} %>
<h:outputText value="#{bean.value2}" escape="false"/>

```

## Coding Guidelines


## References
