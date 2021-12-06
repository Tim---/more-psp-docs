# PSP interrupt controller

The PSP interrupt controller supports 128 interrupts.

## Register mapping

Offset | Type      | Name        |
------ | --------- | ----------- |
0x00   | uint[4]   | array0      | 
0x10   | uint[4]   | array1      | 
0x20   | uint[4]   | enable      | 
0xB0   | uint[4]   | ack         | 
0xC0   | uint      | no_more_int | 
0xC4   | uint      | irq_num     | 

## Description

Note that several registers are bitmaps of type `uint[4]`. 
In this case, interrupt `n` is represented by bit `n % 32` of register index `n / 32`.

To enable an interrupt, the bootloader sets the bit corresponding to the IRQ number in `enable`.

When the interrupt handler is invoked, the handler gets the current interrupt number from register `irq_num`. After handling the interrupts, it writes the corresponding bit in `ack`.

If `no_more_int` is zero, there is another interrupt pending, and we can do the same thing again.

## Registers

### enable[i]

Each bit can be toggled to enable individual interrupts. 

### ack[i]

Each bit can be set to acknowledge an interrupt.

### no_more_int

This register is `1` if there are no more interrupts to process.

### irq_num

This register contains the current IRQ being processed.

## Known interrupts

IRQ  | Name          |
---- | ------------- |
0x10 | SMU doorbell  | 
0x15 | CCP           | 
0x3c | BIOS doorbell | 
0x60 | Timer         | 
