# osTicket Help Desk Lab

## Overview
- Built a working IT help desk ticketing system from scratch
- Installed osTicket on an Ubuntu Server virtual machine
- Set it up like a real company help desk
- Created and resolved tickets through the full ticket lifecycle
- Connected it to my Active Directory lab to fix password and lockout tickets for real

## Tools Used
- **Virtualization:** VMware Workstation
- **Operating System:** Ubuntu Server 22.04 
- **Web Server:** Apache
- **Database:** MariaDB
- **Language:** PHP 8.2
- **Ticketing System:** osTicket
- **Remote Access:** SSH from Windows PowerShell
- **Directory Services:** Active Directory 

## Skills Shown
- Linux command line
- Installing a web stack (Apache, MariaDB, PHP)
- Database setup and security
- File permissions
- SSH remote management
- Ticket lifecycle management
- SLAs and ticket routing
- Escalation (Tier 1 → Tier 2)
- Role-based access control (RBAC)
- Active Directory password resets and account unlocks
- Troubleshooting and documentation


## Phase 1: Building the Server
- Made an Ubuntu Server virtual machine in VMware
- 2 GB RAM, 2 CPUs, 20 GB disk
- NAT networking
- Installed OpenSSH to manage the server remotely
- Updated the system with `apt update` and `apt upgrade`
- Found the server's IP address with `ip a`
- Connected from Windows PowerShell using SSH

<img width="594" height="582" alt="Hardware screen" src="https://github.com/user-attachments/assets/771bdfe6-4d23-41b1-aa7a-38359e8ca4c4" />

<img width="894" height="620" alt="Box checked" src="https://github.com/user-attachments/assets/701516a3-e766-483e-9dd0-3ba37e4a514d" />

<img width="893" height="614" alt="Logged in" src="https://github.com/user-attachments/assets/349539fe-e3a3-4215-86fa-b5aa34e811bf" />

<img width="881" height="651" alt="Connect through ssh" src="https://github.com/user-attachments/assets/19ac974e-b02a-4e49-a037-ccf095b9ad0b" />


## Phase 2: Installing the Web Stack
- Installed:
  - **Apache** to serve web pages
  - **MariaDB** to store tickets and settings
  - **PHP** to run osTicket
- Confirmed Apache was running and showing the default page
- Secured MariaDB with `mysql_secure_installation`:
  - Removed anonymous users
  - Disabled remote root login
  - Deleted the test database
  -
 

<img width="877" height="644" alt="Green active" src="https://github.com/user-attachments/assets/dd7eeb7c-872f-4561-a04f-07fded9076d8" />

<img width="787" height="673" alt="Apache default page" src="https://github.com/user-attachments/assets/581f2079-54e9-4302-a092-8854ae66a011" />

<img width="879" height="647" alt="PHP version" src="https://github.com/user-attachments/assets/8e7783ff-40f0-488c-b10c-28935171f710" />

- <img width="824" height="676" alt="Finished screen" src="https://github.com/user-attachments/assets/add25b08-6ff1-4e98-b29d-bf04dea0e43d" />

## Phase 3: Creating the Database
- Created a dedicated `osticket` database
- Created a database user with access to **only** that database
- Followed the **principle of least privilege**
- Tested the user's login to confirm access

<img width="850" height="579" alt="Screenshot 2026-10-28 025335" src="https://github.com/user-attachments/assets/f69c683c-e8ca-4c56-996e-86fe8de66a66" />

<img width="889" height="482" alt="In as osticketuser" src="https://github.com/user-attachments/assets/203d3663-ef9e-48a7-8b03-908800919c75" />

## Phase 4: Installing osTicket
- Downloaded osTicket from GitHub with `wget`
- Unzipped it and moved it into the web folder
- Set file ownership to the Apache user (`www-data`)
- Ran the osTicket web installer
- Hardened the install afterward:
  - Locked the config file permissions (`chmod 0644`)
  - Deleted the setup folder so no one could reinstall over it


