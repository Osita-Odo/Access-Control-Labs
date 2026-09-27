**Access Control Lab: Detailed Screenshot Explanations**

# **Objectives**

This Cisco Packet Tracer lab configures and tests three access-control services across a two-site network (Headquarters and HQ), with all servers housed in the HQ Wiring Closet. It runs as a single story built around three ideas: authentication (proving who a user is), authorisation (what each user is allowed to do), and verification (confirming the controls actually hold).

Part 1 covers AAA (Authentication, Authorisation and Accounting) authentication. An AAA service is enabled on a RADIUS (Remote Authentication Dial-In User Service) server, and two accounts, user1 and user2, are added centrally. Both HQ laptops are then set to join the HQ-INT wireless network using WPA2 (Wi-Fi Protected Access 2\) with AES (Advanced Encryption Standard) encryption and these credentials, with addressing via DHCP (Dynamic Host Configuration Protocol). Because logins are checked against the RADIUS server, only approved accounts can connect. The proof of success is a laptop moving from a self-assigned 169.254 address to a proper 192.168.50.x lease.

Part 2 covers email services. SMTP (Simple Mail Transfer Protocol) and POP3 (Post Office Protocol version 3\) are activated on the Mail server under the domain mail.cyberhq.com, and mailbox accounts are created. Four devices (PC 1-1, PC 2-3, HQ-Laptop-1 and Net-Admin) are each given a working mail client, and a test message is sent from one user and received by another, confirming mail flows between authenticated mailboxes.

Part 3 covers FTP (File Transfer Protocol) services and privilege testing. The FTP server holds accounts with different permission sets. A file is downloaded with get, read, and a new file uploaded with put, showing read and write access. The decisive test comes when malia, whose permissions are RWNL (Read, Write, reName, List, but no Delete), is denied a delete but allowed a rename, exactly matching her configured rights.

Overall, the lab shows centralised authentication controlling network access, per-user authentication for email, and per-user authorisation being enforced on the FTP server, so authentication, authorisation and verification are each shown working in practice.

# **Tools Used**

* Cisco Packet Tracer, in both Logical and Physical Mode.

* AAA-RADIUS server and a wireless LAN (Local Area Network) controller (WLC) for centralised wireless authentication.

* Wireless client laptops and wired personal computers (PCs) as end devices.

* Mail server running SMTP and POP3, and the built-in Configure Mail client.

* FTP server and the end-device FTP command-line client (get, put, dir, delete, rename).

* Packet Tracer end-device tools: Command Prompt and Text Editor.

# **Lessons Learnt**

* Centralising authentication on a RADIUS server means credentials are checked in one place, so accounts can be managed without touching each device.

* A self-assigned 169.254.x.x address is a clear sign that authentication or DHCP (Dynamic Host Configuration Protocol) has not completed; a proper 192.168.x.x lease is the evidence that it succeeded.

* Authentication and authorisation are separate: identical logins can behave differently because a user's permission set (for example RWNL rather than RWDNL) removes a specific right such as delete.

* Testing a control by trying an action that should fail is stronger evidence than only showing the actions that succeed.

* The order in which evidence is captured matters, since a screenshot taken before DHCP completes can look like a failure even when the configuration is correct.

# **The lab network**

**Logical topology:** The starting logical view shows two sites, Headquarters (the tall building) and HQ (the smaller building), joined by a single link. This is the whole network at a glance, before any device is opened. Almost all of the lab work happens inside the HQ site.

<img width="938" height="561" alt="image" src="https://github.com/user-attachments/assets/faa94eff-6ed9-48fe-9d51-eeafc6f287ae" />

**Physical Mode floor plan:** Switching to Physical Mode reveals the real three-dimensional layout of the HQ office, with the Wiring Closet labelled. The servers used later (AAA-RADIUS, Mail, FTP) are all racked in this closet, so the report keeps returning here. The left Instructions panel lists the three objectives, and the completion meter reads 0%, marking the start of the lab.

