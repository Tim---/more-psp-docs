# PSP entries

## Entries list

The Name columns is followed by an interrogation mark if it is not in amdfwtool.

Num  | Format           | Name                    |
---- | ---------------- | ----------------------- |
0x00 | pubkey           | FW_PSP_PUBKEY           |
0x01 | fw               | FW_PSP_BOOTLOADER       |
0x02 |                  | FW_PSP_SECURED_OS       |
0x03 | fw               | FW_PSP_RECOVERY         |
0x04 |                  | FW_PSP_NVRAM            |
0x05 | signed_pubkey    | FW_PSP_RTM_PUBKEY       |
0x06 |                  | (X86_STUB?)             |
0x07 |                  | (?)                     |
0x08 | fw               | FW_PSP_SMU_FIRMWARE     |
0x09 | signed_pubkey    | FW_PSP_SECURED_DEBUG    |
0x0A | signed_pubkey    | (AGESA_PUBKEY?)         |
0x0B | soft_fuse        | PSP_FUSE_CHAIN          |
0x0C | fw               | FW_PSP_TRUSTLETS        |
0x0D | signed_pubkey    | FW_PSP_TRUSTLETKEY      |
0x10 | fw               | (FW?)                   |
0x12 | fw               | FW_PSP_SMU_FIRMWARE2    |
0x13 | fw               | DEBUG_UNLOCK            |
0x14 | fw               | (FW?)                   |
0x1A |                  | (EMPTY?)                |
0x20 | fw               | HW_IPCFG                |
0x21 | wrapped_ikek     | WRAPPED_IKEK            |
0x22 |                  | TOKEN_UNLOCK            |
0x24 | fw               | SEC_GASKET              |
0x25 | fw               | MP2_FW                  |
0x28 | fw               | DRIVER_ENTRIES          |
0x29 |                  | FW_KVM_IMAGE            |
0x2A | fw               | (FW?)                   |
0x2B |                  | (SIGNATURE?)            |
0x2D |                  | S0I3_DRIVER             |
0x2E | fw               | (?)                     |
0x2F | fw               | (?)                     |
0x30 | fw               | ABL0                    |
0x31 | fw               | ABL1                    |
0x32 | fw               | ABL2                    |
0x33 | fw               | ABL3                    |
0x34 | fw               | ABL4                    |
0x35 | fw               | ABL5                    |
0x36 | fw               | ABL6                    |
0x37 | fw               | ABL7                    |
0x3A |                  | FW_PSP_WHITELIST        |
0x3C | fw               | VBIOS_BTLOADER          |
0x40 | psp_dir          | FW_L2_PTR               |
0x42 | fw               | (FW?)                   |
0x43 | signed_pubkey    | (PUBKEY?)               |
0x44 | fw               | FW_USB_PHY              |
0x45 | fw               | FW_TOS_SEC_POLICY       |
0x46 |                  | (?)                     |
0x47 | fw               | FW_DRTM_TA              |
0x48 | psp_dir          | FW_RECOVERYAB_A         |
0x49 | bios_dir         | FW_BIOS_TABLE           |
0x4A | psp_dir          | FW_RECOVERYAB_B         |
0x4C | fw               | (?)                     |
0x4D | fw               | (?)                     |
0x4E | signed_pubkey    | (PUBKEY?)               |
0x50 | keydb            | FW_KEYDB_BL             |
0x51 | keydb            | FW_KEYDB_TOS            |
0x52 |                  | FW_PSP_VERSTAGE         |
0x53 |                  | FW_VERSTAGE_SIG         |
0x54 |                  | RPMC_NVRAM              |
0x55 | fw               | FW_SPL                  |
0x58 | fw               | FW_DMCU_ERAM            |
0x59 | fw               | FW_DMCU_ISR             |
0x5A |                  | FW_MSMU                 |
0x5C |                  | FW_SPIROM_CFG           |
0x5F |                  | FW_PSP_SMUSCS           |
0x71 |                  | FW_DMCUB                |
0x73 |                  | FW_PSP_BOOTLOADER_AB    |
0x8d |                  | AMD_TA_IKEK             |

