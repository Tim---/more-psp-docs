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
