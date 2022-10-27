# Boot sequence

## On-chip bootloader

The PSP on-chip bootloader is a piece of immutable code executed when the PSP boots.

When the machine boots (cold or warm start), the PSP starts executing the on-chip bootloader.

It locates and parse the Embedded Firmware Structure and the PSP directory table in the flash.

It loads and verifies the off-chip bootloader and starts executing it.

## Off-chip bootloader

The off-chip bootloader has several functions:
  * initialize some devices
  * execute the ABL code (mainly used to initialize DRAM and PCI)
  * load the SMU firmware
  * load the BIOS and boot the x86 cores
  * at the end, start executing the fTPM.

## References

  * [coreboot docs on family 17h](https://doc.coreboot.org/soc/amd/family17h.html)
  * [coreboot docs on the PSP](https://doc.coreboot.org/soc/amd/psp_integration.html)
