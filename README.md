# W65C265SXB EhBASIC
This repository contains a port of the 65C02 version of EhBasic which will run on a WDC W65C265SXB board from the flash ROM in the CPU's emulation mode.

A compiled binary image of the interpreter and the S28 for my SXB-Hacker program are included but you will also need:
- A W65C265SXB which has a Flash memory chip installed.
- A copy of TeraTerm or a similar terminal application with XMODEM support.

## Installing the Image
Boot the W65C265SXB and load the SXB-Hacker (in tools/sxb-hacker.s28) using TeraTerm's send file command ('File > Send File...'). When it is loaded start it with the command 'G000300'.
```
>S  .0001.0002.0003.0004.0005.0006.0007.0008.0009.0010.0011.0012.0013.0014.0015.
0016.0017.0018.0019.0020.0021.0022.0023.0024.0025.0026.0027.0028.0029.0030.0031.
0032.0033.0034.0035.0036.0037.0038.0039.0040.0041.0042.0043.0044.0045.0046.0047.
0048.0049.0050.0051.0052.0053.0054.0055.0056.0057.0058.0059.0060.0061.0062.0063.
0064.0065.0066.0067.0068.0069.0070.0071.0072.0073.0074.0075.0076.0077.0078.0079.
0080.0081.0082.0083.0084.0085.0086.0087.0088.0089.0090.0091.0092.0093.0094.0095.
0096.0097.0098.0099.0100.0101.0102.0103.0104.0105.0106.0107.0108.0109.0110.0111.
0112.0113.0114.0115.0116.0117.0118.0119.0120.0121.0122.0123.0124.0125.0126.0127.
0128.0129.0130.0131.0132.0133.0134.0135.0136.0137.0138.0139.0140.0141.0142.0143.
0144.0145.0146.0147.0148.0149.0150.0151.0152.0153.0154.0155.0156.0157.0158.0159.
0160.0161.0162.0163.0164.0165.0166.0167.0168.0169.0170.0171.0172.0173.0174.0175.
0176.0177.0178.0179.0180.0181.0182.0183.0184.0185.0186.0187.0188.0189.0190.0191.
0192.0193.0194.0195.0196.0197.0198.0199.0200.0201.0202.0203.0204.0205.0206.0207.
0208.0209.0210.0211.0212.0213.0214.0215.0216.0217.0218.0219.0220.0221.0222.0223.
0224.0225.0226.0227.0228.0229.0230
READY
>g
Enter Address  BB:AAAA 00:0300

W65C265SXB-Hacker [18.06]
.
```
Erase the ROM area with the 'E' command and start an XMODEM download to install the BASIC image with the command 'X 8000'. The start a XMODEM transfer of the 'basic.bin' file in TeraTerm ('File > Transfer > XMODEM > Send...')
```
.E
.X 8000
Waiting for XMODEM transfer to start

.
```
You can check that it has been written using the display memory command. 
```
.M 8000 807f
00:8000 58 58 58 00 78 D8 38 FB 4C 2B 80 AD 48 DF 29 40 |XXX.x.8.L+..H.)@|
00:8010 18 F0 04 AD 77 DF 38 60 48 AD 48 DF 29 80 F0 F9 |....w.8`H.H.)...|
00:8020 68 8D 77 DF 60 60 60 00 EA 80 FC A0 0E B9 05 A0 |h.w.```.........|
00:8030 99 7F 04 88 10 F7 A2 FF 86 3A 9A A9 4C 85 53 A2 |.........:..L.S.|
00:8040 0B BD 14 A0 95 00 CA 10 F8 64 64 64 19 A9 0E 85 |.........ddd....|
00:8050 16 A9 03 85 52 A2 1A 86 17 A9 00 92 0A E6 0A D0 |....R...........|
00:8060 08 E6 0B A5 0B C9 80 F0 0F A9 55 92 0A D2 0A D0 |..........U.....|
00:8070 07 0A 92 0A D2 0A F0 E1 A5 0A A4 0B 85 37 84 38 |.............7.8|
```
## Running EhBASIC
Press the reset button on the W65C265SXB the enter the command 'G008004'. You should see this:
```
>G
Enter Address  BB:AAAA 00:8004
30719 Bytes free

Ready
```
## Rebuilding EhBASIC
I've included a JAR file containing my Dev65 assembler, some include files defining the W65C265's registers and the batch file to rebuild the ROM if you make changes to it.

If the first three bytes of the ROM are changed from 'XXX' to 'WDC' then the ROM will start automatically when the system is powered on or reset.

> The minimal code I provided needs to be extended to initialise the UART properly or you will be locked out of your SXB.

Have fun!