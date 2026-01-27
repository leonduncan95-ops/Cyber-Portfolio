# SSH Login Attempt Tracking Lab (Windows → Ubuntu VM)

## Summary 
I set up an Ubuntu VM in VMware and connected it to my Windows laptop on a **lab-only network** (Host-only).

Then I did a few **intentional bad SSH login attempts** (wrong username/password) and one **successful SSH login**.  
After that, I used **Wireshark** (network traffic) + **Ubuntu logs** (what the server recorded) to confirm what happened.

This is where I checked activity:
- traffic happened on the network
- the server logs show whether the login worked or failed

---

## Lab setup
**Host machine:** Windows laptop  
**VM:** Ubuntu (VMware Workstation Pro)  
**Network type:** Host-only (VMnet1) *(keeps traffic between host + VM only)*  
**Service tested:** SSH (port 22)

### IPs used
- **Windows (VMnet1):** `192.168.145.1`
- **Ubuntu VM:** `192.168.145.128`

---

## What I was trying to learn
- How to connect a VM to my laptop on a private “lab” network
- How SSH logins show up in:
  - **Wireshark** 
  - **Ubuntu auth logs** (login success/fail on the server)
- How to build a basic investigation timeline using evidence

---

## Tools I used
- VMware Workstation Pro
- Ubuntu (VM)
- Wireshark (Windows)
- Windows Command Prompt / PowerShell
- Ubuntu Terminal

---

## What I did (simple steps)

### 1) Confirm the VM and laptop can talk

- On Ubuntu, I checked my IP:
  - `ip -br a`
- On Windows, I checked VMnet1 IP:
  - `ipconfig`

---

### 2) Generate “attack-like” activity
**Why:** In real life you might see password guessing or repeated failed logins.  
Here, I’m doing it **on purpose** so I can learn what it looks like.

I did:
- A few **failed SSH attempts** (wrong username/password)
- Then a **successful SSH login**

> Note: This is a simulation in my own lab.

---

### 3) Capture the traffic in Wireshark
**Why:** Wireshark proves the network connection + port being used.

In Wireshark I:
- Captured on the **VMware Network Adapter VMnet1**
- Filtered to SSH only:
  - `tcp.port == 22`

#### Evidence: SSH traffic (port 22)
![Wireshark SSH filter (tcp.port == 22)](tcp-port-22-filter.png)

---

### 4) Pull the login evidence from Ubuntu logs
**Why:** Wireshark shows traffic, but the **server logs** prove the result (failed vs accepted).

On Ubuntu, I checked SSH log entries:
```bash
sudo grep "sshd" /var/log/auth.log | egrep "Failed|Accepted|Invalid" | tail -n 50
