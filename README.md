## Active Directory Access Control Using Group Policy

## Overview

This project demonstrates how to enforce access control in a Windows Server environment by restricting Remote Desktop (RDP) access for specific users using Active Directory and Group Policy Objects (GPOs).

The objective was to prevent users in the Sales group from accessing the domain controller while maintaining administrative access for authorized users.

## Environment Setup
Platform: Microsoft Azure
Domain Controller: Windows Server VM (dc)
Client Machine: Windows Server VM (vm)
Domain: corp.awesome.com
Tools Used:
Active Directory Domain Services (AD DS)
Group Policy Management Console (GPMC)
PowerShell ISE

## Implementation
1. Network Configuration

Configured the domain controller with a static private IP address to ensure consistent communication within the virtual network.

<img src="YOUR_IMAGE_1" width="700"/>
2. Active Directory Deployment

Installed and configured Active Directory Domain Services using PowerShell, creating a new forest:

corp.awesome.com
<img src="YOUR_IMAGE_2" width="700"/> <img src="YOUR_IMAGE_3" width="700"/>
3. User and Group Management

Automated the creation of:

A Domain Admin account (awesomeadmin)
A Sales security group
A Sales user (awesomesales) assigned to the group
<img src="YOUR_IMAGE_4" width="700"/>
4. Group Policy Configuration

Created and applied a Group Policy Object (GPO) to:

Deny log on through Remote Desktop Services

Applied specifically to the Sales group.

<img src="YOUR_IMAGE_5" width="700"/>

5. Access Validation
🚫 Restricted User Test

Attempted RDP login using a Sales user:

corp\awesomesales

Result: ❌ Access Denied

<img src="YOUR_IMAGE_6" width="700"/> <img src="YOUR_IMAGE_7" width="700"/>
✅ Admin Access Test

Logged in using Domain Admin credentials:

corp\awesomeadmin

Result: ✔️ Successful Login

<img src="YOUR_IMAGE_8" width="700"/> <img src="YOUR_IMAGE_9" width="700"/>

## Results
- Successfully blocked RDP access for all users in the Sales group.
- Maintained unrestricted access for administrative accounts.
- Verified enforcement through real login attempts.

## Key Learnings
🔹 Group Policy as a Security Layer

This project reinforced how powerful GPOs are for enforcing centralized security policies across a domain environment.

🔹 Importance of Role-Based Access Control (RBAC)

Instead of managing permissions per user, assigning policies to groups simplifies administration and scales efficiently.

🔹 Automation with PowerShell

Using scripts to create users and configure AD significantly reduces manual errors and improves consistency.

🔹 Testing is Critical

Validating both failure (denied access) and success (admin access) scenarios ensures policies are correctly applied.

## Improvements & Next Steps
🔸 Implement OU-Based Policies

Instead of applying GPOs at the domain level, organizing users into Organizational Units (OUs) would allow more granular control.

🔸 Add Logging & Monitoring

Integrate:

Event Viewer auditing. 
Azure Monitor / Log Analytics. 
To track login attempts and detect unauthorized access attempts. 
🔸 Harden Security Further 
Restrict access using Network Security Groups (NSGs). 
Enable Multi-Factor Authentication (MFA). 
Limit RDP exposure using Just-in-Time (JIT) VM access. 
🔸 Use Least Privilege Principle

Refine permissions so users only have access strictly necessary for their role.

## Project Resources
PowerShell scripts for AD setup and user configuration
Azure VM environment
Group Policy configuration

## Summary

This project highlights how combining Active Directory, Group Policy, and Azure infrastructure enables strong access control mechanisms in enterprise environments. It demonstrates a practical implementation of security best practices such as least privilege and centralized policy enforcement.
