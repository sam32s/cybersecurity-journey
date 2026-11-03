# Reflected Cross-Site Scripting (XSS) Assessment

## 1. Objective
To investigate how DVWA handles user input and identify reflected XSS risks at different security levels.

## 2. Lab Environment
- Application: Damn Vulnerable Web Application (DVWA)
- Target: Metasploitable 2
- Lab IP: 192.168.50.20
- Testing machine: Kali Linux
- Browser: Firefox

## 3. Normal Input Test
Submitted normal text through the name input field.

**Input:** isaac

**Observation:** The application displayed "Hello isaac".

This confirmed that user input was reflected in the HTTP response.

## 4. Source Code Analysis

### Low Security
```php
echo 'Hello ' . $_GET['name'];

Medium Security
str_replace('<script>', '', $_GET['name']);
The application attempts to remove script tags. This is insufficient protection because filtering a single string is not reliable.

High Security
htmlspecialchars($_GET['name']);

5. Findings
Low security directly displays user input.
Medium security uses basic string filtering.
High security applies HTML character encoding.
Reflected user input requires appropriate output encoding.

6. Recommendations
Use context-appropriate output encoding.
Avoid relying on simple string replacement.
Validate input where appropriate.
Implement a Content Security Policy (CSP) as an additional defense.
Use secure coding practices and test all input fields.

7. Conclusion
The assessment demonstrated how different input-handling techniques affect reflected XSS risk.
 Output encoding provides stronger protection than basic string filtering or displaying untrusted input directly.
