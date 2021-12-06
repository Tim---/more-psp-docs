# SysHub address space

The SysHub address space is basically the address space used by the X86 processor.

The PSP can use this address space to access the AMD chipset ("FCH") and probably anything outside the physical processor.

The SysHub addresses are 48 bits longs. The first 16 bits indicate a subspace. Three subspaces are used: `0000`, `fffe` and `fffd`.

### Space `0000`:

Range               | Name        |
------------------- | ----------- |
`04000000-0400ffff` | APOB region |
`09d80000-09ffffff` | BIOS bin    |
`fed80000-fed81fff` | ACPI MMIO   |

### Space `fffe`:

Range               | Name         |
------------------- | ------------ |
`00000000-000fffff` | PCI MMCONFIG |

### Space `fffd`:

Range               | Name          |
------------------- | ------------- |
`f7000000-f70002ff` | write pattern |
`fb000000-fbffffff` | special RAM   |
`fc000000-fc00ffff` | IO ports      |
