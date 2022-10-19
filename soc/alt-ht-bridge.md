# Alternative HT bridge

The alternative HT bridge allows the SMU and MP2 to read the [HT](../ht.md) address space.

The alt HT bridge uses one region:
  * `03280000-0328ffff`: alt HT bridge registers

## Memory layout

| Offset | Type      | Name    |
| ------ | --------- | ------- |
| 0x00   | u32       | addr_lo |
| 0x04   | u32       | addr_hi |
| 0x08   | u32       | ctrl    |
| 0x0c   | u32       | ???     |
| 0x10   | u32       | ???     |
| 0x14   | u32[0x10] | wbuf    |
| 0x54   | u32[0x10] | rbuf    |
