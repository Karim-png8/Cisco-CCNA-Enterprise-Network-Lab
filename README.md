# Cisco-CCNA-Enterprise-Network-Lab    
# Cisco CCNA Basic Device Configuration Lab

## 📌 Project Overview
This repository contains a laboratory exercise focused on the initial configuration and security hardening of a Cisco Router using Cisco CLI. The main objective is to establish basic device identification and restrict access to privileged modes.

## 🛠️ Tasks Performed
1. **Hostname Configuration:** Changed the default router name to a specific identifier (`r1`).
2. **Device Security:** Configured a secure enable password (`ccna`) to restrict access to the Privileged EXEC Mode.

---
<img width="923" height="140" alt="Network" src="https://github.com/user-attachments/assets/8db3d5e7-afe1-41aa-8ce5-49b88118ea8d" />
## 💻 CLI Configuration & Verification

Here is the step-by-step configuration executed on the device:

```topology
Router(config)# hostname r1
r1(config)# enable password ccna
r1(config)# exit


