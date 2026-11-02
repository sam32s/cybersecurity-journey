## FTP Security Assessment

### 1. Service Identification

Nmap identified the following service:

- Port: 21/tcp
- Service: FTP
- Version: vsftpd 2.3.4
- Status: Open

### 2. Anonymous Authentication

An FTP anonymous login test confirmed that anonymous authentication is permitted.

The server returned:

- FTP response: 230 Login successful
- Logged-in account: ftp
- Initial remote directory: /

The directory listing showed no additional files or folders.

### 3. FTP Server Information

The ftp-syst Nmap script revealed:

- Control connection: Plain text
- Data connection: Plain text
- Session timeout: 300 seconds
- Transfer mode: ASCII

### 4. Security Risks

The assessment identified these potential risks:

- Anonymous access may expose files to unauthorized users.
- Plain-text FTP communication can expose credentials and transferred data to network observers.
- The server uses an old FTP software version that warrants further security review.

### 5. Recommended Mitigations

- Disable anonymous FTP access unless explicitly required.
- Replace FTP with SFTP or another encrypted file-transfer solution.
- Restrict access using firewall rules.
- Keep FTP software updated.
- Apply appropriate file and directory permissions.

### 6. Conclusion

The assessment confirmed that the target permits anonymous FTP authentication and uses unencrypted FTP control and data connections.

These configurations create potential confidentiality and access-control risks.