<img width="938" height="527" alt="image" src="https://github.com/user-attachments/assets/f35c8cca-f6a2-4194-be41-fddcb7b20d67" />


# **Part 1: Configure and use AAA authentication credentials**

## **Step 1: Configure user accounts on the AAA server**

**AAA service, starting state:** The AAA-RADIUS server is open on the Services tab with AAA selected in the left menu. The RADIUS port is 1812\. The Network Configuration table already lists one client, WLC-1 at 192.168.99.250, server type Radius, with the shared key WLC-auth\! (this is the wireless controller that will forward login requests to the server). The User Setup table below holds one pre-existing account, 1stFLprn. The rack on the right confirms this is the AAA-RADIUS server in the Wiring Closet.

<img width="938" height="598" alt="image" src="https://github.com/user-attachments/assets/5b1e4747-4fc2-43f2-b656-0c5d6a668084" />


**AAA users added:** The same AAA screen after the two lab accounts have been added to User Setup: user1 with password PASSuser1\! and user2 with password PASSuser2\!. These are the credentials the laptops will use. From now on, any device joining the wireless network must present one of these usernames and passwords, which the server checks centrally.

<img width="938" height="688" alt="image" src="https://github.com/user-attachments/assets/9949ed21-d1ad-40cc-95ee-bba2a487bb18" />


## **Step 2: Configure wireless authentication on HQ-Laptop-1**

**HQ-Laptop-1 before configuration:** Hovering over HQ-Laptop-1 shows its status bubble. Wireless0 is up but every network field reads "not set": no IPv4 (Internet Protocol version 4\) address, no gateway, no DNS (Domain Name System). This is the blank state before the wireless interface is configured, and it confirms the laptop cannot yet reach anything.

<img width="938" height="431" alt="image" src="https://github.com/user-attachments/assets/534afc32-7345-471d-88cd-6160fd4dcdb8" />


**HQ-Laptop-1 wireless settings:** The laptop's Config tab, Wireless0 interface. Port Status is On at 11 Mbps, with a MAC (Media Access Control) address of 00D0.D374.E26E. The SSID (Service Set Identifier) is set to HQ-INT and Authentication is WPA2, with User ID user1 and password PASSuser1 (the AAA account from Step 1\) and Encryption Type AES. Internet Protocol (IP) Configuration is set to DHCP. Note the IPv4 address still shows 169.254.226.110 with mask 255.255.0.0, which is a self-assigned APIPA (Automatic Private IP Addressing) address: at this instant the RADIUS login and DHCP had not yet completed, so no real address had been leased.

<img width="936" height="938" alt="image" src="https://github.com/user-attachments/assets/041ecbc1-f5e0-4d01-a932-a2a647aa98bc" />


## **Step 3: Configure wireless authentication on HQ-Laptop-2**

**HQ-Laptop-2 before configuration:** HQ-Laptop-2's status bubble, again with Wireless0 up but all addressing "not set". The same blank starting point as the first laptop, ready to be configured with the second account.

<img width="938" height="513" alt="image" src="https://github.com/user-attachments/assets/1fa08588-ac83-4eaa-a5e5-fb1e38cc5b54" />


**HQ-Laptop-2 wireless settings:** HQ-Laptop-2's Wireless0 interface configured identically to Laptop-1 but with user2's credentials, SSID HQ-INT, WPA2 and AES, IP on DHCP. Repeating the exact steps with a different AAA account proves the server authenticates multiple users rather than a single hard-coded login.

<img width="905" height="938" alt="image" src="https://github.com/user-attachments/assets/a450eda7-c137-48c3-a9e4-62001c23341f" />


# **Part 2: Configure and use email services**

## **Step 1: Activate email services and configure user accounts**

**Locating the Mail server:** The Wiring Closet rack in Physical Mode with the Mail server picked out. This simply locates the correct device before its services are switched on.

