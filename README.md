<img width="1917" height="1078" alt="image" src="https://github.com/user-attachments/assets/8dafbaa4-8db1-4b47-87da-b296af71eac9" /># Cybersecurity Lab Setup: Kali Linux on VirtualBox

An isolated virtual lab with a Kali Linux machine on a private VirtualBox NAT Network, built for ethical hacking and penetration testing practice.

<img width="1920" height="922" alt="Kali page" src="https://github.com/user-attachments/assets/7cd790d4-86a5-448a-9adb-977e443449f0" />


> Week 1 project, Cybersecurity at Networkwalks (Batch B084).
> Author: **ABDULKADIRI ADARANIJO** 
---

## Objectives

- [x] Install VirtualBox and 7-Zip
- [x] Create a private NAT Network
- [x] Import Kali Linux and attach it to the NAT Network
- [x] Set a static IP on Kali
- [x] Verify connectivity and DNS
- [x] Take a clean snapshot for recovery

---

## Lab Configuration

| Component | Configuration |
|---|---|
| Host OS | Windows 11 Pro |
| Host RAM | 16 GB |
| Hypervisor | VirtualBox Version 7.2.22 |
| Security OS | Kali Linux 2026.2 |
| Kali RAM | 2048 MB |
| Virtual Network | NatNetwork (DHCP enabled) |
| Network Address | 10.0.0.0/24 |
| Kali IP | 10.0.0.2/24 |
| Gateway | 10.0.0.1 |
| DNS | 8.8.8.8 |

---

## Setup Steps

### Step 1: Install 7-Zip and VirtualBox
Installed 7-Zip to extract the Kali image, and VirtualBox as the hypervisor.

### Step 2: Create the NAT Network
Created a NAT Network named `NatNetwork` with prefix `10.0.0.0/24` and DHCP enabled. A NAT Network lets multiple VMs talk to each other while still reaching the internet.

![NAT Network settings](02-nat-network.png)

### Step 3: Import Kali Linux
Downloaded the Kali VirtualBox image from the official site, extracted it with 7-Zip, and added it to VirtualBox.

<img width="1293" height="837" alt="image" src="https://github.com/user-attachments/assets/7eac85bc-de7d-4879-bbc8-fad7475ae3be" />


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b2d5f89d-da2b-4b02-bf04-e1773eed1810" />


### Step 4: Attach Kali to the NAT Network
Set Adapter 1 to **NAT Network** and selected `NatNetwork`.

![Kali network adapter](04-kali-adapter.png)

### Step 5: Set the static IP
Configured Kali with IP `10.0.0.2/24`, gateway `10.0.0.1`, DNS `8.8.8.8`.

<img width="1920" height="922" alt="Wired connection 1" src="https://github.com/user-attachments/assets/9b4c6384-f8b4-4c59-b42e-7e7fb1f7500f" />


### Step 6: Take a clean snapshot
Created a snapshot named `Clean Kali - Network Setup` as a recovery baseline.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/a536a7af-ed99-4fe6-aa89-d7261f3b081b" />


---

## Verification

| Test | Command | Result |
|---|---|---|
| IP address | `ip a` | 10.0.0.2/24 shown |
| Gateway | `ping 10.0.0.1` | Replies received |
| Internet | `ping 8.8.8.8` | Replies received |
| DNS | `networkwalks.com` | Replies received |


<img width="1920" height="922" alt="Ping test" src="https://github.com/user-attachments/assets/1c02b1ec-e9a4-414e-b1ed-486bc424e6bf" />

<img width="1920" height="922" alt="Ping Networkwalks" src="https://github.com/user-attachments/assets/677f1bb8-274e-47a5-8b4a-1e1961d9a508" />


---

## Problems and Solutions

**Problem 1: Network dropped after setting the static IP**
Fix: disabled duplicate address detection, then restarted the connection.
```
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
```

## Additional Tasks: Windows & Android Labs

I also set up Windows and Android virtual machines in VirtualBox, following similar setup procedures and carefully applying the relevant configuration steps.


<img width="1917" height="1078" alt="image" src="https://github.com/user-attachments/assets/e8d928b8-0bf0-4832-887d-9cf2676cdbbc" />


<img width="1917" height="1078" alt="Andriod VM" src="https://github.com/user-attachments/assets/c8fc4016-0a7d-4442-ae83-c746e22dddc5" />

---

## What I Learned

- Difference between NAT and NAT Network
- Configuring static IPs, gateways, and DNS in Kali
- Troubleshooting VM network issues
- Using snapshots for safe recovery
- Documenting technical work clearly

---

## Tools

[7-Zip](https://7-zip.org/download.html) | [VirtualBox](https://virtualbox.org/wiki/Downloads) | [Kali Linux](https://kali.org/get-kali)
