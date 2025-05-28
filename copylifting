# RFID-toolkit

Set of tools needed to interact with RFID tags over arduino

# Basic info about Mifare Clasic 1k

## Memory layout

![Mem layout](https://firefart.at/img/mifare/mifare_memory_layout_thumb.png)

## Keys
```

Each sector of a MIFARE Classic card has two authentication keys: key A and key B. These two keys together with access conditions are stored in the last block of each sector (the so-called sector trailer). The sector trailer looks like this:

+-----------------------------+--------------+----+-----------------------------+
|  0 |  1 |  2 |  3 |  4 |  5 |  6 |  7 |  8 |  9 | 10 | 11 | 12 | 13 | 14 | 15 |
+-----------------------------+--------------+----+-----------------------------+
|            Key A            | Access Conditions |            Key B            |
|          (6 bytes)          |     (4 bytes)     |          (6 bytes)          |
+-----------------------------+--------------+----+-----------------------------+
The access conditions define how you can access the blocks in the sector:

the commands you can issue after authenticating with key A (read, write, value block operations),
the commands you can issue after authenticating with key B (read, write, value block operations),
if key B is used as an authentication key at all.
Typical scenarios are:

Authentication is only possible with key A. Key A has read-only access.
Authentication is only possible with key A. Key A has read/write access.
Authentication is possible with both keys. Key A has read-only access. Key B has read/write access.
Authentication is possible with both keys. Key A and B have read-only access.
You can find a full description of the possible access conditions in the MIFARE datasheet.

```
from http://stackoverflow.com/a/28051227


## Default keys list

```
ffffffffffff
a0b0c0d0e0f0
a1b1c1d1e1f1
a0a1a2a3a4a5 
b0b1b2b3b4b5
4d3a99c351dd 
1a982c7e459a
000000000000
aabbccddeeff
d3f7d3f7d3f7
aabbccddeeff
714c5c886e97
587ee5f9350f
a0478cc39091
533cb6c723f6
8fd0a4f256e9
```

## Game rules

```
 * MIFARE Classic 1K (MF1S503x):
 * 		Has 16 sectors * 4 blocks/sector * 16 bytes/block = 1024 bytes.
 * 		The blocks are numbered 0-63.
 * 		Block 3 in each sector is the Sector Trailer. See http://www.mouser.com/ds/2/302/MF1S503x-89574.pdf sections 8.6 and 8.7:
 * 				Bytes 0-5:   Key A
 * 				Bytes 6-8:   Access Bits
 * 				Bytes 9:     User data
 * 				Bytes 10-15: Key B (or user data)
 * 		Block 0 is read-only manufacturer data.
 * 		To access a block, an authentication using a key from the block's sector must be performed first.
 * 		Example: To read from block 10, first authenticate using a key from sector 3 (blocks 8-11).
 * 		All keys are set to FFFFFFFFFFFFh at chip delivery.
 * 		Warning: Please read section 8.7 "Memory Access". It includes this text: if the PICC detects a format violation the whole sector is irreversibly blocked.
 *		To use a block in "value block" mode (for Increment/Decrement operations) you need to change the sector trailer. Use PICC_SetAccessBits() to calculate the bit patterns.

```
, from https://github.com/miguelbalboa/rfid/blob/master/MFRC522.h


## References

* [A Practical Attack on the MIFARE Classic](http://arxiv.org/pdf/0803.2285.pdf)
* [How to Crack Mifare Classic Cards](https://firefart.at/post/how-to-crack-mifare-classic-cards/)
* [BlackHat 2014 - Hacking Mifare Classic Cards](https://www.blackhat.com/docs/sp-14/materials/arsenal/sp-14-Almeida-Hacking-MIFARE-Classic-Cards-Slides.pdf)
* [mfoc](https://github.com/nfc-tools/mfoc.git)
* [MIFARE Classic 1K - Mainstream contactless](http://www.mouser.com/ds/2/302/MF1S503x-89574.pdf)
* [Cloning a MiFare classic 1k tag](https://pmo.io/blog/cloning-a-mifare-tag.html)
* [Arduino MFRC522](http://www.nxp.com/documents/data_sheet/MFRC522.pdf)
