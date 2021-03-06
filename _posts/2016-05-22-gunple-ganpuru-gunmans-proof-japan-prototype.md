---
layout: post
title: Ganpuru (Gunple) - Gunman's Proof (Japan) (Prototype)
date: 2016-05-22 20:00:00
slug: gunple-ganpuru-gunmans-proof-japan-prototype
category: Super Famicom
author: matthew_callis
download:
 title: Ganpuru (Gunple) - Gunman's Proof (Japan) (Prototype)
 filename: sfc/gunple-ganpuru-gunmans-proof-japan-prototype.7z
---

__[ガンプル Gunple - Gunman's Proof](https://superfamicom.org/info/ganpuru-strange-world-gunmans-proof)__

A super cute Zelda clone game with some really interesting debugging code that I can't seem to access. In game seems very much like the final. The part that is blanked out in the final is not blanked out here.

_Intro - Final_  / _Sample_

The intro window is a few pixels larger in the final version.

{% include compare_local.html
    name_1='Intro - Final'
    image_1='screenshots/gunple-japan/intro.png'
    name_2='Intro - Sample'
    image_2='screenshots/gunple-japan-prototype/intro.png'
%}

_Title - Final_  / _Sample_

Title is the same.

{% include compare_local.html
    name_1='Title - Final'
    image_1='screenshots/gunple-japan/title.png'
    name_2='Title - Sample'
    image_2='screenshots/gunple-japan-prototype/title.png'
%}

_Debug Mode / X-MODEM Code_

From `0x0000A8` - `0x000200` we see the same 1BPP font seen in later in this ROM and in the final version at `0x005000` - `0x005158`. Booting with the `0000` checksum seems to activate the X-Modem code and enters a waiting period.

![1BPP Font - Prototype]({% asset_path 'screenshots/gunple-japan-prototype/1bpp-font-1.png' %} "1BPP Font")
![1BPP Font - Prototype]({% asset_path 'screenshots/gunple-japan-prototype/1bpp-font-2.png' %} "1BPP Font")

The [weird Ln-MOS mode](https://tcrf.net/Gunman%27s_Proof), as seen on [The Cutting Room Floor](https://tcrf.net/), also works in the prototype:

![Ln-MOS 1 - Prototype]({% asset_path 'screenshots/gunple-japan-prototype/ln-mos-1.png' %} "Ln-MOS 1 - Prototype")
![Ln-MOS 2 - Prototype]({% asset_path 'screenshots/gunple-japan-prototype/ln-mos-2.png' %} "Ln-MOS 2 - Prototype")

There are some development and debugging strings in the binary that aren't in the final build.

```
.SEXTRA-00
** MONITOR SW **
COPY@OK@@@@TURN@SWITCH
LOAD@COMPLETE
PARAREL@INPUT@ MOTOROLA@9600@ MONITOR@9600@@ K
#d0dCdD

SUPER FAMICOM   DELUX MONITOR   version 0.27
command > 
    command err.

HELP LOCK SD VD 1MROM 4MROM
M ﾇｰDLS
EXIT 恙SYSTEM 恙GAME 恙RUN 恙RESET ユQUIT
BANK
nX-MODEM(128sum)

CASETTE@COPYING@
0123456789ABCDEF

edit %02x:%04x  %02x ->  hhhhhh

*a list of op codes*
```

This appears to be an `X-MODEM` debugging solution. The full strings via Google Translate:

1. "で受信を開始して下さい" -> "Start the reception in".
1. "準備が出来たなら黄色ボタンを押して下さい" -> "Press the yellow button if ready"
1. "ダウンロード終了" -> "Download Exit"
1. "モニターモードに固定しました｡" -> "It was fixed to the monitor mode."

```
X-MODEM(128sum)で受信を開始して下さい  bank=%02x
準備が出来たなら黄色ボタンを押して下さい 
hh
L� ﾟ｢ｩ �Vｩ�W徭� ｷV ｣ﾈﾐW0觜ｩ�Wﾎsﾐ鯰rﾐ�
譴 r拿n\a
**ダウンロード終了**
 Lｵ陶 Hｩ r拿a

X-MODEM(128sum)で受信を開始して下さい  bank=%02x
準備が出来たなら黄色ボタンを押して下さい 
hh
L� ﾟ｢ｩ �Vｩ �W� ｷV ｣ﾈﾐW･Wﾉ 栓
譴 r拿n\a
**ダウンロード終了**
 Lｵ� r拿a

X-MODEM(128sum)で受信を開始して下さい  sound_unit
準備が出来たなら黄色ボタンを押して下さい 
L� ﾟ｢ｩ �Vｩ �W�  ﾁ� ｣ﾈﾐWﾐ�
譴 r拿n\a
**ダウンロード終了**
 Lｵ� r拿a

X-MODEM(128sum)で受信を開始して下さい  video_ram
準備が出来たなら黄色ボタンを押して下さい 
L� ﾟ｢ｩ �Vｩ �W�   ｣ﾈﾐWﾐ�
譴 r拿n\a
**ダウンロード終了**
 Lｵ適ｫｭ�)ﾐｩﾍ�ﾐｩﾍ�ﾐｩ昨` r拿tモニターモードに固定しました｡ Kｫｩ柵ｩ窄Lｵ� r�
  ･････ good bye
 ｯB 0崧B 寘 柵窄Lф r�
    EXIT ･･････ end debuger for game  
    DUMP ･･････                       
    FILE ･･････ backup file display   
         ･･････                       
         ･･････                        
;adrs    +1  +2  +3  +4  +5  +6  +7  +8  +9  +A  +B  +C  +D  +E  +F  r�
```

In the `SRAM`:

```
Wiz497
```

_ROM Info_

```
---------------------Internal ROM Info----------------------
       File: Gunple (Japan) (Sample).sfc
       Name: GUNPLE                   Company: ASCII Co./Nexoft
     Header: None                        Bank: LoROM
Interleaved: None                        SRAM: 64 Kb
       Type: Normal + Batt                ROM: 24 Mb
    Country: Japan                      Video: NTSC
  ROM Speed: 120ns (FastROM)         Revision: 1.0
   Checksum: Good 0x2F71            Game Code: AXAJ
---------------------------Hashes---------------------------
      CRC32: 72FEB165
        MD5: 209D36AC912D60EE71E0D8492016C7F4
      SHA-1: CB753DA21F0E98D16EE282D2E9029B907534BDF1
--------------------------Database--------------------------
    ROM wasn't found in the database (possible bad dump).

---------------------Internal ROM Info----------------------
       File: Gunple (Japan).sfc
       Name: GUNPLE                   Company: ASCII Co./Nexoft
     Header: None                        Bank: LoROM
Interleaved: None                        SRAM: 64 Kb
       Type: Normal + Batt                ROM: 24 Mb
    Country: Japan                      Video: NTSC
  ROM Speed: 120ns (FastROM)         Revision: 1.0
   Checksum: Good 0x110D            Game Code: AXAJ
---------------------------Hashes---------------------------
      CRC32: AF415C24
        MD5: C79CA7C76D169FD42524FA7DBA2317F7
      SHA-1: DAD73D2C0B1A3C916D40C4A208566EE4193333B2
--------------------------Database--------------------------
       Name: Ganpuru - Gunman's Proof
    Country: Japan                   Revision: 1.0
     Port 1: Gamepad                   Port 2: Gamepad
    Genre 1: RPG                      Genre 2: Unknown
```

If you happen to know the game well and find more differences, or can translate any of the screen shots above- [please update this post on GitHub](https://github.com/MatthewCallis/eludevisibility.org) or contact me!

[Article on SNESCentral.](http://www.snescentral.com/article.php?id=1035)

PCB Scans coming soon!
