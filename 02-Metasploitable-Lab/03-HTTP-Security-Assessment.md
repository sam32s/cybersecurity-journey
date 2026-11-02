# HTTP Security Assessment

## 1. Service Identification

- Port: 80/tcp
- Service: HTTP
- Web Server: Apache 2.2.8
- Operating System: Ubuntu
- PHP Version: 5.2.4
- WebDAV: DAV/2 advertised

## 2. HTTP Header Analysis

The HTTP response revealed:

- HTTP Status: 200 OK
- Server: Apache/2.2.8 (Ubuntu) DAV/2
- X-Powered-By: PHP/5.2.4
- Content-Type: text/html

Security Observation:
The server discloses its Apache and PHP versions through HTTP headers.

## 3. HTTP Methods

Nmap identified the following supported methods:

- GET
- HEAD
- POST
- OPTIONS

These methods are not inherently vulnerabilities. Their use should be restricted according to application requirements.

## 4. Web Applications Discovered

The homepage exposed links to:

- TWiki
- phpMyAdmin
- Mutillidae
- DVWA
- WebDAV

These applications provide additional areas for security assessment.

## 5. WebDAV Directory Inspection

A request to /dav/ returned:

- HTTP Status: 200 OK
- Directory listing: Enabled
- Visible files: None

Security Observation:
Directory listing exposes the directory structure to visitors. No files were visible during this assessment.

## 6. Security Risks

- Software version disclosure.
- Use of outdated Apache and PHP versions.
- Directory listing enabled.
- Potential exposure through additional web applications.

## 7. Recommended Mitigations

- Upgrade Apache and PHP to supported versions.
- Remove unnecessary version information from HTTP headers.
- Disable directory listing where unnecessary.
- Restrict access to administrative applications.
- Review WebDAV permissions and disable unnecessary functionality.
- Enforce HTTPS for web applications.

## 8. Conclusion

The assessment identified outdated web-server software, version disclosure, multiple hosted applications, and directory listing enabled on the WebDAV directory.

Further testing is required to establish whether WebDAV permits unauthorized file modification.
