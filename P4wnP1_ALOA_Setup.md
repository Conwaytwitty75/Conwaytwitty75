# P4wnP1 A.L.O.A. Setup Guide for Raspberry Pi Zero W

**A Little Offensive Appliance** - A flexible, low-cost platform for pentesting, red teaming, and physical engagements.

## Main Repository

- **GitHub:** https://github.com/RoganDawes/P4wnP1_aloa
- **Original Developer:** mame82 (now RoganDawes)

## Pre-built Image Downloads

### Option 1: Official Kali Linux P4wnP1 A.L.O.A. Image

Download the official Kali image for Raspberry Pi Zero W with P4wnP1 A.L.O.A.:

https://www.kali.org/get-kali/#kali-arm

Look for: **Raspberry Pi Zero W (P4wnP1 A.L.O.A.)**

### Option 2: NightRang3r Custom Image (Kali 2023.1)

Pre-configured image with additional payloads:

https://github.com/NightRang3r/P4wnP1-A.L.O.A.-Payloads

## Installation Steps

### Requirements
- Raspberry Pi Zero W
- MicroSD card (8GB minimum, 16GB+ recommended)
- MicroUSB cable (data-capable, not charge-only)
- SD card reader
- Imaging software (Balena Etcher, Raspberry Pi Imager, or dd)

### Step 1: Download the Image
Download one of the images listed above.

### Step 2: Flash the Image
Using **Balena Etcher** (recommended):
1. Download Balena Etcher: https://www.balena.io/etcher/
2. Insert your MicroSD card
3. Select the downloaded image
4. Select your MicroSD card
5. Click "Flash!"

Using **Raspberry Pi Imager**:
1. Download: https://www.raspberrypi.com/software/
2. Choose OS > Use custom > Select downloaded image
3. Choose Storage > Select your MicroSD card
4. Click "Write"

### Step 3: Boot the Pi
1. Insert the MicroSD card into the Raspberry Pi Zero W
2. Connect the Pi to your computer via the **data** MicroUSB port (not PWR)
3. Wait 1-2 minutes for initial boot

### Step 4: Connect to P4wnP1

**SSH Access:**
- IP Address: `172.16.0.1` (USB Ethernet)
- Username: `root`
- Password: `toor`

```bash
ssh root@172.16.0.1
```

**Web Interface:**
- URL: http://172.16.0.1:8000

## Default Settings

| Feature | Details |
|---------|---------|
| USB Mode | Keyboard, Mouse, Ethernet (RNDIS/CDC ECM) |
| SSH Port | 22 |
| Web Port | 8000 |
| WiFi AP | P4wnP1 (configurable) |
| Default User | root |
| Default Pass | toor |

## Keyboard Layouts Available
br, de, es, fr, gb, it, ru, us

## Payload Repositories

Additional payloads and scripts:

| Repository | Link |
|------------|------|
| NightRang3r Payloads | https://github.com/NightRang3r/P4wnP1-A.L.O.A.-Payloads |
| chriskalv Payloads | https://github.com/chriskalv/p4wnp1_payloads |
| ALOA Menu Reworked | https://github.com/FuocomanSap/P4wnp1-ALOA-Menu-Reworked |
| HID Scripting Guide | https://github.com/Teerasak-Mairoddee/P4wnp1_HID_Scripting |

## Useful Commands

```bash
# Check P4wnP1 service status
systemctl status P4wnP1

# Restart P4wnP1 service
systemctl restart P4wnP1

# View logs
journalctl -u P4wnP1 -f
```

## Troubleshooting

1. **Pi not detected over USB:** Use the DATA port, not the PWR port
2. **Can't SSH:** Wait 2+ minutes for full boot, check IP 172.16.0.1
3. **Web interface not loading:** Ensure you're using http:// not https://

## Resources

- Main Repo: https://github.com/RoganDawes/P4wnP1_aloa
- Wiki/Docs: https://github.com/RoganDawes/P4wnP1_aloa/wiki
- Kali Docs: https://www.kali.org/docs/arm/raspberry-pi-zero-w-p4wnp1-aloa/
- Setup Guide: https://jamesachambers.com/kali-linux-p4wnp1-aloa-guide-setup-usage-examples/