<img width="938" height="517" alt="image" src="https://github.com/user-attachments/assets/d30f2173-978c-4179-8319-8fd31ef6c2e0" />

**Mail server EMAIL service:** The Mail server, Services tab, EMAIL. The SMTP and POP3 services are enabled and the domain is set to mail.cyberhq.com (shown in the domain field with the Set button beside it). The account list already contains HQuser1, HQuser2 and BRuser1, and a further account, BRuser2 with password Cisco123+, is being typed in ready to add with the plus (+) button. The \+, \-, and Change Password controls manage the mailbox accounts. This makes the server the SMTP/POP3 host every client will rely on.

<img width="938" height="644" alt="image" src="https://github.com/user-attachments/assets/4d02b587-41f4-44e3-bb43-e6c60405bbdd" />


## **Step 2: Configure the email clients**

For each device the report first confirms a working IP address in the status bubble, then fills in the Desktop \> Configure Mail screen. The pattern is identical each time: a display name, the user's email address, incoming and outgoing servers both set to mail.cyberhq.com, and the matching mailbox logon.

**PC 1-1 addressing:** PC 1-1's status bubble shows a proper wired address, 192.168.10.2/24, gateway 192.168.10.1, with a DNS server set. Unlike the laptops it is on a wired FastEthernet link, so it is ready for mail configuration straight away.

<img width="938" height="495" alt="image" src="https://github.com/user-attachments/assets/336511ca-37ad-48d1-ad28-7fc84d0f0566" />

**PC 1-1 mail client:** PC 1-1's Configure Mail screen for Suk-Yi, address HQuser1@mail.cyberhq.com, incoming and outgoing mail server mail.cyberhq.com, logon user HQuser1 with its password. This binds the mailbox created on the server to a client.

<img width="938" height="542" alt="image" src="https://github.com/user-attachments/assets/bf98e4bc-308e-476a-93bb-5e78f472e504" />

**PC 2-3 addressing:** PC 2-3's status bubble, address 192.168.30.3/24, confirming it too has a valid address before its client is set up.

<img width="938" height="427" alt="image" src="https://github.com/user-attachments/assets/47ccedb9-9717-458c-9171-89101583b4a3" />

**PC 2-3 mail client:** PC 2-3's Configure Mail screen for Ajulo, address BRuser1@mail.cyberhq.com, servers mail.cyberhq.com, logon BRuser1.

<img width="938" height="544" alt="image" src="https://github.com/user-attachments/assets/b6ec065e-ee5b-4c96-96f3-e2d72972f304" />

**HQ-Laptop-1 now addressed:** HQ-Laptop-1's status bubble, this time showing a real DHCP address, 192.168.50.3/24, gateway 192.168.50.1, a wireless data rate of 300 Mbps and signal strength 100%. This is the proof that the WPA2 \+ AAA login from Part 1 eventually succeeded: the laptop that earlier held a 169.254 self-assigned address now has a proper lease.

<img width="938" height="438" alt="image" src="https://github.com/user-attachments/assets/98fc3f12-da88-4ba7-8011-f78a0c1075b2" />

**HQ-Laptop-1 mail client:** HQ-Laptop-1's Configure Mail screen for Malia, address BRuser2@mail.cyberhq.com, servers mail.cyberhq.com, logon BRuser2.

<img width="938" height="545" alt="image" src="https://github.com/user-attachments/assets/6446c556-f7a7-4aa4-b82b-2be019f4ef5f" />

**Net-Admin addressing:** The Net-Admin PC in the Wiring Closet, address 192.168.99.9/24. Its status bubble locates it physically in the rack area and confirms its address before configuration.

<img width="938" height="666" alt="image" src="https://github.com/user-attachments/assets/2191607d-de5a-4817-bfb0-40f3f9f92675" />

**Net-Admin mail client:** Net-Admin's Configure Mail screen for Cisco, address HQuser2@mail.cyberhq.com, servers mail.cyberhq.com, logon HQuser2. This is the fourth and final mail client, and the machine used for the FTP work in Part 3\.

