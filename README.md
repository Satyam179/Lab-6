# Lab 6 – HTTP Request/Response Interception and Manipulation (Exp 7)

**Target:** DVWA (local intentionally vulnerable application), `http://localhost:4280`  
**Tools:** Windows PowerShell, Docker Desktop, MariaDB, Burp Suite Community Edition v2026.10.1, Burp's integrated Chromium browser  
**Date of exercises:** 17 November 2026

## Aim

Conduct dynamic web application analysis by intercepting and comparing HTTP requests and responses through Burp Suite, changing a hidden form field, a session cookie, and an HTTP header.

## Observed work

1. **Hidden form field:** On `POST /vulnerabilities/upload/`, changed multipart `MAX_FILE_SIZE` from `100000` to `1`. The original `test.png` upload succeeded; the modified request returned `200 OK` with the page message **"Your image was not uploaded."**
2. **Session cookie:** On `GET /security.php`, changed a valid `PHPSESSID` to `invalidsession123` while keeping `security=low`. DVWA returned `302 Found` with `Location: login.php`.
3. **Request header:** On `GET /security.php`, changed `User-Agent` to `Lab6-Security-Test` with a valid session cookie. DVWA returned `200 OK` with the authenticated Security page.

See [Experiment_Results.md](Experiment_Results.md) for procedure, request/response observations, and limitations.

## Uploaded evidence

The following files have been uploaded to this GitHub repository:
- `Lab6_Burp_Suite_Report.pdf` (seven-page PDF report)
- `01_Docker_DVWA_Startup.png`
- `02_DVWA_Security_Low.png`
- `03_Burp_HTTP_History.png`
- `04_Original_Image_Upload.png`
- `05_Original_Hidden_Field.png`
- `06_Modified_Hidden_Field.png`
- `07_Modified_Upload_Response.png`
- `08_Session_Baseline.png`
- `09_Invalid_Session_Redirect.png`
- `10_Modified_User_Agent.png`

Screenshots prepared for publication have session identifiers redacted.

## Additional Firefox proxy, CA and HTTPS verification (18 Nov 2026)

After the original DVWA tests, Firefox was configured with a **manual HTTP and HTTPS proxy** at `127.0.0.1:8080`. Firefox successfully opened `http://burpsuite`, and the imported **PortSwigger CA** appeared under **Firefox Certificate Manager > Authorities**.

Burp Proxy Intercept captured Firefox's HTTPS requests. In HTTP History, `GET https://example.com/` appeared with **TLS checked** and **HTTP 200 OK**. No external-site vulnerability test or request manipulation was performed.

**Additional evidence prepared but not yet uploaded to GitHub:**

- `Lab6_Final_Updated_Report.pdf` - revised ten-page report, to replace the earlier seven-page PDF for submission
- `11_Firefox_Proxy_Configuration.png`
- `12_Burp_Welcome_Proxy_Verification.png`
- `13_PortSwigger_CA_in_Firefox.png`
- `14_HTTPS_Intercept_Queue.png`
- `15_HTTPS_History_ExampleDotCom.png`

The lab portal submission is a separate step. After the demo, restore Firefox's normal proxy settings and remove the lab CA trust.

This lab did not require original application source code; DVWA is a third-party learning application. The report and notes document student-observed experiments rather than claiming ownership of DVWA source.
