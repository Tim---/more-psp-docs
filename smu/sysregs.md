# SMU sysregs

Note: this specific to Summit processors.

## Public sysregs

| offset  | type          | name                 |
| ------- | ------------- | -------------------- |
| `0x000` | pub_misc_t    | pub_misc             | 
| `0x5xx` | *             | other_mbs            | 
| `0x7xx` | *             | psp_mb               | 
| `0x780` | u32           | ?                    | 
| `0x784` | u32           | ?                    | 
| `0xb08` | u32           | ?                    | 

pub_misc_t:

| offset | type          | name                 |
| ------ | ------------- | -------------------- |
| `0x04` | u32           | ?                    | 
| `0x14` | u32           | ?                    | 
| `0x34` | u32           | smu_is_ready         | 
| `0x48` | u32           | smu_fw_version       | 
| `0x4c` | u32           | ?                    | 
| `0x50` | u32           | ?                    | 
| `0x54` | u32           | ?                    | 
| `0x58` | u64           | ticks                | 

The following regions are masked when accessed from SMN:

| start   | end          | name                 |
| ------- | ------------ | -------------------- |
| `0x000` | `0x02f`      | ?                    | 
| `0x058` | `0x05f`      | ticks                | 
| `0x200` | `0x21f`      | small_intc           | 
| `0x300` | `0x3c7`      | big_intc             | 
| `0x600` | `0x60f`      | ?                    | 
| `0x700` | `0x717`      | psp_mb               | 

## Private sysregs

| offset  | type          | name                 |
| ------- | ------------- | -------------------- |
| `0x000` | priv_misc_t   | ?                    | 
| `0x200` | small_intc_t  | ?                    | 
| `0x300` | big_intc_t    | ?                    | 
| `0x400` | timer_t[8]    | ?                    | 
| `0x900` | u32[4]        | ?                    | 
| `0x914` | u32           | ?                    | 
| `0x918` | u32           | ?                    | 

priv_misc_t:

| offset | type          | name                 |
| ------ | ------------- | -------------------- |
| `0x00` | u32           | ?                    | 
| `0x04` | u32           | ?                    | 
| `0x08` | u32           | ?                    | 
| `0x14` | u32           | ?                    | 
| `0x1c` | u32           | ?                    | 
| `0x20` | u32           | ?                    | 
| `0x60` | u32           | smu_fw_version       | 
| `0x64` | u32           | ?                    | 
| `0x74` | u32           | ?                    | 
| `0x78` | u32           | ?                    | 
| `0x88` | u32           | ?                    | 
