# Cisco-CCNA-Enterprise-Network-Lab    
# Cisco IOS Router Basic Configuration Lab

This repository documents the step-by-step process of configuring a Cisco router with basic settings, security configurations, and saving the running configuration.

## Lab Topology & Overview
The configuration was performed on a Cisco Router (R1) to establish hostname identification, enable password security, and ensure configurations persist after a reboot.

<img width="923" height="140" alt="Network" src="https://github.com/user-attachments/assets/e8901bfb-3023-467e-8e07-e15b6dfb4c8c" />
14  ```cisco
15  Router> enable
16  Router# configure terminal
17  Router(config)# hostname r1
18  r1(config)# enable password ccna
19  r1(config)# exit
20  ```
21  
22  ### Step 2: Enable Password Encryption
23  
24  
```cisco
25  r1# configure terminal
26  r1(config)# service password-encryption
27  ```