## Detail

### 0x00 - FW_PSP_PUBKEY

Root RSA key. It is hardcoded in the on-chip bootloader, and it is used to sign the secondary keys, and signed entries.

### 0x01 - FW_PSP_BOOTLOADER

Loaded by the on-chip bootloader of the PSP.

### 0x02 - FW_PSP_SECURED_OS

Executed by the PSP after the bootloader, during runtime. Runs in "system" mode, and implements the syscalls for the user applications.

### 0x03 - FW_PSP_RECOVERY

Recovery bootloader ?

### 0x04 - FW_PSP_NVRAM

Nvram, containing RW non-volatile data.

### 0x05 - FW_PSP_RTM_PUBKEY

Secondary RSA key. Authenticates some entries.

### 0x06 - (X86_STUB?)

### 0x07 - (?)

### 0x08 - FW_PSP_SMU_FIRMWARE

First part of the SMU firmware. It is loaded by the PSP and executed by the SMU.

### 0x09 - FW_PSP_SECURED_DEBUG

### 0x0A - (AGESA_PUBKEY?)

Secondary RSA key. Authenticates the AGESA entries.

### 0x0B - PSP_FUSE_CHAIN

Not an actual entry (no data). Contains a bitmap of options for the bootloader.

### 0x0C - FW_PSP_TRUSTLETS

### 0x0D - FW_PSP_TRUSTLETKEY

Secondary RSA key. Authenticates the TRUSTLETS.

### 0x10 - (FW?)

### 0x12 - FW_PSP_SMU_FIRMWARE2

Second part of the SMU firmware. 

### 0x13 - DEBUG_UNLOCK

### 0x14 - (FW?)

### 0x1A - (EMPTY?)

### 0x20 - HW_IPCFG

### 0x21 - WRAPPED_IKEK

Wrapped AES key, used to encrypt some entries (mainly the PSP bootloader on old processors). It is wrapped by another AES key hardcoded in the on-chip bootloader.

### 0x22 - TOKEN_UNLOCK

### 0x24 - SEC_GASKET

Small program run by the PSP. It writes registers in the SMN nodes to prevent access to senstive registers from the x86 host.

### 0x25 - MP2_FW

Firmware of the MP2 core.

### 0x28 - DRIVER_ENTRIES

### 0x29 - FW_KVM_IMAGE

### 0x2A - (FW?)

### 0x2B - (SIGNATURE?)

### 0x2D - S0I3_DRIVER

### 0x2E - (?)

### 0x2F - (?)

### 0x30-0x37 - ABLx

Agesa bootloader. 

In old processors, ABL0 is the "scheduler", which executes the other programs.

In newer processor, there is only an ABL0 entry containing all other parts.

### 0x3A - FW_PSP_WHITELIST

### 0x3C - VBIOS_BTLOADER

### 0x40 - FW_L2_PTR

Secondary PSP directory table.

### 0x42 - (FW?)

### 0x43 - (PUBKEY?)

### 0x44 - FW_USB_PHY

### 0x45 - FW_TOS_SEC_POLICY

### 0x46 - (?)

### 0x47 - FW_DRTM_TA

### 0x48 - FW_RECOVERYAB_A

### 0x49 - FW_BIOS_TABLE

### 0x4A - FW_RECOVERYAB_B

### 0x4C - (?)

### 0x4D - (?)

### 0x4E - (PUBKEY?)

### 0x50 - FW_KEYDB_BL

### 0x51 - FW_KEYDB_TOS

### 0x52 - FW_PSP_VERSTAGE

### 0x53 - FW_VERSTAGE_SIG

### 0x54 - RPMC_NVRAM

### 0x55 - FW_SPL

### 0x58 - FW_DMCU_ERAM

### 0x59 - FW_DMCU_ISR

### 0x5A - FW_MSMU

### 0x5C - FW_SPIROM_CFG

### 0x5F - FW_PSP_SMUSCS

### 0x71 - FW_DMCUB

### 0x73 - FW_PSP_BOOTLOADER_AB

### 0x8d - AMD_TA_IKEK

