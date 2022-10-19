# Programmable DMA controller memory region

The programmable DMA controller region allows the SMU and MP2 to control the [programmable DMA](../prog-dma/README.md).

It is located at address `0x03270000`:`0x0327ffff`.

## Memory region layout

| offset | type        | name          | usage                                      |
| ------ | ----------- | ------------- | ------------------------------------------ |
| 0x020  | u32         | ???           | bitmap?                                    |
| 0x024  | u32         | ???           | bitmap?                                    |
| 0x034  | u32         | error\_bitmap | bitmap of channels with an error           |
| 0x040  | u32[8]      | error[]       | contains the error code for each channel   |
| 0x100  | state\_t[8] | state[]       | state of the channel                       |
| 0x400  | regs\_t[8]  | registers[]   | register values of the channel             |
| 0xd00  | ctrl\_t     | control       | registers to send commands to the channels | 
| 0xe00  | u32[8]      | ???           |                                            |
| 0xe80  | u32         | ???           |                                            |
| 0xfe0  | u32[8]      | ???           |                                            |

state\_t:
| offset | type   | name          | usage                          |
| ------ | ------ | ------------- | ------------------------------ |
| 0x0    | u32    | status        | status of the channel          |
| 0x4    | u32    | pc            | program counter of the channel |

regs\_t:
| offset | type   | name | usage          |
| ------ | ------ | ---- | -------------- |
| 0x00   | u32    | src  | value of $src  | 
| 0x04   | u32    | dst  | value of $dst  |
| 0x08   | u32    | cfg  | valud of $cfg  |
| 0x0c   | u32    | cnt0 | value of $cnt0 |
| 0x10   | u32    | cnt1 | value of $cnt1 |
| 0x14   | u32    | ???  |                |
| 0x18   | u32    | ???  |                |
| 0x1c   | u32    | ???  |                |

ctrl\_t:
| offset | type   | name       | usage                                  |
| ------ | ------ | ----       | -------------------------------------- |
| 0x00   | u32    | status     | nonzero if busy                        |
| 0x04   | u32    | exec       | write to start running                 |
| 0x08   | u32    | cmd        | command to execute                     |
| 0x0c   | u32    | prog\_addr | physical address of the program to run |


## Commands

Process to execute a command:

* wait for `control.status & 1 == 0` (not busy)
* write the command to `control.cmd`
* if the command is "run\_program", write the program address to `control.prog_addr`
* write 0 to `control.exec` to execute the command

Once a command is sent, it can monitor the state of the channel using `state[n]`, `registers[n]`, `error[n]`.

The format of `control.cmd` determines the commands to execute. 

| command      | cmd[3] | cmd[2] | cmd[1] | cmd[0] | usage                                                                |
| ------------ | ------ | ------ | ------ | ------ | -------------------------------------------------------------------- |
| run\_program | n      | 0xa0   |        |        | execute the program at address `control.prog_addr` using channel `n` |
| clear        |        | 0x01   | n      | 0x01   | clear the errors of channel `n`                                      |

