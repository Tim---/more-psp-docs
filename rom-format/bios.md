# BIOS entries

## Entries list

The Name columns is followed by an interrogation mark if it is not in amdfwtool.

Num  | Format           | Name              |
---- | ---------------- | ----------------- |
0x05 | signed_pubkey    | RTM_PUBKEY        |
0x07 |                  | SIG               |
0x60 | apcb             | APCB              |
0x61 |                  | APOB              |
0x62 |                  | BIN               |
0x63 |                  | APOB_NV           |
0x64 | fw               | PMUI              |
0x65 | fw               | PMUD              |
0x66 |                  | UCODE             |
0x67 |                  | (?)               |
0x68 | apcb             | APCB_BK           |
0x6a |                  | MP2_CFG           |
0x6b |                  | PSP_SHARED_MEM    |
0x70 | bios_dir         | L2_PTR            |


## Detail

### 0x05 - RTM_PUBKEY

Secondary RSA key. Authenticates the other entries.

### 0x07 - SIG

### 0x60 - APCB

AGESA PSP Customization block.

### 0x61 - APOB

Not an actual entry (no data). Gives the address in HT where the PSP should write the APOB data.

### 0x62 - BIN

UEFI image.

### 0x63 - APOB_NV

### 0x64 - PMUI

PMU firmware (instructions).

### 0x65 - PMUD

PMU firmware (data).

### 0x66 - UCODE

Microcode patches.

### 0x67 - (?)

### 0x68 - APCB_BK

AGESA PSP Customization block - backup.

### 0x6a - MP2_CFG

### 0x6b - PSP_SHARED_MEM

### 0x70 - L2_PTR

Secondary BIOS directory table.
