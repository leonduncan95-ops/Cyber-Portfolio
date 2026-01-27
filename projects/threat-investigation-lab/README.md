# SSH Login Attempt Tracking Lab (Windows → Ubuntu VM)

## summary
I set up an Ubuntu VM in VMware and connected it to my Windows laptop on a **host-only** “lab network” (VMnet1).  
Then I did a few **bad SSH login attempts** (wrong username/password) and one **successful login**.  
After that, I used **Wireshark + Ubuntu logs** to prove what happened.

---

## Lab setup
- **Host:** Windows laptop  
- **VM:** Ubuntu (VMware Workstation Pro)  
- **Network:** Host-only (VMnet1)  
- **Service tested:** SSH (port 22)

**IPs used**
- Windows (VMnet1): `192.168.145.1`
- Ubuntu VM: `192.168.145.128`

---

## What I did
1. Confirmed the VM and laptop could talk on the host-only network
2. Tried SSH logins on purpose:
   - a few **failed** attempts
   - then a **successful** attempt
3. Captured traffic in Wireshark and checked Ubuntu logs to confirm the results

---

## Evidence (screenshots)

### 1) Wireshark capture
**Filter used:** `tcp.port == 22`  
This screenshot shows SSH traffic between my Windows host and Ubuntu VM. Even though SSH is encrypted, I can still see the connection and that it’s using port 22.

![Wireshark SSH filter (tcp.port == 22)](tcp-port-22-filter.png)

---

### 2) Wireshark conversations / stats
This view is a quick summary of “who talked to who” during the capture. It confirms the two IPs involved and that the traffic was going to **port 22**.

![Wireshark Conversations/Stats for SSH traffic](statistics.png)

---

### 3) Ubuntu log proof (failed + successful)
This screenshot is from Ubuntu’s auth log and shows:
- **Failed password / invalid user** lines (bad attempts)
- **Accepted password** line (successful login)

This is the “server-side proof” of what happened.

![Ubuntu auth.log showing failed and accepted logins](login-attempts.png)

---

## What I learned
- Host-only networking is great for labs because it keeps traffic **between my laptop and VM**
- Wireshark helps confirm the **network activity**
- Ubuntu logs confirm the **login result** (failed vs successful)