<img width="938" height="533" alt="image" src="https://github.com/user-attachments/assets/3f446fde-e920-4d05-a7eb-d0412dcec22c" />

## **Step 3: Send an email as Suk-Yi**

From PC 1-1, a message is composed to BRuser1 and then received on PC 2-3, proving mail flows end to end between two separate authenticated mailboxes. This step is performed on the mail clients already shown and is not graded by Packet Tracer, so the report includes no separate screenshot for it.

# **Part 3: Configure and use FTP services**

## **Step 3: Transfer files between Net-Admin and the FTP server**

**FTP accounts and permissions:** The FTP server, Services tab, FTP. The account table is the key detail: cisco (cisco), sukyi (cisco123) and ajulo (cisco321) each carry the permissions RWDNL, while malia (cisco123) carries RWNL. The letters stand for Read, Write, Delete, reName and List, so malia has every right except Delete. This single difference is what the privilege test in Step 4 will demonstrate. The lower panel lists the files on the server, including aMessage.txt at the top.

<img width="938" height="527" alt="image" src="https://github.com/user-attachments/assets/6fdb5e61-4dbf-4080-9cf8-853b962d5361" />

**Downloading a file with get:** Net-Admin's Command Prompt. The user connects with ftp 192.168.75.2, logs in as sukyi, and runs dir, which lists the server's files (aMessage.txt is item 0, size 57 bytes). The get aMessage.txt command then downloads it, and the terminal confirms "Transfer complete \- 57 bytes" before the session is quit. This shows the account's read access working.

<img width="938" height="528" alt="image" src="https://github.com/user-attachments/assets/d0cf08cc-c091-4c88-a038-c21a34931817" />

**Opening the file in Text Editor:** After downloading, the report closes the prompt and opens the Text Editor's File \> Open dialog, which offers the downloaded aMessage.txt (and a sample file). Selecting it opens the file.

<img width="938" height="527" alt="image" src="https://github.com/user-attachments/assets/1e8cdaa5-4217-453b-867d-3574312ae934" />

**The recovered message:** The Text Editor showing the contents of aMessage.txt: a short greeting confirming the FTP server was accessed successfully. This is the payload that the whole transfer was about.

<img width="938" height="527" alt="image" src="https://github.com/user-attachments/assets/cae28e62-dff1-4747-bdda-f1ccddd40058" />

**Uploading a new file with put:** A command prompt reconnecting to 192.168.75.2 and using put to upload a newly created file, aMessage\_new.txt. The terminal reports "Transfer complete" and 34 bytes copied, confirming the account also has write access, not just read.

<img width="938" height="177" alt="image" src="https://github.com/user-attachments/assets/88161edb-c011-4c83-91a6-2fe8ac2f2d38" />

## **Step 4: Verify FTP user privileges are working as configured**

**Delete denied, rename allowed:** The final test, logged in this time as malia (the RWNL account). The delete aMessage\_new.txt command is refused: the server returns "550 Requested action not taken. permission denied". The very next command, rename aMessage\_new.txt aMessage\_rename.txt, succeeds with "OK Renamed file successfully". Because malia's permission set includes reName but not Delete, the server enforces exactly that. This is the clearest demonstration in the lab that authorisation is being applied per user, not just authentication.

<img width="938" height="306" alt="image" src="https://github.com/user-attachments/assets/ce774eb9-46fc-4156-9939-8f12cf4d53cb" />

# **Summary**

Read together, the screenshots trace one access-control story. AAA/RADIUS decides who may join the wireless network; the change from a 169.254 self-assigned address to a proper 192.168.50.x lease is the visible sign that authentication worked. The email service adds per-user mailbox authentication for four clients. The FTP section then shows authorisation being enforced: identical logins behave differently because malia lacks delete rights. Authentication, authorisation and verification are each shown in action.
