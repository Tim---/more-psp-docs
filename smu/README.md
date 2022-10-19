# SMU

According to BKDG:

> The system management unit (SMU) is a subcomponent of the northbridge that is responsible for a variety of
> system and power management tasks during boot and runtime. The SMU contains a microcontroller to assist
> with many of these tasks.

The SMU is running on an Xtensa processor. It uses the same "SoC" that the PSP.

## Boot process

1. The PSP bootloader loads the first part of the SMU firmware (PSP directory type 0x08) into the SMU SRAM.
It write at address SMN:`0x03c00000`-`0x03c3ffff` (mapped to SMU:`0x00000000`-`0x0003ffff`).
2. The bootloader wakes the SMU up by clearing a bit in the "SMU reset control" register.
3. The bootloader waits for the SMU to set the "Interrupt Ready" register to 1.
4. It can then use the mailbox to send messages to the SMU.
5. Once the ABL is executed, and the DRAM is configured, the PSP uses a region of the DRAM to store the whole SMU firmware (PSP directory type 0x08 + 0x12).
6. It informs the SMU using a mailbox message. On cache misses, the SMU loads the pages from the DRAM.

## SMU mappings on SMN

| begin        | end          | name                    |
| ------------ | ------------ | ----------------------- |
| `0x03a00000` | `0x03afffff` | SMU reset control       |
| `0x03b00000` | `0x03bfffff` | SMU sysregs             |
| `0x03c00000` | `0x03cfffff` | SMU SRAM                |

## Registers

### SMU reset control

After writing the firmware to the SMU SRAM, the PSP boots the SMU up by clearing a bit in the "wakeup" register:

* < Zen2:  SMN:`0x03a0008c` (clear bit 2)
* \>= Zen2: SMN:`0x03a000c4` (clear bit 1)

### SMU registers

The range SMN:`0x03b00000`-`0x03bfffff` is mapped to SMU:`0x03000000`-`0x030fffff`.

It is used by the PSP to access the "Interrupt Ready" register, and the mailboxes.

### SMU SRAM

The range SMN:`0x03c00000`-`0x03cfffff` is mapped to SMU:`0x00000000`-`0x000fffff`.

Only 0x40000 bytes of SRAM are available.

