# U-Boot RPi4 Lab

Customising **U-Boot** for Raspberry Pi 4, starting with a QEMU bring-up, automated smoke-tests, and boot-sequence tweaks.

[![CI – QEMU Smoke Test](https://github.com/jiwonj05/u-boot-rpi4-lab/actions/workflows/qemu.yml/badge.svg)](https://github.com/jiwonj05/u-boot-rpi4-lab/actions/workflows/qemu.yml)

---

## Project Summary

| Status | Feature |
| ------ | ------- |
| ✔ | Mainline U-Boot (2025.04) cross-compiled with `gcc-arm-none-eabi` |
| ✔ | Boots under QEMU `virt` board; UART logs captured (`log/bootlog*.txt`) |
| ✔ | `bootdelay` set to 0 for faster headless boot |
| ✔ | GitHub Actions workflow builds and boots U-Boot on every push (20 s timeout) |

---

## Quick Start (QEMU)

```bash
# Install host dependencies (Ubuntu)
sudo apt install gcc-arm-none-eabi qemu-system-arm make bison flex libssl-dev libgnutls28-dev

# Clone repo with submodule
git clone --recurse-submodules https://github.com/jiwonj05/u-boot-rpi4-lab.git
cd u-boot-rpi4-lab/u-boot

# Build for QEMU
make qemu_arm_defconfig
make -j$(nproc) CROSS_COMPILE=arm-none-eabi-

# Run U-Boot
qemu-system-arm -M virt -nographic -kernel u-boot
```
## Roadmap

| Milestone                | Description                                                               |
| ------------------------ | ------------------------------------------------------------------------- |
| GPIO LED in SPL          | Toggle a virtual LED in early boot to demonstrate SPL hooks               |
| I²C temperature read     | Probe a dummy sensor before DRAM initialisation (RPi4 target)             |
| FIT image signatures     | Sign kernel/DTB and verify in U-Boot                                      |
| CI improvements          | Cache the tool-chain and upload UART logs as artefacts                    |

---

## References

- **U-Boot documentation:** <https://u-boot.readthedocs.io/>
- **Mainline source:** <https://source.denx.de/u-boot/u-boot>
- **QEMU `virt` board:** <https://www.qemu.org/docs/master/system/arm/virt.html>
