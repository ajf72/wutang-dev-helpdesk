# Day 02 – Promoting DC01 to Domain Controller (PowerShell Deployment)

---

## 🎯 Objective

Promote DC01 to a Domain Controller by:

- Installing Active Directory Domain Services (AD DS)
- Creating a new forest
- Installing and configuring DNS
- Validating successful domain controller promotion

This deployment was performed using PowerShell instead of the GUI to build automation and infrastructure scripting skills.

---

## 🖥️ Environment

**Server Name:** DC01  
**Operating System:** Windows Server 2022 (Desktop Experience)  
**Static IP:** 10.0.0.10  
**Subnet:** 255.255.255.0 (/24)  
**Gateway:** 10.0.0.1  
**DNS:** 10.0.0.10 (self)  

---

## 🛠️ AD DS Deployment via PowerShell

### 1️⃣ Import AD DS Deployment Module

```powershell
Import-Module ADDSDeployment
```

---

### 2️⃣ Create New Forest & Promote Domain Controller

```powershell
Install-ADDSForest `
-CreateDnsDelegation:$false `
-DatabasePath "C:\Windows\NTDS" `
-DomainMode "WinThreshold" `
-DomainName "Helpdesk.Lab" `
-DomainNetbiosName "HELPDESK" `
-ForestMode "WinThreshold" `
-InstallDns:$true `
-LogPath "C:\Windows\NTDS" `
-NoRebootOnCompletion:$false `
-SysvolPath "C:\Windows\SYSVOL" `
-Force:$true
```

---

## 🌲 Domain Configuration

**Domain Name:** Helpdesk.Lab  
**NetBIOS Name:** HELPDESK  
**Forest Functional Level:** Windows Server 2016 (WinThreshold)  
**Domain Functional Level:** Windows Server 2016 (WinThreshold)  
**DNS Installed:** Yes  
**Global Catalog:** Enabled (default)  

---

## ⚠️ DNS Delegation Warning

Received warning:

> A delegation for this DNS server cannot be created...

This is expected in a new forest lab environment without a parent DNS zone. No action required for isolated lab setup.

---

## 🔄 Automatic Reboot

After installation completed successfully, the server automatically restarted to finalize:

- NTDS database creation
- SYSVOL folder creation
- DNS zone configuration
- Domain controller role activation

---

## 🧪 Post-Promotion Validation

### Confirm Domain Exists

Opened:

- Active Directory Users and Computers

Verified:
- Domain **Helpdesk.Lab** is present
- Default containers created (Users, Computers, etc.)

---

### Run Domain Controller Diagnostics

```powershell
dcdiag
```

Purpose:
- Validate DNS registration
- Confirm replication readiness
- Ensure core AD services running properly

---

### Verify Netlogon Service

```powershell
Get-Service netlogon
```

Expected Status:
```
Running
```

---

### Confirm SYSVOL Exists

Checked path:

```
C:\Windows\SYSVOL
```

SYSVOL folder confirms successful domain controller promotion and policy share readiness.

---

## 🧠 Key Concepts Practiced

- AD DS deployment via PowerShell
- Forest creation
- DNS integration with Active Directory
- Functional levels (Forest & Domain)
- NetBIOS naming standards
- Understanding DNS delegation warnings
- Infrastructure-first deployment mindset

---

## 📊 Outcome

DC01 is now:

- Forest Root Domain Controller
- Global Catalog Server
- DNS Server
- Authentication authority for Helpdesk.Lab

The lab environment now supports:

- User account creation
- Group Policy configuration
- Domain-joined clients
- NTFS permissions & file share lab
- Organizational Unit structure design

---

## 🚀 Next Steps (Day 03 Preview)

- Create Organizational Units (OUs)
- Create test user accounts
- Create security groups
- Join Windows client to domain
- Begin Helpdesk scenario simulations

---

## 📌 Lab Reflection

Using PowerShell instead of the GUI reinforced a deeper understanding of the AD DS deployment process and mirrors real-world infrastructure automation practices. This approach improves scripting confidence and prepares for scalable enterprise deployments.

Day 02 marks the transition from standalone server setup to full Active Directory infrastructure.
