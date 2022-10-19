# Common SoC

The Zen CPUs contain several small CPU cores in addition to the x86 cores: the PSP, SMU, MP2...

Although these cores use different architecture, they all seem to have the same devices available on their "system bus".

We will name "SoC" the collection of devices that are directly accessible using the system address space.

## Devices

* [HT bridge](ht-bridge.md)
* [alt HT bridge](alt-ht-bridge.md)
* [SMN bridge](smn-bridge.md)
* [CCP](ccp.md)
* [sysregs](sysregs.md)
* [programmable DMA](prog-dma.md)

## Memory layout

| start        | end          | name                 | used by |
| ------------ | ------------ | -------------------- | ------- |
| `0x00000000` | variable     | SRAM                 | all     |
| `0x01000000` | `0x02ffffff` | SMN bridge mappings  | all     |
| `0x03000000` | `0x0300ffff` | CCP registers        | psp     |
| `0x03010000` | `0x0301ffff` | sysregs (public)     | all     |
| `0x03030000` | `0x0303ffff` | ???                  | psp     |
| `0x03050000` | `0x0305ffff` | I2C buses ?          | mp2     |
| `0x03200000` | `0x0320ffff` | sysregs (private)    | all     |
| `0x03210000` | `0x0321ffff` | ???                  | smu,mp2 |
| `0x03220000` | `0x0322ffff` | SMN bridge registers | all     |
| `0x03230000` | `0x0323ffff` | HT bridge registers  | psp,smu |
| `0x03270000` | `0x0327ffff` | Programmable DMA     | smu,mp2 |
| `0x03280000` | `0x0328ffff` | alt HT bridge        | smu,mp2 |
| `0x04000000` | `0x3fffffff` | HT bridge mappings   | psp,smu |
