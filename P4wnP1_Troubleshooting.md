# P4wnP1 A.L.O.A. Troubleshooting Guide

Work through these steps in order to diagnose connection issues.

---

## Step 1: Verify Hardware Setup

### Check the USB Port
The Pi Zero W has **two** micro USB ports:

```
[  PWR  ] [  DATA  ]  [HDMI]  [SD]
    ↑          ↑
  Power    Use this one!
  Only     (for USB data)
```

**Action:** Make sure you're using the **DATA** port (the one closer to the center/HDMI).

### Check the Cable
Many micro USB cables are **charge-only** (no data wires).

**Test:** Try a different cable, preferably one you've used for data transfer before.

---

## Step 2: Verify the Image is Flashed Correctly

### Check LED Activity
When powered on, the Pi Zero W should:
1. Green LED blinks during boot (10-30 seconds)
2. Green LED activity indicates SD card reads

**No LED activity?**
- Re-flash the SD card
- Try a different SD card
- Verify the image downloaded completely (check file size)

---

## Step 3: Check if Device is Detected

### Linux
```bash
# Check for new network interface
ip addr

# Look for usb0 or eth1 with 172.16.0.x
# Or check dmesg for USB device
dmesg | tail -20

# Check for USB ethernet device
lsusb
```

### macOS
```bash
# List network interfaces
ifconfig

# Look for interface with 172.16.0.x address
# Usually appears as "RNDIS" or similar in System Preferences > Network
```

### Windows
1. Open **Device Manager** (Win+X > Device Manager)
2. Look under **Network adapters** for:
   - "USB Ethernet/RNDIS Gadget"
   - "Remote NDIS Compatible Device"
   - Any unknown device with yellow warning
3. Open **Control Panel > Network and Sharing Center > Change adapter settings**
4. Look for new Ethernet adapter

---

## Step 4: Fix Driver Issues (Windows)

If you see an unknown device or RNDIS with a yellow warning:

### Method 1: Update Driver
1. Right-click the unknown device > **Update driver**
2. **Browse my computer for drivers**
3. **Let me pick from a list**
4. Select **Network adapters**
5. Manufacturer: **Microsoft**
6. Model: **Remote NDIS Compatible Device**
7. Click Next and confirm

### Method 2: Manual Driver Install
1. Download RNDIS driver if needed
2. Extract and point Device Manager to the folder

---

## Step 5: Check IP Address Assignment

### Linux
```bash
# Check if you got an IP from P4wnP1
ip addr show usb0

# If no IP, try requesting one
sudo dhclient usb0

# Or set manually
sudo ip addr add 172.16.0.2/24 dev usb0
sudo ip link set usb0 up
```

### macOS
```bash
# Check interface
ifconfig

# Set IP manually if needed (find interface name first)
sudo ifconfig en6 172.16.0.2 netmask 255.255.255.0 up
```

### Windows (PowerShell as Admin)
```powershell
# Check adapters
Get-NetAdapter

# Check IP
Get-NetIPAddress

# Set manual IP if needed (replace "Ethernet 2" with actual adapter name)
New-NetIPAddress -InterfaceAlias "Ethernet 2" -IPAddress 172.16.0.2 -PrefixLength 24
```

---

## Step 6: Test Connectivity

### Ping Test
```bash
ping 172.16.0.1
```

**Expected:** Replies from 172.16.0.1

**No response?**
- Device not booted yet (wait 2 min)
- Wrong USB port
- Driver/IP issue
- Firewall blocking

### Check if SSH Port is Open
```bash
# Linux/macOS
nc -zv 172.16.0.1 22

# Or with nmap
nmap -p 22 172.16.0.1
```

---

## Step 7: SSH Connection

```bash
ssh root@172.16.0.1
```

**Password:** `toor`

### SSH Troubleshooting

**"Connection refused"**
- P4wnP1 service may not be running
- Try the web interface: http://172.16.0.1:8000

**"Connection timed out"**
- IP/Network issue (go back to Step 5)

**"Host key verification failed"**
```bash
# Remove old key and retry
ssh-keygen -R 172.16.0.1
ssh root@172.16.0.1
```

**"Permission denied"**
- Password is `toor` (lowercase)
- Try username `kali` with password `kali` on newer images

---

## Step 8: Alternative Access Methods

### WiFi Access Point
P4wnP1 creates a WiFi hotspot by default:
- SSID: `P4wnP1` (or similar)
- Password: Check web interface or default is often `MaMe82-P4wnP1`

Connect to WiFi and SSH to `172.24.0.1`

### Web Interface
Open in browser: http://172.16.0.1:8000

---

## Step 9: Serial Console (Last Resort)

If USB networking doesn't work, use serial console:

### Requirements
- USB-to-TTL serial adapter (3.3V!)
- Connect: GND→GND, TX→RX, RX→TX on Pi GPIO

### Linux
```bash
sudo screen /dev/ttyUSB0 115200
```

### macOS
```bash
screen /dev/tty.usbserial-* 115200
```

---

## Quick Diagnostic Commands (run on YOUR computer)

### Linux One-Liner
```bash
echo "=== USB Devices ===" && lsusb && echo -e "\n=== Network Interfaces ===" && ip addr && echo -e "\n=== Ping Test ===" && ping -c 3 172.16.0.1
```

### macOS One-Liner
```bash
echo "=== USB Devices ===" && system_profiler SPUSBDataType && echo -e "\n=== Network ===" && ifconfig && echo -e "\n=== Ping ===" && ping -c 3 172.16.0.1
```

---

## Common Issues Summary

| Symptom | Likely Cause | Solution |
|---------|--------------|----------|
| No LED on Pi | Bad power/cable/SD | Check cable, reflash SD |
| Device not in Device Manager | Wrong USB port | Use DATA port |
| Unknown device (Windows) | Missing driver | Install RNDIS driver |
| No IP address | DHCP not working | Set IP manually |
| Ping fails | Network config | Check IP, firewall |
| SSH refused | Service down | Try web UI, reboot Pi |
| Wrong password | Image variant | Try root/toor or kali/kali |

---

## Still Stuck?

1. Try a complete reflash with latest image
2. Test with different computer
3. Check forums: https://forums.hak5.org/forum/92-usb-rubber-ducky/
4. GitHub issues: https://github.com/RoganDawes/P4wnP1_aloa/issues
