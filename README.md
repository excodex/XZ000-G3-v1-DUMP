
# TP-Link XZ000-G3 (EU1) Version 1.0 - Flash chip DUMP

About a year ago I ordered two TP-Link XZ000-G3 GPON terminal from [Senetic](https://www.senetic.net/). The first one I received was a hardware version 1.0 and the second one was 2.0. Later that year, I opened the device and noticed the unpopulated UART headers, also they kindly marked the pins order. So I decided to solder the 2.54mm pins on the board and when I connected my red USB-to-TTL (FT232R) to the pins, noticed there is no dataflow between my computer and the GPON terminal. I measured each pin with a multimeter and that confirmed there is barely any voltage on the TX or on the RX pins.

Fast forward today, I recently ordered this [CH341A/CH341B 24 25 Series EEPROM Flash USB Programmer Module](https://www.aliexpress.com/item/1005006005017028.html) from AliExpress and fortunately the chip on the board was a XM25QH128A, which had 8-pins, also the test clip from AliExpress had 8-pins. So I downloaded [AsProgrammer](https://github.com/nofeletru/UsbAsp-flash) from GitHub and read the flash memory, which I uploaded to this repository. 

## Hardware Specifications
- CPU: ECONET EN7521SCU 2107-BAFAL BCMS9KRH 05XC6016 1B80002
- Flash: XMC QH12BAH16 PPF28700 05 2114A
- Bosa Chip: ECONET EN7571N 2130BWAL ECMDJ6Y1

## Software Details
- Firmware Version: 3.1.4 build 220126 Rel.36878n

## Dump File Checksums
`TP-Link-XZ000-G3_EU1_v1.0_flash_dump.bin`
- MD5 checksum: 54d7dd66b882fd96c483fef908e2af7c
- SHA1 checksum: 7b15217de7583c184f6521fcce237395bc63dbdf

### AsProgrammer IC Read Results
```
Current programmer: CH341
Reading memory...
Done
Execution time: 0:03:22
CRC32 = 0x4629C331
```

### Binwalk result
```
DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
65536         0x10000         LZMA compressed data, properties: 0x5D, dictionary size: 8388608 bytes, uncompressed size: 204352 bytes
655616        0xA0100         LZMA compressed data, properties: 0x5D, dictionary size: 8388608 bytes, uncompressed size: 3775488 bytes
2031616       0x1F0000        Squashfs filesystem, little endian, version 4.0, compression:lzma, size: 2472539 bytes, 638 inodes, blocksize: 131072 bytes, created: 2022-01-26 02:15:13
8388864       0x800100        LZMA compressed data, properties: 0x5D, dictionary size: 8388608 bytes, uncompressed size: 3775488 bytes
9764864       0x950000        Squashfs filesystem, little endian, version 4.0, compression:lzma, size: 2472539 bytes, 638 inodes, blocksize: 131072 bytes, created: 2022-01-26 02:15:13
```

### Web Default Credentials (192.168.1.1)
**Admin user:**
  - Username: admin
  - Password: `admin`

**Regular user:**
  - Username: user
  - Password: `user`

### Shell Root Credentials (/etc/passwd)
- Username: admin
- Password: `1234`

Note: This is the default credentials for V2 as well.

```
$1$$iC.dUsGpxNNJGeOm1dFio/:1234

Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 500 (md5crypt, MD5 (Unix), Cisco-IOS $1$ (MD5))
Hash.Target......: $1$$iC.dUsGpxNNJGeOm1dFio/
Kernel.Feature...: Pure Kernel
Guess.Mask.......: ?1?2?2?2 [4]
Guess.Charset....: -1 ?l?d?u, -2 ?l?d, -3 ?l?d*!$@_, -4 Undefined
Guess.Queue......: 4/15 (26.67%)
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 576/2892672 (0.02%)
Rejected.........: 0/576 (0.00%)
Restore.Point....: 0/46656 (0.00%)
Restore.Sub.#2...: Salt:0 Amplifier:2-3 Iteration:0-1000
Candidate.Engine.: Device Generator
Candidates.#2....: 1ari -> 1nov
Hardware.Mon.SMC.: Fan0: 44%
Hardware.Mon.#2..: Temp: 55c
```
