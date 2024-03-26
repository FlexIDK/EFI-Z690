# MAG Z690M MORTAR WIFI + i7-13700K + DDR5 + RX 6700 XT

## Hardware

- **Motherboard**: MSI MAG Z690M MORTAR WIFI
- **CPU**: Intel Core i7-13700K
- **RAM**: 64GB DDR5 6000MHz (4 x 16GB)
- **GPU**: AMD Radeon RX 6700 XT
- **Storage**: Samsung EVO 970 256gb NVMe
- **OS**: macOS Monterey 12.7.4
- **OpenCore**: 0.9.9
- **WiFi**: Intel AX210 _(default on the motherboard)_
- **Bluetooth**: Intel AX210 _(default on the motherboard)_
- **Ethernet**: Realtek® 8125BG 2.5Gbps LAN controller _(default on the motherboard)_
- **Audio**: Realtek® ALC1200 Codec _(default on the motherboard)_

## Config

- iMacPro1,1 (if use another then performance will be lower)
- dGPU:
  - NootRX.kext for unsupported AMD GPU [RX6000 series](https://en.wikipedia.org/wiki/Radeon_RX_6000_series) 
    - Support GPU: Navi 21, on macOS Big Sur and newer / Navi 22, on macOS Monterey and newer (Yup) / Navi 23, on macOS Monterey and newer
    - Need add boot options: -wegnoigpu (for AMD dGPU) and disable iGPU in BIOS
    - Need disable WhateverGreen.kext
  - WhateverGreen.kext for [default AMD GPU](https://dortania.github.io/GPU-Buyers-Guide/modern-gpus/amd-gpu.html)
    - Need add boot options: agdpmod=pikera (for AMD dGPU)

Need add MLB, SystemSerialNumber and SystemUUID in PlatformInfo section.

## BIOS

- Boot > Fast Boot = off
- Boot > Boot Mode Select = UEFI
- Boot > Secure Boot = off
- Disable iGPU
- SATA Mode = AHCI
- Hyper Threading - Enabled
- All P-Cores and E-Cores - Enabled
- Above 4G decoding - on
- XHCI Hand-off - on

## Performance

**Geekbench 5:** 2933 / 18715 [Results](https://browser.geekbench.com/v6/cpu/5473034)

**Cinebench 2024**

![Multi-Core](https://github.com/FlexIDK/EFI-Z690/blob/master/_/cinebench_mc.jpg)

![RX 6700 XT](https://github.com/FlexIDK/EFI-Z690/blob/master/_/cinebench_rx6700.jpg)

## Kexts

- Audio:
  - [AppleALC.kext](EFI%2FOC%2FKexts%2FAppleALC.kext)
- Ethernet:
  - [LucyRTL8125Ethernet.kext](EFI%2FOC%2FKexts%2FLucyRTL8125Ethernet.kext)
- Intel AX210 Wifi:
  - [AirportItlwm.kext](EFI%2FOC%2FKexts%2FAirportItlwm.kext)
- Intel AX210 Bluetooth:
  - [IntelBTPatcher.kext](EFI%2FOC%2FKexts%2FIntelBTPatcher.kext)
  - [IntelBluetoothFirmware.kext](EFI%2FOC%2FKexts%2FIntelBluetoothFirmware.kext)
  - [IntelBluetoothInjector.kext](EFI%2FOC%2FKexts%2FIntelBluetoothInjector.kext) need add and enable if macOS Big Sur or lower
  - [BlueToolFixup.kext](EFI%2FOC%2FKexts%2FBlueToolFixup.kext)
- RX 6700 XT:
  - [NootRX.kext](EFI%2FOC%2FKexts%2FNootRX.kext)
- CPU:
  - [CpuTopologyRebuild.kext](EFI%2FOC%2FKexts%2FCpuTopologyRebuild.kext)
  - [CPUFriend.kext](EFI%2FOC%2FKexts%2FCPUFriend.kext)