<img width="859" height="583" alt="Screenshot 13" src="https://github.com/user-attachments/assets/f42dd28f-954e-4bdb-a0a8-50d4ca6667b4" />

<img width="858" height="173" alt="14" src="https://github.com/user-attachments/assets/3773714b-257d-4e09-a311-0502e307f4ca" />

<img width="893" height="675" alt="Fix after problem" src="https://github.com/user-attachments/assets/1c43471d-3361-4333-98ce-e394ce1e45f4" />

<img width="770" height="611" alt="15" src="https://github.com/user-attachments/assets/638fca53-93b1-4508-b195-1524c730bce1" />

<img width="881" height="616" alt="16" src="https://github.com/user-attachments/assets/2ddbb16f-40ab-4f77-b2c6-f311d3c3de97" />


## Phase 5: Configuring the Help Desk
- **Role permissions:**
  - Gave the All Access role full ticket permissions
  - Added Extended Access so the admin can see every department
- **Departments:**
  - IT Support
  - Accounts & Access
  - Hardware
- **SLA plans (deadlines):**
  - Urgent: 2 hours
  - Normal: 8 hours
  - Low: 24 hours
- **Help topics** that route tickets automatically:
  - Password Reset → Accounts & Access, High priority, Urgent SLA
  - Account Locked → Accounts & Access, High priority, Urgent SLA
  - Printer Issue → Hardware, Normal priority, Normal SLA
  - Software Install → IT Support, Low priority, Low SLA
  - New Hardware Request → Hardware, Low priority, Low SLA
- **Agents:**
  - Alex (Tier 1)
  - Sam (Tier 2)
- **Users:** 4 pretend employees

<img width="755" height="575" alt="23" src="https://github.com/user-attachments/assets/a8bb9852-0df8-47ae-89e5-3809d9d7f9c9" />

<img width="764" height="359" alt="24" src="https://github.com/user-attachments/assets/4b608160-e936-4d0d-93f9-9c55affa761e" />

<img width="752" height="345" alt="26" src="https://github.com/user-attachments/assets/896ca210-b45c-404a-9530-3de235862a9f" />

<img width="745" height="434" alt="27" src="https://github.com/user-attachments/assets/5d5f886a-f7c3-4f4a-b434-e48e93864da6" />

<img width="762" height="335" alt="28" src="https://github.com/user-attachments/assets/14f80e16-2238-4e9f-aab0-8e33d9edf663" />

<img width="752" height="364" alt="29" src="https://github.com/user-attachments/assets/ee4bbdba-01e7-415b-8a9e-7e662daa812d" />

<img width="715" height="523" alt="30" src="https://github.com/user-attachments/assets/0a4cc57e-6c5c-417d-b410-f656079ed61c" />

## Phase 6: Working Tickets
- Created 5 tickets:
  - 3 from the self-service customer portal
  - 2 as phone calls entered by an agent
- Worked each ticket through the full lifecycle:
  - **Open → Assign → Investigate (internal notes) → Reply → Resolve**
- Tickets handled:
  - Password reset (portal) → Tier 2
  - Printer offline (portal) → Tier 1
  - Zoom install (portal) → Tier 1
  - Account locked (phone) → Tier 2
  - New hire laptop (phone) → Tier 1, **escalated to Tier 2**
- Security practices followed:
  - Verified user identity before account changes
  - Never put passwords in tickets

<img width="713" height="394" alt="32" src="https://github.com/user-attachments/assets/95cc40a3-3a07-49cf-9428-145763862581" />

<img width="739" height="610" alt="33" src="https://github.com/user-attachments/assets/5c6fa967-9e8d-4cbc-8201-52810102804d" />

<img width="745" height="395" alt="34" src="https://github.com/user-attachments/assets/4c967592-0952-499b-91db-a71a1f059a5f" />

<img width="746" height="617" alt="35" src="https://github.com/user-attachments/assets/fa6b8e2a-68c0-42c2-8b2d-4799bd5e5155" />

