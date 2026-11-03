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
