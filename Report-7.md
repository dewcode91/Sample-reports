# Import calendar from the URL feature's can lead to blind SSRF

#### Description
While exploring calendar application, i noticed an endpoint that allows a user to import the calendar from external resources. A malicious user can abuse this feature to interact with the internal networks or performing the port scans.

During my investigation, I noticed if a user tries to import a calendar from http://127.0.0.1/. The server will respond with the error message `unsupported_url`

But if the user tries to import a calendar from http://127.0.0.1:22 (with the port number) then he can successfully import a blank calendar from the local server. I tested port 1-1000 and found port 22,25 and 873 are responding.

This behavior can lead to performing port scanning to the internal network or may be possible to read internal files from the server.

#### Steps to reproduce
1. Browse and sign in https://calendar.example.com
2. Observe import icon infront of Calendars > Click from a URL
3. Now try to import calendar from http://127.0.0.1:22 and observe the response

#### Impact
Exploiting this vulnerability, an attacker can perform a range of malicious activities, including but not limited to:

- Information Disclosure: By accessing internal resources, the attacker can gather sensitive information such as server configuration, application data, or credentials.

- Network Scanning: The attacker can use the application server as a proxy to scan other internal systems, potentially identifying additional vulnerabilities or sensitive information.

- Internal Network Compromise: Exploiting SSRF can allow an attacker to access internal systems or services that are not intended to be exposed publicly, leading to further compromise, lateral movement, or unauthorized access.
