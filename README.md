# Forcing Asus Router to Channel 165

## Issue Description
Asus routers sold in the EU region have firmware restrictions that disable 5 GHz channels 149–165. These channels are legal in many regions (including the US) but are blocked by default in EU-sold models.

This means even though your hardware supports it, you cannot select channel 149–165 (including 165) via the Web GUI.

## Methods to Bypass Limitation

### 1. Using AsusWRT-Merlin Firmware ✅
- Install Merlin (if available for your router model).
- Go to Wireless settings in the web UI.
- Set Region: United States (US).
- Choose Channel 165 from the dropdown.
- Save and reboot.

> Merlin supports JFFS scripts and offers more flexibility with region/channel settings.

### 2. Using JFFS Script on Stock Firmware ⚡
- Enable JFFS custom scripts:
  - Web UI → Administration → System → Enable JFFS custom scripts and configs → Yes.
- Reboot router.
- SSH into router and create script `/jffs/scripts/init-start`:

```sh
#!/bin/sh
nvram set wl1_country_code=US
nvram set wl1_chanspec=165/20
```

- Make it executable:
  - `chmod +x /jffs/scripts/init-start`
- Reboot router.
- Router will boot with US region and channel 165/20 MHz enabled.

#### ⚠️ Important Reminder:
DO NOT change channel settings via Web GUI or console after reboot — doing so will override your script and revert to the EU default country restrictions.

---

This repository provides instructions and scripts to help you enable channel 165 on Asus routers restricted by EU firmware.

---

## References
- [Original Gist by francoism90](https://gist.github.com/francoism90/3dede7973354d067c41bff5e54203fe9)
