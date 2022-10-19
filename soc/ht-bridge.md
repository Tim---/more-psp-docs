# HT bridge

The HT bridge allows the PSP to map parts of the [HT](../ht.md) address space.

It allows to map 15 memory regions of 64 MiB that point to the HT space.

The HT bridge exposes two regions:
  * `03230000-0323ffff`: HT bridge registers
  * `04000000-3fffffff`: HT bridge mappings (15 slots of 64 MiB)

## Register table

Offset | Type              | Name        |
------ | ----------------- | ----------- |
0x0000 | ht_slot[0x3e]     | slots       |
0x03e0 | uint[0x3e]        | array_a     |
0x04d8 | uint[0x3e]        | array_b     |
0x05f0 | uint              | apply       |
0x8000 | aes_key[4]        | aes_keys    |
0x8040 | uint              | aes_related |

Where the datatype `ht_slot` is defined as follows:

Offset | Type | Name   |
------ | ---- | ------ |
0x00   | uint | addr   |
0x04   | uint | status |
0x08   | uint | type1  |
0x0c   | uint | type2  |

## Description

The registers layout seems to indicate that 62 slots are available in the HT bridge, although only 15 are used by the PSP.

The slot `i` is controlled via `slots[i]`, `array_a[i]`, `array_b[i]`.

When the slot is free'd, all the previous values are set to `0`.

## Registers

### slots[i].addr

Contains the high bits of the mapped address. It is shifted by 26 bits to get the base address.

### slots[i].status

This is set to `0x12` to indicate that the slot is active.

### slots[i].type1

This is set to `1` or `4` for "normal" memory (cache enabled), and `6` for "device" memory (cache disabled).

### slots[i].type2

Same value as `slots[i].type1`.

### array_a[i]

Unknown use. Set to `0xffffffff`.

### array_b[i]

Partially known use. Set to one of `0xc0000000`, `0xc0800000`, `0xc0808000`.

It seems that bits 13-14 are used to indicate the index of the AES key to use for encryption when accessing this memory. Maybe bit 15 is used to indicate that encryption must be used ?

### apply

This register is set to `0x3333` after a mapping is enabled. It is not written when a mapping is disabled, nor when the AES key index in `array_b[i]` is changed.

### aes_key[j]

This array can contain 4 AES keys of 16 bytes. It seems to be used to allow memory encryption.

### aes_related

Unknown. This is set to `0` before creating the first mapping.
