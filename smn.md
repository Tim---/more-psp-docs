# SMN address space

The SMN (System Management Network) bus is one of the two main buses of the Zen platform. Is it probably another name for the SCF (Scalable Control Fabric).

Each die of a Ryzen processor contains several internal devices (CCXs, UMCs, Northbridges, GPP bridges, IOMMU...). We will call them "SMN nodes".

The SMN nodes are interconnected with the SMN bus. This allows the cores of the Ryzen processor (PSP, SMU, x86 cores...) to configure and monitor them.

Each node has a unique "node id", and can expose one or more static regions to the SMN bus, to expose its configuration registers.

SMN addresses inside a die are 32-bits, and all read/write operations are 4-bytes aligned.

However, the full SMN address space is 36-bits: the first 4 bits are used to select the target die.

## Access to the SMN space

The SMN can be accessed by cores using the "Common SoC" with the SMN bridge.

The SMN can be accessed by the x86 cores using the PCI host bridge.

## Memory layout

| begin        | end          | name                     |
| ------------ | ------------ | ------------------------ |
| `0x0001c000` | `0x0001dfff` | [D18Fx](devs/df.md)      |
| `0x00050000` | `0x00051fff` | [UMC0](devs/umc.md)      |
| `0x00059800` | `0x00059fff` | [SMUTHM](devs/smuthm.md) |
| `0x0005a000` | `0x0005cfff` | [SMUIO](devs/smuio.md)   |
| `0x0005d000` | `0x0005efff` | [fuses](devs/fuses.md)   |
| `0x00150000` | `0x00151fff` | [UMC1](devs/umc.md)      |
| `0x02d01000` | `0x02d02fff` | [FCH ACPI](devs/fch.md)  |
| `0x02dc4000` | `0x02dc407f` | [FCH SPI](devs/fch.md)   |
| `0x03a00000` | `0x03cfffff` | [SMU](smu/README.md)     |
| `0x03d00000` | `0x03ffffff` | [MP2](mp2/README.md)     |
