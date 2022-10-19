# MP2

According to the Linux driver description:

> The MP2 is an ARM processor programmed as an I2C controller and communicating
> with the x86 host through PCI.

The MP2 is only present on mobile devices ?

It is an ARM Cortex-M processor (>= Cortex-M3).

## MP2 mappings on SMN

| begin        | end          | name                    |
| ------------ | ------------ | ----------------------- |
| `0x03d00000` | `0x03dfffff` | MP2 reset control       |
| `0x03e00000` | `0x03efffff` | MP2 public-sysregs?     |
| `0x03f00000` | `0x03ffffff` | MP2 SRAM                |

## MP2 memory map

| begin        | end          | name                    |
| ------------ | ------------ | ----------------------- |
| `0x00000000` | `0x0002ffff` | SRAM                    |
| `0x01000000` | `0x3fffffff` | Common SoC              | 
| `0xe0000000` | `0xe00fffff` | ARM Cortex PPB          |

