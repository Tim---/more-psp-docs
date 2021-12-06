# PSP versions

The PSP was introduced starting with the AMD Excavator microarchitecture. Since then, there have been several versions (~1 per microarchitecture).

Different PSP versions are not compatible, thus the "BIOS ROM" contains the code for each version supported by the motherboard. The on-chip bootloader selects the binaries that correspond to its major-minor version.

PSP have a version in 4 bytes:
  * **magic**: always 0xbc
  * **major**: probably incremented for each microarchitecture
  * **minor**: version within a microarchitecture
  * **revision**: mostly ignored

The precise mappings between CPU model and PSP version is not known.
To understand it we can either:

  * dump the PSP register containing the version if we get code execution on the PSP ;
  * list the versions supported in different revisions of a motherboard BIOS ;
  * find a way to dump the PSP version from the OS ;
  * ask AMD.

## Known PSP versions

According to PSPEmu:

| Generation    | Version code  |
| ------------- | ------------- |
| Zen           | 0xbc090072    |
| Zen+          | 0xbc090072    |
| Zen2          | 0xbc0b0552    |
| Zen3          | 0xbc0c0100    |

(this looks weird since 0xbc0axxxx doesn't appear. Zen+ ?)

## Crypto material

Each PSP version uses different pubkey and wrapped IKEK.

Version  | pubkey                           | wrapped IKEK
---------| -------------------------------- | -------------------------------- |
-        | c25d8c5591a44f26bf74f09f4813cbdd | -
bc090000 | 1bb987c359494606b174945601c9ea5b | 50d00f3cbcb8f1945a7daa872224107b
bc0a0000 | 60bba67e1a434c6b9807bc8dfdb41f40 | 2ef9a17d93ae1b7307845b22b2883dc2
bc0a0100 | 60bba67e1a434c6b9807bc8dfdb41f40 | 2ef9a17d93ae1b7307845b22b2883dc2
bc0b0500 | fd90b04b797743c6a9c94bd11b10543e | 059bef4a60354f2312cccf5c4b203556
bc0c0000 | 144ed093dc644601a15c81d71a8b4fb4 | 79f6e5acf43697db356b32dcbd15d69f
bc0c0140 | 6c9ea31abe17472797c9f06fe416ade2 | 04c54d0efa5b75b2aab329f50d70ea0a

## Zen series

For information: 

Gen   | Desktop               | Threadripper       |  APU                | Laptop          | server
----- | --------------------- | ------------------ | ------------------- | --------------- | -------------
Zen   | Summit Ridge   (1000) | Whitehaven  (1000) |  Raven Ridge (2000) |                 | Naples (Epyc)
Zen+  | Pinnacle Ridge (2000) | Colfax      (2000) |  Picasso     (3000) |                 |
Zen2  | Matisse        (3000) | Castle Peak (3000) |  Renoir      (4000) | Lucienne (5000) | Rome   (Epyc)
Zen3  | Vermeer        (5000) |                    |                     | Cezanne  (5000) | Milan  (Epyc)
Zen4  | Warhol         (????) |                    |  Rembrandt   (????) |                 | Genoa  (Epyc)
