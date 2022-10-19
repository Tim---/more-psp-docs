# System registers

The "sysregs" region (for lack of a better name) is composed of two regions:

  * `03010000-0301ffff`: "public" sysregs
  * `03200000-0320ffff`: "private" sysregs

They contain miscellaneous registers, and some devices:
  * [timer](timer.md)
  * [intc](intc.md)

## private vs public

Although the sysregs is composed of two regions, we assume that it is "the same" region.

This is how the PSP (summit) accesses the intc device (note that it uses public and private regions):

| Offset     | Name        |
| ---------- | ----------- |
| `03010300` | enable      | 
| `03200310` | A           | 
| `03200320` | B           | 
| `030103c0` | no_more_int | 
| `030103c4` | current_int | 

And this is how the SMU (summit) does (note that it only uses the private region):

| Offset     | Name        |
| ---------- | ----------- |
| `03200300` | enable      | 
| `03200310` | A           | 
| `03200320` | B           | 
| `032003c0` | no_more_int | 
| `032003c4` | current_int | 

So we assume that the "public" and "private" regions are an alias to the "backend" sysregs region.
The public and private regions only map certain parts of the backend region, but they use the same offsets.

## Region access

The public-sysregs region of some cores can be accessed with the SMN bus:

| start        | end          | name |
| ------------ | ------------ | ---- |
| `0x03810000` | `0x0381ffff` | PSP  |
| `0x03b10000` | `0x03b1ffff` | SMU  |
| `0x03e10000` | `0x03e1ffff` | MP2  |

Accessing the public regions from the SMN bus is used to send mailbox messages.

The public-sysregs region of the PSP can also be accessed with the CCP PCI device (BAR2, offset `0x00010000`-`0x0001ffff`).
