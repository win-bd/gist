## ✅ 1. **Check Windows Firewall Rules**

### 🛡️ Allow SSH (Port 22) and ICMP (Ping) Through Firewall

#### 👉 Enable SSH in Firewall:

Run this in **PowerShell as Admin**:

```powershell
New-NetFirewallRule -Name sshd -DisplayName "OpenSSH Server" -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22
```

#### 👉 Enable Ping (ICMP Echo):

```powershell
New-NetFirewallRule -Name ICMPAllow -DisplayName "Allow ICMPv4-In" -Protocol ICMPv4 -IcmpType 8 -Direction Inbound -Action Allow
```

---

## ✅ 2. **Confirm SSH Service is Running and Listening**

### Check service:

```powershell
Get-Service sshd
```

### Check it's listening on port 22:

```powershell
netstat -an | findstr :22
```

You should see something like:

```
TCP    0.0.0.0:22      0.0.0.0:0     LISTENING
```

---

## ✅ 3. **Check Network Profile (Set to Private)**

If the network is set to **Public**, Windows firewall blocks incoming connections by default.

### Change to Private:

* Go to **Settings > Network & Internet > Ethernet or Wi-Fi**
* Click your network
* Set **Network profile** to **Private**

---

## ✅ 4. **Check IP and Reachability from Remote Machine**

On the remote machine:

```bash
ping 192.168.1.100
ssh username@192.168.1.100
```

If still no luck, run:

```bash
telnet 192.168.1.100 22
```

If connection fails, it confirms port 22 is blocked or unreachable.

