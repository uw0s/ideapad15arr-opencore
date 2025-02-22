<p align="center">
 <h2 align="center">macOS Ventura on Lenovo Ideapad 330-15ARR - Ryzen 2500U</h2>
 <p align="center">Lenovo Ideapad 330-15ARR OpenCore EFI and config.</p>
</p>
<p align="center"><img src="https://img.shields.io/badge/BIOS-7VCN49WW-blue?logo=lenovo&amp;logoColor=%23fff" alt="" />&nbsp;<img src="https://img.shields.io/badge/OpenCore-1.0.3-black" alt="" />&nbsp;<img src="https://img.shields.io/badge/macOS-Ventura%2013.7.4-green?logo=apple&amp;logoColor=%23fff" alt="" /></p>

## Table of Contents

*   [Specifications](#specifications)
*   [Features](#features)
*   [BIOS Options](#bios-options)
*   [Other Modifications](#other-modifications)
*   [Boot Arguments](#boot-arguments)
*   [Kexts](#kexts-used)
*   [SSDTs](#ssdts-used)
*   [Tools Used](#tools-used)
*   [About Sonoma](#about-sonoma)

## Specifications

| Item  | Info |
| --- | --- |
| Model | Ideapad 330-15ARR |
| BIOS Version | [7VCN49WW](https://pcsupport.lenovo.com/us/en/products/laptops-and-netbooks/300-series/330-15arr/downloads/driver-list/component?name=BIOS%2FUEFI&id=5AC6A815-321D-440E-8833-B07A93E0428C) |
| CPU | AMD Ryzen 5 2500U |
| iGPU | AMD Radeon RX Vega 8 |
| RAM | 1x 4GB + 1x 16GB  DDR4 2400 MHz |
| WiFi & BT | Realtek RTL8821CE |
| Ethernet | Realtek RTL8111 |
| Audio | Realtek ALC236 |
| OpenCore Version | 1.0.3 |
| SMBIOS | MacBookPro16,3 |

## Features
| Item | Status | Notes |
| --- | --- | --- |
| CPU | ✅ | [AMD Vanilla Kernel Patches](https://github.com/AMD-OSX/AMD_Vanilla?tab=readme-ov-file#read-me-first) |
| iGPU | ✅ | NootedRed.kext |
| Brightness Control | ✅ |   |
| HDMI A/V out | ✅ ℹ | HDMI Audio is not working ([related issue](https://github.com/ChefKissInc/NootedRed/issues/225)) |
| USB | ✅ | All ports working with GUX-RyzenXHCIFix.kext + USBMap |
| Keyboard | ✅ | VoodooPS2.kext |
| Internal Speakers & Mic | ✅ | AppleALC.kext working with [layout-id](https://dortania.github.io/OpenCore-Post-Install/universal/audio.html) 13 |
| Trackpad | ✅ | VoodooI2CHID.kext (no gestures) |
| Ethernet | ✅ | RealtekRTL8111.kext |
| WiFi & BT | ❌ | Unsupported card |
| Battery | ✅ | ECEnabler.kext + SMCBatteryManager.kext |
| AppleTV+ DRM | ❌ | [Related issue](https://github.com/ChefKissInc/NootedRed/issues/28) |
| iServices | ❓ |   |
| Shutdown/Reboot | ✅ |   |
| Sleep/Wake | ✅ |   |
| Virtualization | ❌ | Might never work |

## Bios Options

*   Secure Boot: **Disabled**

## Boot Arguments

`npci=0x3000` 

This boot argument is used due to the absence of [**Above 4G Decoding**](https://dortania.github.io/OpenCore-Install-Guide/AMD/zen.html#enable) in the BIOS options.

## Kexts Used

| Kext | Description |
| --- | --- |
| [AppleALC.kext](https://github.com/acidanthera/AppleALC) | Native macOS HD audio for not officially supported codecs |
| [AppleMCEReporterDisabler.kext](https://github.com/acidanthera/bugtracker/files/3703498/AppleMCEReporterDisabler.kext.zip) | Disables AppleIntelMCEReporter which causes panics on AMD CPUs |
| [ForgedInvariant.kext](https://github.com/ChefKissInc/ForgedInvariant) | A kext for syncing the TSC on AMD & Intel |
| [GenericUSBXHCI.kext](https://github.com/RattletraPM/GUX-RyzenXHCIFix) | A fork of GenericUSBXHCI aimed at analyzing and fixing the USB3 |
| [HoRNDIS.kext](https://github.com/TomHeaven/HoRNDIS) | A USB tethering driver for macOS (since WiFi isn't working) |
| [Lilu.kext](https://github.com/acidanthera/Lilu) | Platform for arbitrary kext, library, and program patching throughout the system |
| [NootedRed.kext](https://github.com/ChefKissInc/NootedRed) | A Lilu plugin for AMD Vega iGPU support |
| [RealtekRTL8111.kext](https://github.com/Mieze/RTL8111_driver_for_OS_X) | Open source driver for the Realtek RTL8111/8168 Ethernet family |
| [RestrictEvents.kext](https://github.com/acidanthera/RestrictEvents) | Blocking unwanted processes causing compatibility issues on different hardware and unlocking the support for certain features restricted to other hardware |
| [Ryzen-CtlnaAHCIPort.kext]() | A kext to properly detect the internal SATA drive |
| [SMCBatteryManager.kext](https://github.com/acidanthera/VirtualSMC) | Enables battery readings |
| [USBToolBox.kext](https://github.com/corpnewt/USBMap) | A USB Mapping kext and tool,  UTBMap.kext must be generated |
| [UTBMap.kext](https://github.com/USBToolBox/tool) | Generated with USBToolBox |
| [VirtualSMC.kext](https://github.com/acidanthera/VirtualSMC) | Advanced Apple SMC emulator in the kernel |
| [VoodooI2C.kext & VoodooI2CHID.kext](https://github.com/VoodooI2C/VoodooI2C) | Fixes trackpad |
| [VoodooPS2Controller.kext](https://github.com/acidanthera/VoodooPS2) | Fixes keyboard |

## SSDTs Used

Generated with SSDTTime in Windows 10. More information [here](https://chefkissinc.github.io/guides/hackintosh/gathering-files/acpi/).

| SSDT | SSDTTime Option |
| --- | --- |
| SSDT-EC | FakeEC Laptop |
| SSDT-HPET | HPET |
| SSDT-PLUG | PluginType |
| SSDT-PNLF | PNLF |
| SSDT-USBX | USBX |
| SSDT-XOSI | XOSI |

## Tools Used

| Tool | Description |
| --- | --- |
| [acidanthera/OpenCorePkg](https://github.com/acidanthera/OpenCorePkg/releases) | Core, useful utilities included |
| [corpnewt/ProperTree](https://github.com/corpnewt/ProperTree) | Used for modifying config.plist |
| [corpnewt/SSDTTime](https://github.com/corpnewt/SSDTTime) | Used for creating SSDTs |
| [corpnewt/GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) | Used to generate SMBIOS |
| [corpnewt/MountEFI](https://github.com/corpnewt/MountEFI) | Used to mount the EFI partition |
| [corpnewt/CPU-Name](https://github.com/corpnewt/CPU-Name) | Used to change the displayed CPU name |
| [DavidS95/Smokeless_UMAF](https://github.com/DavidS95/Smokeless_UMAF) | Used to increase the iGPU VRAM to 2GB |
| [NyaomiDEV/AMDFriend](https://github.com/NyaomiDEV/AMDFriend) | Patches libraries to work on AMD |
| [USBToolBox/tool](https://github.com/USBToolBox/tool) | Used to generate USBToolBox.kext |

## About Sonoma
It's possible to install macOS Sonoma but hardware acceleration is currently broken (constant crashes). Here's the steps for installing macOS Sonoma:

1. Disable **NootedRed.kext** and set **SecureBootModel** to **Disabled** in **config.plist**
2. Proceed with installation
3. After installation is completed, set **SecureBootModel** back to **Default** in **config.plist**
4. Go through the account creation process
5. Enable **NootedRed.kext** in **config.plist**

At the moment, interacting with GUI elements will crash the system. The cause is probably NootedRed.kext,  future updates might fix this behavior ([related issue](https://github.com/ChefKissInc/NootedRed/issues/235)).

## Credits

*   People in the AMD-OSX Discord server (really helpful).
*   [corpnewt](https://github.com/corpnewt) for all the useful tools.
*   [Dortania](https://dortania.github.io/OpenCore-Install-Guide/) for the guides.
*   [Acidanthera](https://github.com/acidanthera) for OpenCore and most kexts.