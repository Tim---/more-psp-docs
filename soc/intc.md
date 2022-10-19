# Interrupt controller

The common SoC contains two interrupt controllers:

  * `sysregs:0x200-0x2ff`: "small" interrupt controller (8 interrupts)
  * `sysregs:0x300-0x3ff`: "big" interrupt controller (128 interrupts)

## Register mapping

"small" interrupt controller:

Offset | Type      | Name        |
------ | --------- | ----------- |
0x00   | uint[1]   | enable      | 
0x04   | uint[1]   | A           | 
0x08   | uint[1]   | B           | 
0x0C   | byte[0x8] | prio        |
0x14   | uint[1]   | ack         | 
0x18   | uint      | no_more_int | 
0x1C   | uint      | current_int | 

"big" interrupt controller:

Offset | Type      | Name        |
------ | --------- | ----------- |
0x00   | uint[4]   | enable      | 
0x10   | uint[4]   | A           | 
0x20   | uint[4]   | B           | 
0x30   | byte[0x80]| prio        |
0xB0   | uint[4]   | ack         | 
0xC0   | uint      | no_more_int | 
0xC4   | uint      | current_int | 

## Description

Note that several registers are bitmaps of type `uint[N]`. 
In this case, interrupt `n` is represented by bit `n % 32` of register index `n / 32`.

To enable an interrupt, the bootloader sets the bit corresponding to the IRQ number in `enable`.

When the interrupt handler is invoked, the handler gets the current interrupt number from register `current_int`. After handling the interrupts, it writes the corresponding bit in `ack`.

If `no_more_int` is zero, there is another interrupt pending, and we can do the same thing again.

## Registers

### enable[]

Each bit can be toggled to enable individual interrupts. 

### A[]

Unknown bitmap

### B[]

Unknown bitmap

### prio[]

Interrupt priority. `prio[0]` contains the interrupt number with the most priority.

### ack[]

Each bit can be set to acknowledge an interrupt.

### no_more_int

This register is `1` if there are no more interrupts to process.

### current_int

This register contains the current IRQ being processed.

## Known interrupts

"big" interrupt controller:

IRQ  | Name          |
---- | ------------- |
0x10 | SMU doorbell  | 
0x15 | CCP           | 
0x3c | BIOS doorbell | 
0x60 | Timer         | 
