# PSP timer

The PSP timer has several purposes:
  * get the number of "ticks" spent from the boot time;
  * get recurring interrupts.

## Register addresses

Offset | Type      | Name        |
------ | --------- | ----------- |
0x00   | uint      | int_ctrl0   | 
0x04   | uint      | int_ctrl1   | 
0x0C   | uint      | int_enable  | 
0x10   | uint      | int_freq    | 
0x24   | uint      | ticks_cfg   | 
0x28   | uint      | ticks_reg0  | 
0x2C   | uint      | ticks_reg1  | 
0x30   | uint      | ticks_reg2  | 
0x34   | uint      | ticks_reg3  | 
0x38   | uint      | ticks_reg4  | 
0x3C   | uint      | ticks_reg5  | 
0x40   | uint      | ticks_reg6  | 
0x44   | uint      | ticks_value | 

## "Recurring interrupts"

The `int_*` registers are used to control the periodic timer interrupt.

Recurring interrupts are enabled by writing `1` to int_enable. The timer frequency (or period ?) is written to `int_freq`. Some things are also written to `int_ctrl*`.

## Ticks

The `ticks_*` register are probably used to get ticks. They are used for busy-waiting sleeps.

To sleep for some time `n`, the PSP resets all `ticks_*` registers. It then sets `ticks_cfg` to `0x101` to start counting. It waits for `ticks_value` to increase by `n`. It then write `0` to `ticks_cfg` to stop counting.
