# CCX

Note: the following is for the Summit version

Each CCD contains 2 CCX. Each CCX contains 4 cores.

## SMN layout

| begin        | end          | type  | name   |
| ------------ | ------------ | ----- | ------ |
| `0x18000000` | `0x180fffff` | ccx_t | ccx[0] |
| `0x18400000` | `0x184fffff` | ccx_t | ccx[1] |

ccx_t:

| begin     | end       | type      | name    |
| --------- | --------- | --------- | ------- |
| `0x00000` | `0x1ffff` | core_t    | core[0] |
| `0x20000` | `0x3ffff` | core_t    | core[1] |
| `0x40000` | `0x5ffff` | core_t    | core[2] |
| `0x60000` | `0x7ffff` | core_t    | core[3] |
| `0x80000` | `0xfffff` | ccx_cfg_t | ccx_cfg |

ccx_cfg_t:

| address         | type          | name          |
| --------------- | ------------- | ------------- |
| `0x084`         | ccx_int_t[3]  | int_ccx       |
| `0x0e0`         | u32           | int_ack       |

ccx_int_t:

| address | type | name          |
| ------- | ---- | ------------- |
| `0x0`   | u32  | int_cb        |
| `0x4`   | u32  | int_bitmap    |
| `0x8`   | u32  | int_?         |

core_t:

| address         | type          | name          |
| --------------- | ------------- | ------------- |
| `0x200`         | u32[3]        | int_cb        |
| `0x20c`         | u32[3]        | int_?         |
| `0x218`         | u32[3]        | int_bitmap    |
| `0x234`         | u32           | int_ack       |

