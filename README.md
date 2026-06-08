# Cisco-CCNA-Enterprise-Network-Lab    
# Cisco IOS Router Basic Configuration Lab

This repository documents the step-by-step process of configuring a Cisco router with basic settings, security configurations, and saving the running configuration.

## Lab Topology & Overview
The configuration was performed on a Cisco Router (R1) to establish hostname identification, enable password security, and ensure configurations persist after a reboot.

---

## Configuration Steps

### Step 1: Change Hostname
Modify the default router name to a specific identifier (`r1`).
```cisco
Router> enable
Router# configure terminal
Router(config)# hostname r1
