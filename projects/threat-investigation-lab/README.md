# SSH Login Attempt Tracking Lab (Windows → Ubuntu VM)

## summary
I set up an Ubuntu VM in VMware and connected it to my Windows laptop on a “lab-only” network.  
Then I did a few **bad SSH login attempts** (wrong username/password) and one **successful SSH login**, and used **Wireshark + Ubuntu logs** to prove what happened.

---

## What I was trying to learn
- How to connect a VM and host on the same virtual network
- What **SSH traffic** looks like in Wireshark (port **22**)
- How to confirm “failed vs successful login” using **Ubuntu logs**
- How to write a simple investigation timeline based on evidence

---

## Lab setup 
**Host machine:** Windows laptop  
**VM:** Ubuntu on VMware Workstation Pro  
**Network type:** Host-only (VMnet1)

### IPs used
- **Windows (VMnet1 / host-only):** `192.168.145.1`
- **Ubuntu VM (host-only):** `192.168.145.128`
- **Service being tested:** SSH on **port 22**

> Why host-only?  
> It keeps the lab traffic between my laptop and VM only (safer).

---

## Tools I used
- VMware Workstation Pro
- Ubuntu (VM)
- Wireshark (Windows)
- Windows Command Prompt / PowerShell
- Ubuntu Terminal

