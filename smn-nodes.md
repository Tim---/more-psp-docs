# SMN nodes

Note: this article focuses on Summit-ridge. The details may vary for other versions.

SMN nodes are heterogeneous devices. However, they all have some common configuration registers that are used by the PSP to enable the devices, configure there speed (on the SMN bus ?), and protect the regions exposed to the SMN bus.

Two regions are used to configure the nodes:
  * region A: `0x01000000`-`0x010fffff` (256 nodes * 4k)
  * region B: `0x02f00000`-`0x02f3ffff` (256 nodes * 1k)

## Region A

| address         | type          | name          |
| --------------- | ------------- | ------------- |
| `0x008`         | u32           | enable?       |
| `0x810`         | u32           | frequency     |
| `0x814`         | u32           | clock_enable? |
| `0x82c`         | u32           | ?             |
| `0x830`         | u32           | ?             |
| `0x834`         | u32           | ?             |
| `0x840`         | u32           | ?             |
| `0x84c-0x92b`   | u32[]         | 3-bitmap      |
| `0x92c`         | general_sec_t | general_sec   |
| `0x950`-`0xa6f` | range_sec_t[] | range_sec     |

general_sec_t:

| address | type | name          |
| ------- | ---- | ------------- |
| `0x00`  | u32  | ?             |
| `0x04`  | u32  | ?             |
| `0x10`  | u32  | write_bitmap  |
| `0x2c`  | u32  | read_bitmap   |
| `0x20`  | u32  | ?             |

range_sec_t:

| address | type | name          |
| ------- | ---- | ------------- |
| `0x00`  | u32  | begin         |
| `0x04`  | u32  | end           |
| `0x10`  | u32  | write_bitmap  |
| `0x2c`  | u32  | read_bitmap   |
| `0x20`  | u32  | ?             |

### Security gasket

Each SMN node has a unique id and one or more exposed SMN region.

For example, the first UMC has id `0x96`, and exposes its configuration registers in the range SMN:`0x00050000`-`0x00051fff`.

However, not all exposed registers should be accessible by any chip. For example, we may want some registers to be readable or writable only to the PSP or SMU, and not the x86 cores.

During the security gasket, the PSP configures the permissions for each node. It can set the read/write permissions for a whole device using the general_sec registers.

It can also fine tune to set different permissions for specific ranges of exposed registers using the range_sec registers.

### Permissions

Each device that can access the SMN bus (PSP, SMU, x86 through the PCIe host bridge) is assigned an "initiatorTrust" level (lower is better):

* PSP: probably level 0
* SMU: level 1 or 2
* x86: level >= 3

The PSP configures the allowed levels using the write_bitmap and read_bitmap fields.

* write_bitmap format: 0x1*xx* where *xx* is a bitmap of initiatorTrusts allowed to write.
* read_bitmap format: 0x2*xx* where *xx* is a bitmap of initiatorTrusts allowed to read

## Region B

| address | type | name |
| ------- | ---- | ---- |
| 0x004   | u32  | ???  |
