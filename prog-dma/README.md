# Programmable DMA

The "common SoC" has a programmable DMA controller. It is used by the SMU, mainly to copy data from/to the SMN and HT regions (the PSP uses the CCP).

Unlike simple DMA controllers, it is really a microcontroller with a simple instruction set specialized for copying data. The microarchitecture is custom.
