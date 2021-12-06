# SMN bridge

The SMN bridge allows the PSP to map parts of the SMN space.

It allows to map 32 memory regions of 1MB that point to the SMN space.

The SMN bridge exposes two register maps:
  * 01000000-02ffffff: SMN bridge mappings (32 slots * 0x100000)
  * 03220000-0322ffff: SMN bridge registers

## Registers memory

The registers region mapping is simple:

Offset | Type      | Name  |
------ | --------- | ----- |
0x0000 | u16[0x20] | slots | 

## Description

The mapping `i` is controlled with the corresponding `slots[i]` register that contains the high 12 bits of the SMN address.

Eg: writing `0x123` to the address `0x03220008` (`slots[4]`) will map the PSP addresses `01400000-014fffff` to SMN addresses `12300000-123fffff`. See the [SMN address space description](../smn.md).

Note that the PSP cannot write a single slot since it can only write 32-bits integer to the registers region. It will must write two slots at once (keeping the same value for the untouched slot).