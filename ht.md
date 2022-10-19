# HT address space

The HT (Hypertransport) bus is one of the two main buses of the Zen platform. Is it probably another name for the SDF (Scalable Data Fabric).

The HT address space is basically the address space used by the x86 processor.

The PSP can use this address space to access the AMD chipset ("FCH") and probably anything outside the physical processor.

The HT address space is 48 bits longs.

## Access to the HT address space

The HT space can be accessed by cores using the "Common SoC" with the HT bridge, or HT alternative bridge.

The "system memory" region of the HT space is the address space of the x86 cores.

## Memory layout

| range                       | name          |
| --------------------------- | ------------- |
| `000000000000-fffcffffffff` | system memory |
| `fffdf7000000-fffdf70002ff` | test RAM      |
| `fffdfb000000-fffdfbffffff` | special RAM   |
| `fffdfc000000-fffdfc00ffff` | IO ports      |
| `fffdfe000000-fffdfe0fffff` | PCI MMCONFIG  |


### System memory

Range               | Name        |
------------------- | ----------- |
`04000000-0400ffff` | APOB region |
`09d80000-09ffffff` | BIOS bin    |
`fed80000-fed81fff` | ACPI MMIO   |

## Reference

[Hypertransport 3 specifications (archive)](https://web.archive.org/web/20160325155250/http://www.hypertransport.org/default.cfm?page=HyperTransportSpecifications31)
