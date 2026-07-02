# ThinkPad E450 Hackintosh - OpenCore EFI

> OpenCore 1.0.7 | macOS Big Sur 11.7.11 | Lenovo ThinkPad E450 (Haswell)

## Hardware Specifications

| Component | Model | Status |
|-----------|-------|--------|
| **CPU** | Intel Core i5-4210U / i3-4005U / i7-4510U (Haswell-ULT) | ✅ |
| **iGPU** | Intel HD Graphics 4400 [8086:0a16] (spoofed as HD 4600 0x0412) | ✅ |
| **dGPU** | AMD Radeon R5 M240 [1002:6664] | ⛔ Disabled (SSDT-dGPU-Off) |
| **Audio** | Conexant CX20751/2 (AppleALC layout-id: 3) | ✅ |
| **HDMI Audio** | Intel Haswell HDMI | ✅ |
| **Ethernet** | Intel I218-V [8086:1559] | ✅ |
| **Wi-Fi** | Intel Wireless 7265 [8086:095a] | ✅ (AirportItlwm) |
| **Bluetooth** | Intel Bluetooth (7265 combo) | ✅ |

## BIOS Settings

| Setting | Value |
|---------|-------|
| Secure Boot | Disabled |
| CSM | Disabled |
| VT-d | Disabled |
| SATA Mode | AHCI |
| Boot Mode | UEFI |

## OpenCore Configuration

| Item | Value |
|------|-------|
| **OpenCore Version** | 1.0.7 (REL-107-2026-03-20) |
| **SMBIOS** | MacBookPro15,2 |

### SMBIOS Info

> ⚠️ **Important**: The serial numbers in this repo are placeholders. You **must** generate your own using [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) for a valid MacBookPro15,2 configuration.

### ACPI (10 SSDTs)

| SSDT | Function | Status |
|------|----------|--------|
| SSDT-ALS0.aml | Ambient Light Sensor | ✅ Enabled |
| SSDT-EC-USBX.aml | Fake EC + USB Power | ✅ Enabled |
| SSDT-EHCx.aml | EHC1/EHC2 rename (USB) | ✅ Enabled |
| SSDT-GPRW.aml | Instant wake fix | ✅ Enabled |
| SSDT-PL.aml | Plugin type (XCPM) | ✅ Enabled |
| SSDT-PNLF.aml | Backlight brightness | ✅ Enabled |
| SSDT-PTSWAK.aml | Sleep/Wake fix | ✅ Enabled |
| SSDT-SMBU.aml | SMBus support | ✅ Enabled |
| SSDT-UIAC.aml | USB port inject (install-time) | ✅ Enabled |
| SSDT-WNTF.aml | ACPI battery/WLAN fix | ✅ Enabled |

### Kexts (22)

| Kext | Version | Function |
|------|---------|----------|
| **Lilu.kext** | 1.6.0 | Kernel patcher (dependency) |
| **VirtualSMC.kext** | 1.2.9 | SMC emulation |
| **SMCProcessor.kext** | 1.2.9 | CPU sensor |
| **SMCSuperIO.kext** | 1.2.9 | Fan sensor |
| **SMCBatteryManager.kext** | 1.2.9 | Battery status |
| **SMCLightSensor.kext** | 1.2.9 | Ambient light sensor |
| **WhateverGreen.kext** | 1.5.8 | GPU patches |
| **AppleALC.kext** | 1.7.1 | Audio (CX20751/2, layout 3) |
| **IntelMausi.kext** | 1.0.7 | Intel I218-V ethernet |
| **AirportItlwm.kext** | 2.2.0 | Intel Wi-Fi (Big Sur) |
| **AirportItlwms.kext** | 2.2.0 | Intel Wi-Fi (Monterey) |
| **USBInjectAll.kext** | 0.7.7 | USB port injection |
| **ECEnabler.kext** | 1.0.2 | EC read fix for battery |
| **VoodooPS2Controller.kext** | 2.2.8 | Keyboard, TrackPoint, Touchpad |
| **BrightnessKeys.kext** | — | F5/F6 brightness keys |
| **CpuTscSync.kext** | 1.0.8 | TSC sync on wake |
| **RTCMemoryFixup.kext** | 1.0.8 | RTC memory range fix |
| **HibernationFixup.kext** | 1.4.5 | Hibernate support |
| **IntelBluetoothFirmware.kext** | 2.1.0 | Intel Bluetooth |
| **IntelBluetoothInjector.kext** | 2.1.0 | Bluetooth injector |
| **BlueToolFixup.kext** | 2.6.1 | Bluetooth firmware |
| **RealtekCardReader.kext** | 0.9.6 | SD card reader |
| **RealtekCardReaderFriend.kext** | 1.0.2 | SD card reader helper |

## EFI Structure

```
EFI/
├── BOOT/
│   └── BOOTx64.efi              # OpenCore bootloader
└── OC/
    ├── OpenCore.efi              # OpenCore core
    ├── config.plist              # Main configuration
    ├── ACPI/                     # SSDT patches (10 files)
    ├── Drivers/                  # UEFI drivers
    ├── Kexts/                    # Kernel extensions (22)
    ├── Resources/                # GUI resources (boot picker)
    └── Tools/                    # EFI tools
```

## Installation Notes

1. **Prepare USB**: Restore macOS Big Sur 11.7.11 image to external drive
2. **Copy EFI**: Mount EFI partition, replace with this EFI folder
3. **First Boot**: Select OpenCore → Reset NVRAM → Reboot
4. **Install**: Select macOS installer, proceed with installation
5. **Post-Install**: Generate unique SMBIOS, map USB ports with USBToolBox

## Known Issues

- After install, USB port mapping is recommended (replace USBInjectAll with custom SSDT)
- XhciPortLimit quirk disabled (broken on Big Sur 11.3+)
- AMD dGPU permanently disabled (not supported on macOS)

## Credits

- [Acidanthera](https://github.com/acidanthera) for OpenCore and kexts
- [Dortania](https://dortania.github.io) for OpenCore install guide

---

*Generated from a ThinkPad E450 running Ubuntu via lspci. Target macOS Big Sur 11.7.11.*
