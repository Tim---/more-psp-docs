# APCB format

The APCB (AMD PSP Customization Block) is an unsigned ROM entry that can be
modified to change the behavior of the AGESA bootloader.

The content is divided in categories (eg: MEMG for memory related customization,
FCHG for FCH customization, etc.).
Each category contains several types.
Each type can contain a number of tokens.

## File structure

### Header

Offset | Format   | Name     | Description                  |
------ | -------- | -------- | ---------------------------- |
0x00   | char[4]  | magic    | `APCB`                       |
0x04   | u32      | version  | `0x00200020`                 |
0x08   | u32      | size     | total size, including header |
0x0C   | u32      | ???      |                              |
0x10   | u8[8]    | reserved | null bytes                   |
0x20   | group[*] | groups   | array of groups              |

### Group

Offset | Format   | Name     | Description                  |
------ | -------- | -------- | ---------------------------- |
0x00   | char[4]  | name     | name of the group            |
0x04   | u16      | id       | id of the group              |
0x06   | u16      | ???      | `0x10`                       |
0x08   | u16      | ???      | `0x1`                        |
0x0A   | u16      | ???      | `0x0`                        |
0x0C   | u32      | size     | group size, including header |
0x10   | type[*]  | types    | array of types               |

### Type

Offset | Format   | Name     | Description                  |
------ | -------- | -------- | ---------------------------- |
0x00   | u16      | group_id | id of the group              |
0x02   | u16      | id       | id of the type               |
0x04   | u16      | size     | type size, including header  |
0x06   | u16      | ???      | `0x0`                        |
0x08   | u8[8]    | reserved | null bytes                   |
0x10   | u8[*]    | data     | content                      |

## Tokens structure

A type can contain several parameters called tokens.
Each token has a 13-bit identifier, and a value encoded with one or more bytes.

Bits   | Name     | Description                                 |
------ | -------- | ------------------------------------------- |
0:7    | ???      | `0x1`                                       |
8:20   | token    | token identifier or `0x1fff` for terminator |
21:23  | size     | value size minus 1                          |
24:31  | ???      | `0x0`                                       |

# Content

## PSPG - 0x1701

### Type 0x60

Used by ABL0 to get the PSP generation. Contains a set of register to read/write to get the generation.
If the generation does not match, it loads another ACPB image.

## CCXG - 0x1702

## DFG  - 0x1703

### Type 0x05 / 0x06

Tokens 0x0301 -> 0x030d.

## MEMG - 0x1704

### Type 0x07 / 0x08

Tokens 0x0701 -> 0x0740

### Type 0x30
### Type 0x31
### Type 0x33
### Type 0x40
### Type 0x50
### Type 0x52
### Type 0x53
### Type 0x59
### Type 0x5A
### Type 0x5B
### Type 0x5C
### Type 0x5D

## FCHG - 0x1706

### Type 0x0B / 0x0C

Tokens 0x1c01 -> 0x1c05.

  * 0x1c01: enable serial port
  * 0x1c02: choose the serial port to use (0 = io port 0x3f8, 1 = mmio port 0xfedc9000, 2 = 0xfedca000)
  * 0x1c03: trace assert fails
  * 0x1c04: sleep after test point

## CBSG - 0x1707

### Type 0x0D / 0x0F

Tokens 0x0001 -> 0x00ac.
