# MAG Z690M MORTAR WIFI + i7-13700K + DDR5 + RX 6700 XT + Intel AX211

## Hardware

- **OpenCore**: 1.0.1
- **Motherboard**: MSI MAG Z690M MORTAR WIFI
- **CPU**: Intel Core i7-13700K
- **RAM**: 64GB DDR5 6000MHz (4 x 16GB)
- **GPU**: AMD Radeon RX 6700 XT
- **Storage**: Samsung EVO 970 256gb NVMe
- **OS**: macOS Ventura 13.6.7
- **WiFi**: Intel AX211 _(default on the motherboard)_
- **Bluetooth**: Intel AX211 _(default on the motherboard)_
- **Ethernet**: Realtek® 8125BG 2.5Gbps LAN controller _(default on the motherboard)_
- **Audio**: Realtek® ALC1200 Codec _(default on the motherboard)_

## Tested

- macOS Monterey 12.7.4 / 12.7.5
- update Monterey from 12.7.4 to 12.7.5
- update from Monterey to Ventura 13.6.7

## Working

- CPU 8 core + 24 threads
- GPU 6700 XT (HDMI/DP)
- RAM 6000MHz (4 sticks)
- Audio (from MB)
- Ethernet (from MB)
- WiFi (Intel AX211) (from MB)
- Bluetooth (Intel AX211) (from MB) + BT mac keyboard/mouse
- Sleep and wakeup
- All USB ports (from MB) - USB2.x/3.x

## Config

- iMacPro1,1 (if use another then performance will be lower)
- dGPU:
  - NootRX.kext for unsupported AMD GPU [RX6000 series](https://en.wikipedia.org/wiki/Radeon_RX_6000_series) 
    - Support GPU: Navi 21, on macOS Big Sur and newer / Navi 22, on macOS Monterey and newer (Yup) / Navi 23, on macOS Monterey and newer
    - Need add boot options: -wegnoigpu (for AMD dGPU) and disable iGPU in BIOS
    - Need disable WhateverGreen.kext
  - WhateverGreen.kext for [default AMD GPU](https://dortania.github.io/GPU-Buyers-Guide/modern-gpus/amd-gpu.html)
    - Need add boot options: agdpmod=pikera (for AMD dGPU)

_**Need add MLB, SystemSerialNumber and SystemUUID in PlatformInfo section.**_

## BIOS

- Boot > Fast Boot = off
- Boot > Boot Mode Select = UEFI
- Boot > Secure Boot = off
- Disable iGPU (can be left enable) (UHD 770 / Arc / Xe does not work in MacOS)
- SATA Mode = AHCI
- Hyper Threading = Enabled
- All P-Cores and E-Cores = Enabled
- Above 4G decoding = on
- XHCI Hand-off = on
- Resize BAR = on

## Performance

**Geekbench 5**: 2984 / 18965

![Multi-Core](https://github.com/FlexIDK/EFI-Z690/blob/master/_/gb_cpu.png)

![Multi-Core](https://github.com/FlexIDK/EFI-Z690/blob/master/_/gb_opencl.png)

![Multi-Core](https://github.com/FlexIDK/EFI-Z690/blob/master/_/gb_metal.png)

Results: [CPU](https://browser.geekbench.com/v6/cpu/6048962), 
[Metal](https://browser.geekbench.com/v6/compute/2166660), 
[OpenCL](https://browser.geekbench.com/v6/compute/2166666)

**Cinebench R23**: * / 30500

![Multi-Core](https://github.com/FlexIDK/EFI-Z690/blob/master/_/cb_r23_m.png)

**Cinebench 2024**

![Multi-Core](https://github.com/FlexIDK/EFI-Z690/blob/master/_/cinebench_mc.jpg)

![RX 6700 XT](https://github.com/FlexIDK/EFI-Z690/blob/master/_/cinebench_rx6700.jpg)

## Kexts

- Audio:
  - [AppleALC.kext](EFI%2FOC%2FKexts%2FAppleALC.kext)
- Ethernet:
  - [LucyRTL8125Ethernet.kext](EFI%2FOC%2FKexts%2FLucyRTL8125Ethernet.kext)
- Intel AX211 Wifi:
  - [AirportItlwm_Monterey.kext](EFI%2FOC%2FKexts%2FAirportItlwm_Monterey.kext) - only for Monterey (disabled)
  - [AirportItlwm_Ventura.kext](EFI%2FOC%2FKexts%2FAirportItlwm_Ventura.kext) - only for Ventura (enabled)
- Intel AX211 Bluetooth:
  - [IntelBTPatcher.kext](EFI%2FOC%2FKexts%2FIntelBTPatcher.kext)
  - [IntelBluetoothFirmware.kext](EFI%2FOC%2FKexts%2FIntelBluetoothFirmware.kext)
  - [BlueToolFixup.kext](EFI%2FOC%2FKexts%2FBlueToolFixup.kext)
- RX 6700 XT:
  - [NootRX.kext](EFI%2FOC%2FKexts%2FNootRX.kext) - for unsupported AMD rDNA 2 dGPU (enabled)
  - [SMCRadeonSensors.kext](EFI%2FOC%2FKexts%2FSMCRadeonSensors.kext) - VirtualSMC plug-in that provides temperature readings for AMD GPUs (6xxx series) (enabled)
- GPU/iGPU
  - [WhateverGreen.kext](EFI%2FOC%2FKexts%2FWhateverGreen.kext) - for other GPU/iGPU (disabled)
- CPU:
  - [CpuTopologyRebuild.kext](EFI%2FOC%2FKexts%2FCpuTopologyRebuild.kext)
- USB (deprecate) (disabled)
  - [USBToolBox.kext](EFI%2FOC%2FKexts%2FUSBToolBox.kext)
  - [UTBDefault.kext](EFI%2FOC%2FKexts%2FUTBDefault.kext)
  - [USBWakeFixup.kext](EFI%2FOC%2FKexts%2FUSBWakeFixup.kext)
- USB 2/3 (correct mapped port)
  - [USBMap.kext](EFI%2FOC%2FKexts%2FUSBMap.kext) **(enable)**
  - [USBMapDummy.kext](EFI%2FOC%2FKexts%2FUSBMapDummy.kext) - for debug (disabled)
  - [USBMapLegacy.kext](EFI%2FOC%2FKexts%2FUSBMapLegacy.kext) - legacy (disabled)
  - [USBMapLegacyDummy.kext](EFI%2FOC%2FKexts%2FUSBMapLegacyDummy.kext) - legacy for debug (disabled)