<img width="731" height="550" alt="35 too" src="https://github.com/user-attachments/assets/5fb1e56b-8bb2-4d8c-aac7-ee9d3a5536e1" />

<img width="733" height="549" alt="36" src="https://github.com/user-attachments/assets/57877cef-3a36-4a99-b8f9-738874aeb484" />

### Fixing Tickets in Active Directory
- Reset a user's password with "User must change password at next logon"
- Set an account lockout policy with Group Policy (3 failed attempts)
- Locked an account on purpose, then unlocked it like a real tech

<img width="650" height="488" alt="37" src="https://github.com/user-attachments/assets/585cd469-9ec3-4f88-99e3-f909111e05b8" />

<img width="800" height="559" alt="38" src="https://github.com/user-attachments/assets/670a48ab-610a-4488-a6ba-c04021a79d11" />

<img width="524" height="483" alt="38 too" src="https://github.com/user-attachments/assets/ddc934fc-ea4f-466f-8418-f48a5b9f0d35" />

<img width="484" height="487" alt="38 as well" src="https://github.com/user-attachments/assets/c4fe5a3a-74e4-4fcc-b7ee-1b1af8ff04dc" />

<img width="754" height="368" alt="39" src="https://github.com/user-attachments/assets/a8135323-efef-4e0f-9c6e-841e9cc2e8ba" />



## Key Takeaways
- **The ticket lifecycle keeps a help desk organized.** Every ticket followed the same
  path: Open → Assign → Investigate → Reply → Resolve. Having a clear process made it easy
  to see what was done and what still needed attention.
- **SLAs and ticket routing save time.** Setting up help topics meant tickets automatically
  went to the right department with the right priority and deadline, so urgent problems
  like password resets and lockouts got handled first.
- **Documentation matters.** Writing internal notes on each ticket created a record of what
  I checked and what I fixed. If another tech picks up the ticket, they know exactly where
  things stand.
- **Escalation is part of the job.** Not every problem can be solved at Tier 1. Passing a
  ticket to Tier 2 with good notes keeps the user from repeating themselves.
- **Permissions control everything.** When tickets were hidden or I got "Access denied," the
  problem was role-based access control. I learned how roles and department access decide
  what each agent can see and do, which connects directly to identity and access management.
- **Security belongs in everyday tasks.** I verified user identity before account changes,
  never put passwords in tickets, locked down config file permissions, and gave the database
  user access to only one database (least privilege).
- **Troubleshooting is a step-by-step process.** I ran into a PHP version mismatch, a database
  login error, wrong folder paths, and permission problems. Each time, I read the error,
  checked one thing at a time, and fixed the cause instead of guessing.
- **Version requirements matter.** The latest osTicket needed a newer PHP than Ubuntu 22.04
  had. Checking software requirements before installing can prevent problems later.
- **Snapshots and clean reinstalls are a safety net.** When my setup got messy, I wiped the
  database and reinstalled cleanly, and I used VMware snapshots as save points. Knowing how
  to roll back made me more confident trying new things.
- **The command line is less scary with practice.** I got comfortable with commands like
  `cd`, `ls`, `mv`, `chmod`, `chown`, and `ssh`, and learned to always check my prompt to
  make sure I was on the right machine and in the right folder.

## Final Outcome
By the end of this project, I had a fully working IT help desk running on an Ubuntu Server
virtual machine that I built and configured from the command line. The system routes tickets
to the right department with set priorities and SLA deadlines, uses role-based access for
Tier 1 and Tier 2 agents, and supports tickets from both a self-service portal and phone calls.
I worked five realistic tickets through the full lifecycle, including an escalation, and
resolved the password reset and account lockout tickets for real in my Active Directory lab,
connecting my two projects together.This project gave me hands-on experience with the core parts of a help
desk role: managing tickets, communicating with users, following security best practices,
and solving problems methodically.
