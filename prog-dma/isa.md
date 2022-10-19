# Programmable DMA ISA

## Registers

The DMA controller has 8 channels, each one having a separate set of registers.

Each channel has the following registers:

* $pc (32-bits): Instruction Pointer. Contains the physical address of the next instruction.
* $src (32-bits): Source register. Contains the physical address of the data source.
* $dst (32-bits): Destination register. Contains the physical address of the data destination.
* $cnt0 (8-bits): Loop register 0. Counter used for loop instructions.
* $cnt1 (8-bits): Loop register 1. Counter used for loop instructions.
* $cfg (32-bits): Configuration register. Allows customization of load/store operations.

## Instruction set

| encoding             | operation  | details                                      |
| -------------------- | ---------- | -------------------------------------------- |
| 0x00<br>0x01         | ret        | stop the execution                          |
| 0x04<br>0x05<br>0x07 | load $src  | read data from $src to the internal buffer  |
| 0x08<br>0x09<br>0x0b | store $dst | write data to $dst from the internal buffer |
| 0x0c                 | zero $dst  | write zeros to $dst                        |
| 0x12<br>0x13         | ???        |                                              |
| 0x18                 | nop        | do nothing                                   |
| 0x20 u8              | set $cnt0  | $cnt0 = u8                                   |
| 0x22 u8              | set $cnt1  | $cnt1 = u8                                   |
| 0x2c u8              | ???        |                                              |
| 0x33<br>0x34<br>0x35<br>0x36<br>0x37 | ??? |                                     |
| 0x38 u8              | loop $cnt0 | if $cnt0-- == 0: goto u8                     |
| 0x3f u8              | loop $cnt1 | if $cnt1-- == 0: goto u8                     |
| 0x54 u16             | add $src   | $src += u16                                  |
| 0x56 u16             | add $dst   | $dst += u16                                  |
| 0x5c u16             | sub $src   | $src -= (0x10000 - u16)                      |
| 0x5e u16             | sub $dst   | $dst -= (0x10000 - u16)                      |
| 0xbc 00 u32          | set $src   | $src = u32                                   |
| 0xbc 01 u32          | set $cfg   | $cfg = u32                                   |
| 0xbc 02 u32          | set $dst   | $dst = u32                                   |

## Configuration register

The $cfg register can be used to customize the load and store operations.

| bits  | name         | usage                                                             |
| ----- | ------------ | ----------------------------------------------------------------- |
| 0     | src\_inc     | increment the $src register during and after a load operation     |
| 1     | src\_unit\_2 | reads from $src by chunks of 2 bytes                              |
| 2     | src\_unit\_4 | reads from $src by chunks of 4 bytes                              |
| 4-7   | src\_size    | number of chunks to read for a single load operation (minus one)  |
| 14    | dst\_inc     | increment the $dst register during and after a store operation    |
| 15    | dst\_unit\_2 | write to $dst by chunks of 2 bytes                                |
| 16    | dst\_unit\_4 | write to $dst by chunks of 4 bytes                                |
| 18-21 | dst\_size    | number of chunks to write for a store write operation (minus one) |
| 28    | swap\_2      | swap bytes 2-by-2 when copying                                    |
| 29    | swap\_4      | swap bytes 4-by-4 when copying                                    |

## Sample program

A simple program to copy data looks like this:

```
  set $src = <source address>
  set $dst = <dest address>
  set $cfg = <config>
  set $cnt0 = <number of iteration - 1>
label:
  load $src
  store $dst
  loop $cnt0, label
  ret
```
