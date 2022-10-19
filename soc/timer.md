# Timer

The Common SoC contains up to 8 timers.

Timers are located at address:
  * `sysregs:0x400-0x423`: timer[0]
  * `sysregs:0x424-0x447`: timer[1]
  * `sysregs:0x448-0x46b`: timer[2]
  * `sysregs:0x46c-0x48f`: timer[3]
  * `sysregs:0x490-0x4b3`: timer[4]
  * `sysregs:0x4b4-0x4d7`: timer[5]
  * `sysregs:0x4d8-0x4fb`: timer[6]
  * `sysregs:0x4fc-0x51f`: timer[7]

The timers can run in several modes:
  * "free" running
  * system timer

## Memory layout

| Offset | Type      | Name       |
| ------ | --------- | ---------- |
| 0x00   | uint      | ctrl0      | 
| 0x04   | uint      | ctrl1      | 
| 0x08   | uint      | ctrl2      | 
| 0x0C   | uint      | int_enable | 
| 0x10   | uint      | interval   | 
| 0x14   | uint      | ???        | 
| 0x18   | uint      | ???        | 
| 0x1c   | uint      | ???        | 
| 0x20   | uint      | value      | 

## Free running

The timers can run in "free running" mode. In this mode, the `value` register is incremented at 100 MHz.

It is often used for a small delay, as a busy loop.

To do this:
  * set `ctrl0` = `latch` | `run`
  * read `value` in a loop until the delay is expired

## System timer

The system timer mode is used to generate interrupts at a fixed interval.

To do this:
  * set `int_enable` = 1
  * set `ctrl1` = `auto_reload`
  * set `interval` to the desired frequency
  * set `ctrl0` = `decrement`
  * set `ctrl0` = `decrement` | `latch` | `run`

An interrupt is sent each time the `value` reaches 0.
It is automatically reloaded to `interval`.

Apparently, only timer[0] can be used to generate an interrupt (IRQ 0x60).
## Registers

Note: the bits corresponding to one-shot operations are noted "cwd" (cleared-when-done).

### ctrl0

| bit | name      | description                                     |
| --- | --------- | ----------------------------------------------- |
|  0  | run       | 0=stop. 1=run                                   | 
|  8  | latch     | cwd. `value` = (`interval` if `decrement` else 0)<br>Note: `decrement` must be set before setting `latch`. | 
| 16  | decrement | 0=`value` increases. 1=`value` decreases        |
| 24  | ???       | kills the effect of `decrement` and `ceiling` ? |

### ctrl1

| bit | name         | description                                                        |
| --- | ------------ | ------------------------------------------------------------------ |
|  8  | auto_reload  | in decrement mode, set `value` = `interval` when `value` reaches 0 | 
| 16  | ceiling      | in increment mode, stop when `value` = 0xffffffff                  | 

### ctrl2

| bit | name          | description                     |
| --- | ------------- | ------------------------------- |
|  0  | inverval_step | Hmmm... it's hard to explain... | 


### int_enable

1=Enable interrupts. An interrupt pulse is sent in decrement mode when `value` reaches 0.

### interval

Can be used as a reload value for the timer.

### value

Current value of the timer. It is incremented or decremented at 100 MHz.
