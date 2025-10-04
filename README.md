# Using-Wireshark---analyzing-web-browser-artifacts-email-header-analysis
## AIM:
To use Wireshark to analyze web browser activities and inspect email headers from captured network traffic.
## Architecture Diagram:
```mermaid
flowchart TD
    A[User System] --> B[Web Browser]
    A --> C[Email Client]
    B --> D[Network Traffic]
    C --> D
    D --> E[Wireshark Capture Engine]
    E --> F[Protocol Decoders HTTP SMTP IMAP POP]
    F --> G[Browser Artifacts URLs Cookies Auth]
    F --> H[Email Headers Source IP Server Timestamps]
    G --> I[Findings and Reports]
    H --> I
```
## DESIGN STEPS:
### Step 1:
- Install Wireshark and ensure correct network adapter selection.
- Enable packet capturing for your active interface (Wi-Fi/Ethernet).

### Step 2:
**Web Browser Artifact Analysis**
- Open a browser and visit websites with login forms (use dummy credentials).
- In Wireshark, filter traffic with:
    - ```http``` for normal HTTP requests
    - ```http.cookie``` for cookies
    - ```http.authbasic``` for basic authentication
- Identify:
    - URLs visited
    - GET/POST requests
    - Cookies & session IDs
    - Credentials (if plaintext HTTP is used)
### Step 3:
- Capture email traffic by sending/receiving emails (dummy mail server or provided PCAP).
- Use filters:
    - ```smtp``` (Simple Mail Transfer Protocol)
    - ```pop``` / ```imap``` (for received mail)
- Inspect email headers:
    - Source IP
    - Mail server hostname
    - Timestamps
    - Possible forged headers
## PROGRAM:
```mermaid
flowchart TD
    A[Start Wireshark Capture] --> B[Generate Traffic: Web Browsing & Emails]
    B --> C[Apply Protocol Filters: HTTP/SMTP/IMAP/POP]
    C --> D[Extract Browser Artifacts: URLs, Cookies, Credentials]
    C --> E[Analyze Email Headers: Source, Server, Metadata]
    D --> F[Save Findings]
    E --> F[Save Findings]
    F --> G[Generate Digital Forensic Report]

## A.Capturing Traffic in Wireshark
1.Open Wireshark and start capturing on the active interface (Wi- Fi/Ethernet).

<img width="1909" height="1021" alt="Screenshot 2025-10-04 131921" src="https://github.com/user-attachments/assets/9614e978-1d66-4ed3-9e12-89ebab0a8b8e" />

2.Perform activities like opening a website or sending an email through a client (e.g., Gmail via browser or Thunderbird).
<img width="1891" height="961" alt="Screenshot 2025-10-04 132932" src="https://github.com/user-attachments/assets/0a0d1a2a-2529-4f30-b45f-f126582cf1bc" />
4.Stop the capture once done.

## B. Analyzing Web Browser Artifacts
1.Apply filters like: http, tcp.port == 443 (for HTTPS), or dns to isolate browser traffic.
<img width="1915" height="1017" alt="Screenshot 2025-10-04 133403" src="https://github.com/user-attachments/assets/7c72d7ca-a947-4f3a-a41f-5dd5ce491cfd" />

2.Inspect HTTP GET/POST requests: o Look for URLs, hostnames, user agents, and cookies in the HTTP headers. o Follow TCP Stream to reconstruct page request flow: ▪ Right-click a packet → Follow → TCP Stream.
<img width="1919" height="993" alt="Screenshot 2025-10-04 133534" src="https://github.com/user-attachments/assets/b5bf5d75-1270-4c20-9e27-f69321ec74ef" />
Analyze DNS Queries: o Filter: dns o Reveal domains the browser tried to resolve.
<img width="1918" height="1020" alt="Screenshot 2025-10-04 133626" src="https://github.com/user-attachments/assets/5e223017-dbaf-4b44-94a1-05bd61f9948a" />
## C. Email Header Analysis
1.Apply relevant filters: o For POP3: tcp.port == 110 o For SMTP: tcp.port == 25 or 587 o For IMAP: tcp.port == 143 or 993
<img width="1900" height="1019" alt="Screenshot 2025-10-04 133856" src="https://github.com/user-attachments/assets/6dc6bf22-14fd-40d6-b967-f8539a7acb34" />
3.Locate email data: o Look for SMTP packets to see sender/receiver email addresses. o Use "Follow TCP Stream" to view the full email headers and body if unencrypted.
<img width="1913" height="561" alt="Screenshot 2025-10-04 134144" src="https://github.com/user-attachments/assets/a2f6e63e-29bd-49d4-83a2-110a1103cd36" />
5.Extract Email Header Fields: o Analyze From, To, Subject, Date, Message-ID, and relay servers used in sending the email.
<img width="1914" height="935" alt="Screenshot 2025-10-04 134427" src="https://github.com/user-attachments/assets/0f54fc26-ffee-420c-93a9-6fa44277a100" />

```

## OUTPUT:
Captured Web Activity and Email Header Information

## RESULT:
Web browser artifacts and email headers were successfully analyzed using Wireshark.

