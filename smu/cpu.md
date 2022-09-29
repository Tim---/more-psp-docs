# SMU CPU

The SMU is based on an Xtensa processor.

This is a guess of the Options and Configuration Additions for the processor.

Refer to the "Xtensa Instruction Set Architecture (ISA) Reference Manual".

## 4.2 Core Architecture

| Parameter | Value |
| --------- | ----- |
| msbFirst  | 0     |

## 4.3 Options for Additional Instructions

1.  ✅ Code Density Option
2.  ✅ Loop Option
3.  ✅ Extended L32R Option
4.  ✅ 16-bit Integer Multiply Option
5.  ✅ 32-bit Integer Multiply Option
6.  ✅ 32-bit Integer Divide Option
7.  ❌ MAC16 Option
8.  ✅ Miscellaneous Operations Option
9.  ❌ Coprocessor Option
10. ✅ Boolean Option
11. ✅ Floating-Point Coprocessor Option
12. ❌ Multiprocessor Synchronization Option
13. ✅ Conditional Store Option

## 4.4 Options for Interrupts and Exceptions

1.  ✅ Exception Option

| Parameter             | Value |
| --------------------- | ----- |
| NDEPC                 | 0     |
| ResetVector           | 0x100 |
| UserExceptionVector   | 0x23c |
| KernelExceptionVector | 0x23c |
| DoubleExceptionVector |       |
2.  ✅ Relocatable Vector Option
3.  ❓ Unaligned Exception Option
4.  ✅ Interrupt Option

| Parameter                | Value |
| ------------------------ | ----- |
| NINTERRUPT               | ?     |
| INTTYPE[0..NINTERRUPT-1] | ?     |
| LEVEL[0..NINTERRUPT-1]   | ?     |
5.  ✅ High-Priority Interrupt Option

| Parameter                       | Value |
| ------------------------------- | ----- |
| NLEVEL                          | 6     |
| EXCMLEVEL                       | ?     |
| NNMI                            | ?     |
| LEVEL[0..NINTERRUPT-1]          | ?     |
| InterruptVector[2..NLEVEL+NNMI] | 0x17c |
| LEVELMASK[1..NLEVEL-1]          | ?     |
6.  ❌ Timer Interrupt Option

## 4.5 Options for Local Memory

2.  ✅ Instruction Cache Option

| Parameter          | Value |
| ------------------ | ----- |
| InstCacheWayCount  | ?     |
| InstCacheLineBytes | 32?   |
| InstCacheBytes     | ?     |
| MemErrDetection    | ?     |
| MemErrEnable       | ?     |
3.  ❌ Instruction Cache Test Option
4.  ✅ Instruction Cache Index Lock Option
5.  ✅ Data Cache Option

| Parameter          | Value |
| ------------------ | ----- |
| DataCacheWayCount  | ?     |
| DataCacheLineBytes | 16?   |
| DataCacheBytes     | ?     |
| IsWriteback        | ?     |
| MemErrDetection    | ?     |
| MemErrEnable       | ?     |
6.  ❌ Data Cache Test Option
7.  ✅ Data Cache Index Lock Option
9.  ❌ Instruction RAM Option
10. ❌ Instruction ROM Option
11. ❌ Data RAM Option
12. ❌ Data ROM Option
13. ❌ XLMI Option
14. ❌ Hardware Alignment Option
15. ❌ Memory ECC/Parity Option


## 4.6 Options for Memory Protection and Translation

3.  ❌ Region Protection Option
4.  ❌ Region Translation Option
5.  ✅ MMU Option

| Parameter       | Value    |
| --------------- | -------- |
| NIREFILLENTRIES | 16       |
| NDREFILLENTRIES | 32       |
| IVARWAY56       | Variable |
| DVARWAY56       | Variable |

## 4.7 Options for Other Purposes

1.  ✅ Windowed Register Option

| Parameter         | Value |
| ----------------- | ----- |
| WindowOverflow4   | 0x000 |
| WindowUnderflow4  | 0x040 |
| WindowOverflow8   | 0x080 |
| WindowUnderflow8  | 0x0c0 |
| WindowOverflow12  | 0x100 |
| WindowUnderflow12 | 0x140 |
| NAREG             | 64    |
2.  ✅ Processor Interface Option
3.  ✅ Miscellaneous Special Registers Option

| Parameter | Value |
| --------- | ----- |
| NMISC     | 2     |
4.  ❌ Thread Pointer Option
5.  ✅ Processor ID Option
6.  ✅ Debug Option

| Parameter  | Value |
| ---------- | ----- |
| DEBUGLEVEL | ?     |
| NIBREAK    | ?     |
| NDBREAK    | ?     |
| SZICOUNT   | ?     |
7.  ❌ Trace Port Option

