# 🧠 Real-World Networking: MacBook DHCP Issue

## 🔍 Problem
MacBook was stuck with a self-assigned IP (`169.254.x.x`) even though connected to home Wi-Fi. No internet access. Other devices worked fine.

---

## 🧪 Tools Used
- macOS Terminal
- Router admin panel (TP-Link VX220-G2v)
- CLI commands for ping, interface cycling, and routing

---

## 🛠️ Steps Taken

### 1. Local Diagnostics (macOS)
- Flushed DNS:
  ```bash
  sudo dscacheutil -flushcache
  sudo killall -HUP mDNSResponder
### Reset routing table:
```bash
sudo route -n flush
```
### Restarted Wi-fi interface
```bash
sudo ifconfig en0 down && sudo ifconfig en0 up
```

## 2. Manual IP Configuration (as fallback)

IP: 192.168.1.99

Subnet Mask: 255.255.255.0

Gateway: 192.168.1.1

DNS: 1.1.1.1, 8.8.8.8

## 3. Router-Side Checks

Checked DHCP lease table

Matched my Mac’s MAC address

Set a DHCP reservation

Verified no MAC filtering or access control

Rebooted router

## ✅ Final Fix
Router reboot resolved the issue — likely due to stuck DHCP lease table or service crash.

## 💡 Key Takeaways
Diagnosing DHCP and APIPA issues

Using CLI tools for networking

Home router DHCP reservation setup

Staying calm and solving instead of rebooting blindly
