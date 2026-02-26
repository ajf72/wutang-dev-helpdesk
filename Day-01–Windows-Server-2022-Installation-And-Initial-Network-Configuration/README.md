# Day 01 – Windows Server 2022 Installation & Initial Network Configuration

---

## 🎯 Objective

Set up the foundation of the Helpdesk Lab environment by:

- Installing Windows Server 2022
- Renaming the server
- Assigning a static IP address
- Preparing the system for future Active Directory deployment

---

## 🖥️ Environment Details

**Hypervisor:** Hyper-V  
**VM Name:** DC01-Helpdesk-Lab  
**Operating System:** Windows Server 2022 (Desktop Experience)  
**Network Type:** Private Virtual Switch (Helpdesk_Lab_Private)  

---

## 🏗️ Server Configuration

### 1️⃣ Server Installation

- Installed Windows Server 2022 (Desktop Experience)
- Completed initial setup
- Logged in as local Administrator
- Verified Server Manager loads successfully

---

### 2️⃣ Server Rename

Default computer name was replaced with:

```
DC01
```

This naming convention follows infrastructure best practices:

- DC = Domain Controller (future role)
- 01 = First server in environment

Reboot completed successfully after rename.

---

### 3️⃣ Static IP Configuration

Configured static IPv4 settings:

```
IP Address:      10.0.0.10
Subnet Mask:     255.255.255.0 (/24)
Default Gateway: 10.0.0.1
DNS Server:      10.0.0.10
```

### Why These Settings?

- `10.0.0.0/24` selected as lab subnet.
- `.10` reserved for infrastructure server.
- DNS set to itself in preparation for future Active Directory Domain Services installation.
- DHCP disabled (static configuration required for servers).

---

## 🧪 Verification

Executed:

```
ipconfig /all
```

Confirmed:

- Static IPv4 address applied
- DHCP disabled
- Correct subnet mask
- DNS pointing to server IP
- Hostname reflects DC01

---

## 🧠 Key Concepts Practiced

- Windows Server installation process
- Server renaming best practices
- Static IP configuration
- Subnetting fundamentals (/24 network)
- Basic infrastructure planning mindset
- Preparing server for Domain Controller role

---

## 🚀 Next Steps (Day 02 Preview)

- Install Active Directory Domain Services (AD DS)
- Promote DC01 to Domain Controller
- Create new forest
- Configure DNS role
- Begin domain-based lab environment

---

## 📌 Lab Reflection

Day 01 focused on building a proper infrastructure foundation rather than rushing into Active Directory. Establishing correct naming conventions and static IP configuration ensures the environment is structured, scalable, and aligned with enterprise best practices.

This marks the beginning of the Helpdesk Lab build.

