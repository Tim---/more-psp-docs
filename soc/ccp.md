# CCP

The CCP is a cryptoprocessor that allows to do DMA and a bunch of crypto operations.

It is implemented in Linux in [/drivers/crypto/ccp/](https://github.com/torvalds/linux/tree/master/drivers/crypto/ccp).

The CCP has the following mapping:
  * `03000000-0300ffff`: CCP registers
