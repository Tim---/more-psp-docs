# PSP internal registers

The PSP registers are located in regions 03010000-0301ffff (public) and 03200000-0320ffff (private).

The first range is accessible to the X86 processor, and probably the SMU while the second isn't.

We postulate that both ranges point to the same register space because some mappings are similar.
pspFor example, an interrupt related functions uses several u32[4] arrays at offsets 0x03010300, 0x03200310 and 0x03200320. 

## Register addresses

### Common

Offset | Type      | Name           |
------ | --------- | -------------- |
0x004  | uint      | ???            | 
0x04c  | uint      | psp_version    | 
0x104  | uint      | ???            | 
0x108  | uint64    | ticks          | 
0x400  | timer     | timer          | 
0x570  | uint      | bios::io       | 
0x574  | uint      | bios::addr0    | 
0x578  | uint      | bios::addr1    | 
0x69c  | uint      | ???            | 
0x6a0  | uint      | ???            | 
0x70c  | uint      | smu_related0   | 
0x710  | uint      | smu_related1   | 
0x714  | uint      | smu_related2   | 
0x71c  | uint      | smu::io        | 
0x994  | uint      | ???            | 
0x998  | uint      | ???            | 
0x9ec  | uint      | bl_version_bis | 

### type2-specific registers

Offset | Type      | Name           |
------ | --------- | -------------- |
0x03c  | uint      | serial_enable  | 
0x044  | uint      | bl_version     | 
0x0a0  | uint[?]   | some_array     | 
0x300  | int_ctrl  | int_controller | 

### type3-specific registers

Offset | Type      | Name           |
------ | --------- | -------------- |
0x040  | uint      | serial_enable  | 
0x048  | uint      | bl_version     | 
0x090  | uint[?]   | some_array     | 
0x144  | uint      | ???            | 
0x148  | uint      | ???            | 
0x14c  | uint      | ???            | 
0x160  | uint[4]   | int::a3[4]     | 
0x300  | int_ctrl  | int_controller | 

## Version

The register `psp_version` contains the [version](../versions.md) of the PSP.

If the minor version is 0 (0xbc0a00xx), we have a "type2" PSP. If it is another value (0xbc0axxxx), we have a "type3" PSP. The layout of some PSP registers changes depending on the PSP version.
