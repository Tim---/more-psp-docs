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
0x48 | psp_dir          | (FW_L2_PTR?)            |
0x49 | bios_dir         | (BIOS_L2_PTR?)          |
0x4A | psp_dir          | (FW_L2_PTR?)            |
0x4C | fw               | (?)                     |
0x4D | fw               | (?)                     |
0x4E | signed_pubkey    | (PUBKEY?)               |
0x50 | keydb            | FW_KEYDB_BL             |
0x51 | keydb            | FW_KEYDB_TOS            |
0x52 |                  | FW_PSP_VERSTAGE         |
0x53 |                  | FW_VERSTAGE_SIG         |
0x54 |                  | RPMC_NVRAM              |
0x55 | fw               | (FW?)                   |
0x58 | fw               | FW_DMCU_ERAM            |
0x59 | fw               | FW_DMCU_ISR             |
0x5F |                  | FW_PSP_SMUSCS           |
0x73 |                  | FW_PSP_BOOTLOADER_AB    |
