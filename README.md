# Arm9LoaderHax for Nintendo 3DS

## 說明

這是我個人對於arm9loaderhax利用方式的進展, 您可以在這查閱相關文件 [here](http://3dbrew.org/wiki/3DS_System_Flaws) 另外我也推荐看看 [in this conference](https://media.ccc.de/v/32c3-7240-console_hacking), 利用了 9.6 以上版本 New3DS arm9loader 的漏洞 , 使得 ARM9 的代碼能夠在開機的時候直接運行.

這個項目在 New 與 OLD 3DS 都已確認運行.

這個接入口是由 **plutoo** 與 **yellows8** 發現的 , 我並不擁有這個想法 , 只是對這個項目有些微的進展.

Screen_init 是由 [**dark-samus** pull request](https://github.com/delebile/arm9loaderhax/pull/9) 所研擬的 (萬分感謝!).

## 使用

一旦您安裝了這個接入口 , 他將會在您開機的時候運行 SD 卡根目錄下的 **arm9loaderhax.bin** 文件.

如果找不到這個文件, 主機就會直接切斷電源.


## 安裝

編譯完成之後在您的 **data_output** 資料夾內會有以下三個檔案:

* arm9loaderhax.3dsx
* arm9loaderhax.bin
* arm9loaderhax.pack

*.pack* 檔案包含了所有將安裝的數據 (如果只有一個文件的話, 那麼專屬於您主機的數據也將被包含), 必須將這個文件放置於 SD 卡的根目錄.

*.bin* 是個可被 Brahma2, CakeHax, Arm9LoaderHax 本身 (主要是更新接入點), 等等的方式運行的獨立 payload .
這是一個安裝用的程序, 只要您找到了一個方法可以運行他之後, 您就只需要按照指示運行即可.

*.3dsx* 是個可在 9.2 以下的固件由 Homebrew Launcher 運行的預先編譯好的 Brahma2 3dsx .
這是一個 *.bin* 文件的加載器, *.bin*文件已被包含在 3dsx 內.

## 軟體更新

當有些程序上的優化被釋出的時候, 您將可以使用本安裝器來更新將來所釋出的  *.pack* 檔案.


## 配置
####**需要的文件**
有些必要的文件必須被配置好, 請確保以下的文件都被放到了 **data_input** 資料夾內, 你將必須自己去找到他們:

| Name          | Description           | SHA-256  |
| ------------- |---------------| ------|
| **new3ds10.firm**|系統版本 10.2 的 New3DS NATIVE_FIRM.| d253c1cc0a5ffac6b383dac1827cfb3b2d3d566c6a1a8e5254e389c2950623e5 |
| **new3ds90.firm**|系統版本 9.0 的 New3DS NATIVE_FIRM.|d7be76e1813f398dcea85572d0c058f7954761a1d5ea03b5eb5047ac63ac5d6b |
|**secret_sector.bin**|New 3DS 的秘密 0x96 秘鑰扇區.|    82f2730d2c2da3f30165f987fdccac5cbab24b4e5f65c981cd7be6f438e6d9d3 |
|**otp.bin**|從您的機器內區域 0x10012000-0x10012100 所導出的 OTP 數據. 如果使用其他機器的 OTP 會使你的機器變磚.|     |

####**環境需求**

* devkitARM r45
* libctru (ver. 1.0.0)
* Python with PyCcrypto (2.7 or 3.x should work)
* GCC or MinGW (Only needed to compile the buildt-in tool, you can download [a pre-compiled windows build here](https://mega.nz/#!j0RkxLjb!4Am-3yDAR9g4VDxY93pWhXVYNDiylSW1cKJntOLfDWU), place it in **common** folder)

####**編譯選項**

* **make** : 本指令會生成所有文件
* **make hax** : 本指令會跳過 3DSX 安裝器的編譯
* **make stage2_update** : 本指令只會生成次要的 payload, 主要用來更新接入點文件.

## Credits

*Copyright 2016, Jason Dellaluce*


*Licensed under GPLv2 or any later version, refer to the license.txt file included.*

* Smealum and contributors for libctru
* Normmatt for sdmmc.c and .h, and also for .ld files and the log from XDS by ichfly that provided us some of the information needed to get screen init
* Christophe Devine for the SHA codes
* Archshift for i2c.c and .h
* Megazig for crypto.c and .h
* Patois for original BRAHMA code
* Smealum, Derrek, Plutoo for publishing the exploit
* Yellows8 and Plutoo as ideators of it
* [3dbrew community](http://3dbrew.org/)
* bilis/b1l1s for his screen init code, and work on inegrating it into stage 2
* dark_samus for work on integrating screen init into stage 2
