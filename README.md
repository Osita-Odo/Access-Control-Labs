# Identity and Access Management Labs

Two hands-on labs on controlling who can access a system and what they are allowed to do. The first builds access control on a simulated enterprise network in Cisco Packet Tracer (authentication, email and file services with per-user permissions). The second onboards a user to passwordless sign-in in Microsoft Entra ID using a Temporary Access Pass and a passkey. Together they cover access control across both on-premises network services and cloud identity.

## Projects

| Project | Objective | Tools applied | Lessons learnt |
|---|---|---|---|
| [AAA Access Control Lab](./AAA-Access-Control-Lab) (https://github.com/Osita-Odo/Access-Control-Labs/blob/main/IAM%20Labs.md).| Configure and verify centralised authentication and per-user authorisation across wireless, email and file services on a simulated enterprise network. | **Platform:** Cisco Packet Tracer (Logical and Physical Mode)<br>**Tools:** AAA-RADIUS server, wireless LAN controller and clients, mail server (SMTP/POP3), FTP server, Command Prompt, Text Editor | Authentication and authorisation are enforced per user: a permission set such as RWNL rather than RWDNL decides exactly what each account can do. |
| [Microsoft Entra-ID: Passkey Onboarding](https://github.com/Osita-Odo/Access-Control-Labs/blob/main/Microsoft%20Entra-ID.md) | Onboard a user to passwordless sign-in by issuing a one-time Temporary Access Pass and registering a passkey as the ongoing method. | **Platform:** Microsoft Entra ID<br>**Tools:** Entra admin centre, security info portal, Temporary Access Pass (TAP), passkey (FIDO2), Google Password Manager, Windows Hello PIN | A one-time Temporary Access Pass enables a secure first sign-in without a password, from which a passkey becomes the durable, phishing-resistant method. |
