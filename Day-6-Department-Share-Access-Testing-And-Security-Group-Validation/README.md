# Day 06 – Departmental Share Access Testing & Security Group Validation

## 🎯 Objective
Validate that NTFS permissions and Security Groups are correctly enforcing access control for departmental file shares.

This lab simulates real-world user access testing within an Active Directory environment.

---

## 🏗️ Environment Recap

### File Shares Created on DC01

| Share Name | Path |
|------------|------|
| Sales      | C:\Shares\Sales |
| Finance    | C:\Shares\Finance |
| Helpdesk   | C:\Shares\Helpdesk |

### Security Groups

- Sales_SG
- Finance_SG
- Helpdesk_SG

### User Assignments

| User | Department Group |
|------|------------------|
| Muhammad Ali | Sales_SG |
| Mike Tyson | Finance_SG |
| Floyd Mayweather | Helpdesk_SG |

---

## 🔐 Permission Model

For each departmental folder:

- Inheritance disabled
- Only the matching Security Group granted **Modify**
- Administrators retained **Full Control**
- SYSTEM retained **Full Control**

Example:

```
HELPDESK\Sales_SG → Modify
```

This ensures role-based access control (RBAC) is enforced.

---

## 🖥️ Testing Procedure (From CLIENT01)

Each user logged into the domain-joined client and attempted to access:

```
\\DC01
```

or

```
\\10.0.0.10
```

Then manually tested access to:

- Sales
- Finance
- Helpdesk

---

## 🧪 Test Results

### 🔹 Muhammad Ali (Sales_SG)

| Share | Result |
|--------|--------|
| Sales | ✅ Access Granted |
| Finance | ❌ Access Denied |
| Helpdesk | ❌ Access Denied |

---

### 🔹 Mike Tyson (Finance_SG)

| Share | Result |
|--------|--------|
| Finance | ✅ Access Granted |
| Sales | ❌ Access Denied |
| Helpdesk | ❌ Access Denied |

---

### 🔹 Floyd Mayweather (Helpdesk_SG)

| Share | Result |
|--------|--------|
| Helpdesk | ✅ Access Granted |
| Sales | ❌ Access Denied |
| Finance | ❌ Access Denied |

---

## 🔍 Validation Commands Used

From client:

```powershell
whoami
whoami /groups
```

Confirmed users were members of correct security groups.

---

## 🧠 Key Learning Points

- NTFS permissions override share permissions when more restrictive
- Security Groups simplify permission management
- Inheritance must be carefully managed
- Always test with actual user accounts (not Administrator)
- Role-based access control prevents lateral access between departments

---

## 🏢 Real-World Relevance

This simulates:

- Department separation in small-to-medium businesses
- File server permission structuring
- Helpdesk-level user access troubleshooting
- Access denied scenario validation

This is a core IT Support skill.

---

## ✅ Lab Status

Environment now includes:

- Domain Controller (DC01)
- AD Users & Groups
- Proper OU Structure
- NTFS Permission Enforcement
- Validated Departmental Access Control
- Domain-Joined Client Testing

---

## 🚀 Next Steps (Day 07)

- Implement Drive Mapping via Group Policy
- Apply mappings based on Security Groups
- Validate automatic drive provisioning at login

---

End of Day 06.
