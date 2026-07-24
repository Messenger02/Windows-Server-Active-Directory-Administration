# Windows-Server-Active-Directory-Administration
# Network and Lab Architecture
  - Hypervisor: Oracle VirtualBox
  - Virtual Network: Internal Network
  - Domain Controller: 
    - OS: Windows Server 2025
    - HostName: DC01
    - Domain: Lab.local
    - Roles: AD DS. DNS Server
  Client Workstation:
  - OS: Windows 11 Pro
  - Hostname: WIN11-WORKSTATION
# Key Configurations and Implementation Details
  ## Active Directory OU and User Hierarchy
  I was able to create a structured Heirarchy inside Active directory Users and Computers using Organizational Units as departments:
  - Company OU
    - IT
    - Management
    - Sales
## Group Policy Objects and Security Policies
  - Password Complexity: Enabled (Password requires Uppercase, Lowercase, Symbols and Numbers)
  - Minumum Password Length: 7
  - Account Lockout Threshould: 4 invalid logon attempts
  - Account Lockout Duration: 15min
## File Share Permissions and Tiered Access Control (RBAC)
  - Configured a centralized shared folder on DC01 with departmental subfolders to demonstrate role-based access control:
      - NTFS Granular Permissions:
        - Department Manager are granted explicit full control over the department share, allowing full administrative management, permission modification, and file control.
        - Department Staffing are granted modify and write permissions, enabling dail document creation, editing, and deletion while restricting permission modification.
        - Non-Department users are resticted from accessing these files, enforcing the principle of least privilege.
# Testing and Verification
- Domain join Verification: Successfully joined WIN11-WORKSTATION to lab.local using domain credentails, verifying network communication and DNS resolution
- Access control (Access Denied testing):
  - Loggined into the Windows 11 VM as a Management user and successfully accessed \\DC01\Management.
  - attempted to access \\DC01\Sales folder as the same Management user and received a system prompt explaining that the current user does not have the permission to access this folder.
- Account lockout and administrative recovery
    - I purposely triggered an account lockout on Windows 11 VM.
    - A logon error occurred: "User is currently locked out"
    - On Windows Server VM, I verified the user lockout status on the user properties, and successfully unlocked the account
# Screenshots and proof of implementation
### Active Directory OU Structure
![Companyname/threeOUs](.//TheThreeOUs.png)
   ---
### Access Denied Verification
  ![BellonaUserAccessingManagementSharedFolder](.//SharedDocsManagementUser.png)
  ![CassiusUserDeniedAccesstoSalesSharedFolder](.//UserBlockedNoPermission.png)
  ---
### User Lockout and Administrative Unlock
![UserLockedout](.//UserLockout.png)
![unlockingUserAccount](.//CBellonaAccountUnlocked.png)
