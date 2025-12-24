🔐 Access Control Vulnerabilities – Theory & Practical Understanding
📌 Overview

Access control vulnerabilities occur when an application fails to properly enforce authorization checks, allowing users to access resources or functionality beyond their intended permissions.
These issues are among the most critical and commonly exploited vulnerabilities in real-world web applications.

<img width="1920" height="1080" alt="Screenshot at 2025-12-24 13-13-29" src="https://github.com/user-attachments/assets/40f8afb4-9343-4348-a491-289ea1ca240e" />
<img width="1920" height="1080" alt="Screenshot at 2025-12-24 13-11-41" src="https://github.com/user-attachments/assets/9f31b44e-cd6c-479b-a70c-2d4ff1311c08" />
<img width="1920" height="1080" alt="Screenshot at 2025-12-24 13-02-59" src="https://github.com/user-attachments/assets/7a2a4f05-91e0-4f75-bec0-fb58df25149c" />
<img width="1920" height="1080" alt="Screenshot at 2025-12-24 13-02-02" src="https://github.com/user-attachments/assets/903b315b-306d-49e2-a376-38450827e243" />
<img width="1920" height="1080" alt="Screenshot at 2025-12-24 13-01-35" src="https://github.com/user-attachments/assets/057a1992-fbaf-4d61-971e-5f0297215b15" />
<img width="1920" height="1080" alt="Screenshot at 2025-12-24 12-52-49" src="https://github.com/user-attachments/assets/79d9c9a0-685f-4cff-998e-4d17d9fe24e6" />
<img width="1920" height="1080" alt="Screenshot at 2025-12-24 12-52-24" src="https://github.com/user-attachments/assets/33d9ec64-ba61-433b-8e2e-07fa32ede9c9" />
<img width="1920" height="1080" alt="Screenshot at 2025-12-24 12-42-34" src="https://github.com/user-attachments/assets/7ec016de-b2ab-4c42-9fc9-f64f23467822" />
<img width="1920" height="1080" alt="Screenshot at 2025-12-24 12-42-10" src="https://github.com/user-attachments/assets/3ee85343-f0ef-47b0-b782-68fa7ec95732" />
<img width="1920" height="1080" alt="Screenshot at 2025-12-24 12-30-50" src="https://github.com/user-attachments/assets/d8d7189c-8d7e-458e-9c46-2498f06c932c" />
<img width="1920" height="1080" alt="Screenshot at 2025-12-24 12-30-31" src="https://github.com/user-attachments/assets/4204d056-82c5-4dc3-9046-54a9ea0736bd" />
<img width="1920" height="1080" alt="Screenshot at 2025-12-24 12-28-12" src="https://github.com/user-attachments/assets/9c7995ff-d95d-4d42-8226-f78b23704a2f" />
<img width="1920" height="1080" alt="Screenshot at 2025-12-24 12-18-12" src="https://github.com/user-attachments/assets/8bed877e-c225-41ca-8548-3785190e64c2" />
<img width="1920" height="1080" alt="Screenshot at 2025-12-24 12-05-30" src="https://github.com/user-attachments/assets/7f00b2ec-09bc-4a76-933d-df994bc4887d" />
<img width="1920" height="1080" alt="Screenshot at 2025-12-24 12-04-31" src="https://github.com/user-attachments/assets/a2567b13-9b52-4213-b39b-f467e1389495" />
<img width="1920" height="1080" alt="Screenshot at 2025-12-24 11-55-09" src="https://github.com/user-attachments/assets/ab24d520-0459-4790-a829-e6072821ab53" />
<img width="1920" height="1080" alt="Screenshot at 2025-12-24 11-55-03" src="https://github.com/user-attachments/assets/dffa375d-53c8-4859-9d88-9656c95edf28" />
<img width="1920" height="1080" alt="Screenshot at 2025-12-24 11-38-52" src="https://github.com/user-attachments/assets/9fa3beb8-c15b-419c-b9df-98729d199e17" />
<img width="1920" height="1080" alt="Screenshot at 2025-12-24 11-38-46" src="https://github.com/user-attachments/assets/4f2723a9-ba6f-4cda-96b5-110d9c36400d" />
<img width="1920" height="1080" alt="Screenshot at 2025-12-24 11-33-35" src="https://github.com/user-attachments/assets/3f98699d-3092-4f89-b55f-305a7a9c9603" />
<img width="1920" height="1080" alt="Screenshot at 2025-12-24 11-33-30" src="https://github.com/user-attachments/assets/65d48abb-8984-4ede-a648-d9be03891e1e" />


This section documents my theoretical understanding and hands-on practice of access control flaws using the PortSwigger Web Security Academy.

🔑 Key Access Control Concepts
🔹 Authentication vs Authorization

Authentication: Who you are (login)

Authorization: What you are allowed to do

Most real-world bugs happen when authentication is correct but authorization is missing or weak.

🧪 Vulnerability Categories Covered
1️⃣ Unprotected Admin Functionality

Concept:
Sensitive admin endpoints are accessible without proper authorization checks.

Real-World Scenario:

/admin

/manage

/dashboard

Security Impact:

Privilege escalation

Full administrative control

Root Cause:

Missing server-side authorization validation

2️⃣ Hidden / Unpredictable Admin URLs

Concept:
Developers assume that hiding admin URLs provides security.

Why This Fails:

URLs can be guessed, leaked, or discovered via recon

Security through obscurity is ineffective

Real-World Impact:

Unauthorized admin access

Configuration or data manipulation

3️⃣ Role-Based Access Control (RBAC) Failures
a) User role controlled by request parameter
b) User role modification via profile update

Concept:
Application trusts client-controlled values like:

"role": "user"


Attack Technique:

Modify role to admin

Replay request

Impact:

Privilege escalation

Unauthorized feature access

4️⃣ Insecure Direct Object References (IDOR)

Concept:
User-supplied identifiers (IDs) are not validated against the logged-in user.

Examples:

GET /account?id=123
GET /order/456


Attack:

Change ID to another user’s ID

Access sensitive data

Impact:

Data leakage

Privacy violations

Compliance risks (GDPR, etc.)

5️⃣ URL-Based Access Control Bypass

Concept:
Authorization enforced only at URL level, not at backend logic.

Common Bypass Techniques:

URL encoding

Case manipulation

Alternative paths

Impact:

Unauthorized access to restricted functionality

🧠 Real-World Testing Methodology

The following structured approach was used while testing access control vulnerabilities:

Authenticate as a low-privileged user

Intercept requests using Burp Suite

Identify identifiers (IDs, roles, endpoints)

Modify one parameter at a time

Replay requests using Burp Repeater

Observe unauthorized access or data exposure

Capture minimal proof-of-concept

Document impact and remediation

🛠 Tools Used

Burp Suite

Proxy

Repeater

Browser Developer Tools

Manual request manipulation (no blind automation)

🎯 Key Outcomes & Skills Gained

Ability to identify missing authorization checks

Practical understanding of IDOR vulnerabilities

Experience with privilege escalation testing

Strong grasp of business impact assessment

Improved secure design awareness

🏢 Real-World Relevance

Access control vulnerabilities are:

Frequently found in production systems

High severity in bug bounty programs

Commonly tested in VAPT engagements

Heavily weighted in pentesting interviews

This practice directly prepares for:

Web Application Pentester roles

VAPT Intern positions

Bug bounty entry-level testing

⚠️ Legal Disclaimer

All testing activities were conducted only on intentionally vulnerable labs provided by PortSwigger Web Security Academy.
No unauthorized systems were tested.
