# PSP "SoC"

## Memory mapping

The memory mapping of the PSP is :

Start      | End        | Name                    |
---------- | ---------- | ----------------------- |
0x00000000 | 0x0003ffff | SRAM                    | 
0x01000000 | 0x02ffffff | SMN bridge mappings     | 
0x03000000 | 0x0300ffff | CCP registers           | 
0x03010000 | 0x0301ffff | PSP registers (public)  | 
0x03200000 | 0x0320ffff | PSP registers (private) | 
0x03220000 | 0x0322ffff | SMN bridge registers    | 
0x03230000 | 0x0323ffff | SysHub bridge registers | 
0x04000000 | 0x3fffffff | SysHub bridge mappings  | 

## Devices

  * [PSP Registers](psp-registers.md)
  * [CCP](ccp.md)
  * [SMN bridge](smn-bridge.md)
  * [SysHub bridge](syshub-bridge.md)
