# OptiPlex 7050 hackintosh
Clover for OptiPlex 7050 with Skylake CPU & GPU 

Test with OptiPlex 7050 (bought in late 2018) which using i7-6700, Intel HD Graphics 530, Intel I219LM2 Ethernet, macOS 10.15.7

Use DP for primary display，HDMI for secondary.

## UEFI Variables

In order to run macOS successfully a number of EFI BIOS variables need to be modified. The included Clover bootloader contains an updated `DVMT.efi`, which includes a `setup_var` command to help do just that.

`DVMT.efi` can be launched from Clover directly by renaming it to `Shell64U.efi` in the `tools` folder.

The following variables need to be updated:

| Variable              | Offset | Default value  | Desired value   | Comment                                                    |
|-----------------------|--------|----------------|-----------------|------------------------------------------------------------|
| CFG Lock              | 0xAF   | 0x01 (Enabled) | 0x00 (Disabled) | Disable CFG Lock to prevent MSR 0x02 errors on boot        |
| DVMT Pre-allocation   | 0x350  | 0x01 (32M)     | 0x04 (128M)     | Increase DVMT pre-allocated size to 128M for 2K+ displays  |

## Modify DVMT variable step

1. Start up and enter `Clover boot menu`, select `Start UEFI shell 64` and enter.
   
   I has replace `Shell64U.efi` with `DVMT.efi`, so you are running `DVMT.efi` in fact.
   
3. just run `setup_var 0x350 0x4` using this cmd line [中文教程](https://zhuanlan.zhihu.com/p/39798235)

4. fine, the graphics is ok to boot up macOS

5. Note: the UEFI Variables will lose after set BOIS to factory default!

### Working

- [x] APFS
- [x] CPU power management
- [x] GPU acceleration
- [x] Video encoder/decoder hardware
- [x] All USB ports at their max speed (manually mapped)
- [x] Gigabit Ethernet
- [x] Onboard Audio + Integrated Speaker at the front
- [x] All iCloud Services
- [x] App Store
- [x] Dell Sensors (Fans/Temperature)
- [x] Built in Displayport 1.4 and HDMI 1.2
- [x] TRIM working on Sabrent NVMe
- [x] TRIM enabled for SATA SSD with `sudo trimforce enable`
- [x] Time Machine
- [x] Seamless software updates

### FAQ
1. SIP disable default ?

   Yes. It way diabled by "config.plist/RtVariables/CsrActiveConfig=0x67". So you can install macOS system upgrade.
