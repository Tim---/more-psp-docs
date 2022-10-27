# SMU devices

The SMU uses the same "SoC" as the PSP.

## Memory layout

| begin        | end          | name                 |
| ------------ | ------------ | -------------------- |
| `0x00000000` | `0x0003ffff` | SRAM                 | 
| `0x01000000` | `0x02ffffff` | SMN bridge mappings  |
| `0x03010000` | `0x0301ffff` | sysregs (public)     |
| `0x03200000` | `0x0320ffff` | sysregs (private)    |
| `0x03210000` | `0x0321ffff` | ???                  |
| `0x03220000` | `0x0322ffff` | SMN bridge registers |
| `0x03230000` | `0x0323ffff` | HT bridge registers  |
| `0x03270000` | `0x0327ffff` | Programmable DMA     |
| `0x03280000` | `0x0328ffff` | alt HT bridge        |
| `0x04000000` | `0x3fffffff` | HT bridge mappings   |
