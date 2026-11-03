# Stored Cross-Site Scripting (XSS) Assessment

## 1. Objective
To investigate Stored Cross-Site Scripting (XSS) vulnerabilities in DVWA and compare how different security levels handle submitted user input.

## 2. Lab Environment
- Testing machine: Kali Linux
- Target: Metasploitable 2
- Target IP: 192.168.50.20
- Application: DVWA v1.0.7
- Browser: Firefox
- Testing environment: Isolated VirtualBox lab

## 3. Baseline Test

Submitted normal text through the guestbook form.

**Name:** CyberStudent

**Message:** This is my first stored XSS security test.

**Observation:**
The application stored the message and displayed it in the guestbook.

This demonstrated how submitted information can persist and be displayed to users later.

## 4. Source Code Analysis

### Low Security

The Low security implementation uses:

```php
$message = mysql_real_escape_string($message);
$name = mysql_real_escape_string($name);

Finding:
The application applies SQL escaping but does not encode HTML characters. This leaves the application vulnerable to unsafe HTML output.

###Medium Security

The Medium implementation uses:
$message = trim(strip_tags(addslashes($message)));
$message = mysql_real_escape_string($message);

$name = str_replace('<script>', '', $name);
$name = mysql_real_escape_string($name);

Finding:
The application attempts to filter HTML tags from messages and remove a specific script tag from names.

However, these filters are incomplete and do not provide reliable XSS protection.

###High Security

The High implementation uses:

$message = htmlspecialchars($message);
$name = htmlspecialchars($name);
Finding:
Special HTML characters are encoded before the submitted values are stored.

This helps prevent the browser from interpreting the submitted HTML as markup.

5. Practical Testing

Tested harmless HTML input:
<b>Stored XSS Lab Test</b>
Low Security

Observation: The browser interpreted the HTML tags, displaying the message in bold.

Medium Security

Observation: The results were inconsistent. Some entries displayed as HTML while others appeared as text.

This demonstrated that basic filtering is not a reliable security control.

High Security

Observation: HTML tags were encoded and displayed as text rather than interpreted as HTML.

6. Security Comparison
Security Level	Protection	Observation
Low	SQL escaping	HTML was interpreted
Medium	Basic HTML filtering	Incomplete protection
High	HTML character encoding	HTML displayed as text


7. Security Findings
Stored XSS involves user input being saved and displayed later.
Low security does not adequately protect against HTML injection.
Medium security uses incomplete filtering techniques.
High security uses HTML character encoding to reduce XSS risk.
Stored XSS can affect other users who view malicious stored content.


8. Recommendations
Apply context-appropriate output encoding when displaying user-generated content.
Use parameterized SQL queries or prepared statements.
Avoid relying on simple string replacement as an XSS defense.
Validate user input appropriately.
Implement Content Security Policy (CSP) as an additional security layer.
Conduct regular security testing of web applications.


9. Conclusion

The assessment demonstrated how different security controls affect Stored XSS risks.

Low security allowed HTML interpretation, Medium used incomplete filtering, and High encoded HTML characters.

The exercise highlighted the importance of secure input handling, output encoding, and proper database query practices.

