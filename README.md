# IT Support Home Lab – Windows Server 2022 & Active Directory

This project is a small business style lab I built at home to practice real IT support tasks and gain hands-on Windows Server experience.

## Lab Overview

- **Hypervisor:** VMware Workstation 17
- **Domain:** `jzjus.local`
- **Server:** Windows Server 2022 (Domain Controller, DNS)
- **Client:** Windows 11 joined to the domain
- **Directory Services:** Active Directory Users & Computers, Group Policy Management

## What I Implemented

### 1. Active Directory Structure

- Created OUs for departments:
  - `HR`
  - `IT`
  - `Finance`
  - `Marketing`
  - `Sales`
  - `Admins`
- Created computer OUs:
  - `Workstations`
  - `Laptops`
  - `Sales-Computers`
  - `IT-Computers`
  - `TestMachines`
- Created 15+ user accounts and assigned them to the correct department OU.
- Joined a Windows 11 client (`CLIENTWIN11`) to the domain `jzjus.local`.

### 2. Group Policies

- **Password Policy**
  - Enforced a minimum password length of 10 characters for domain users.
  - Tested using a standard domain user to confirm the policy applies.

- **USB Storage Restriction**
  - Created a GPO to block USB mass storage devices on domain-joined machines.
  - Verified that plugging in a USB drive results in access being denied.

- **Mapped Network Drive for Marketing**
  - Created a shared folder: `\\WIN2022DC\MarketingShare`.
  - Created a security group: `SG_Marketing_Share`.
  - Assigned Marketing users to `SG_Marketing_Share`.
  - GPO `Marketing - Map M Drive` maps drive **M:** for Marketing users.

### 3. Help Desk Scenarios

- **Ticket 1 – Password Expired**
  - Configured a user account with “User must change password at next logon”.
  - Verified that the user is forced to change password when signing in.

- **Ticket 2 – Access to Shared Drive**
  - User could not see drive M.
  - Added the user to `SG_Marketing_Share`.
  - Confirmed that drive **M:** appears after `gpupdate /force` and re-login.

- **Ticket 3 – USB Not Working**
  - Simulated a user reporting USB not working.
  - Confirmed that the USB restriction GPO is the cause and working as designed.

## Screenshots

Key screenshots are in the [`Screenshots`](./Screenshots) folder:

- AD DS and DNS roles on the server.
- OU structure and user accounts.
- Client joined to `jzjus.local` domain.
- Password policy configuration and enforcement.
- USB restriction policy in action.
- Mapped Marketing shared drive (M:).

## Skills Practiced

- Windows Server 2022 installation and configuration.
- Active Directory (users, OUs, groups, computers).
- Group Policy creation, linking, and troubleshooting.
- DNS / domain join troubleshooting (IP, gateway, DNS, nslookup).
- Basic file sharing and NTFS/share permissions.
- Simulated level 1/2 help desk workflows (password resets, access issues, policy troubleshooting).
- Working with virtualized environments using VMware Workstation.
