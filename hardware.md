# Asus chromebook c100 flip hardware

Similar devices: chromebook veyron veyron_pinky - they share same CPU rk3288 but can have different peripherals (bt, screen etc)

## CPU FEATURS:   

rockchip rk3288 arm7 armhf - see  https://rockchip.fr/RK3288%20TRM/  and https://rockchip.fr/RK3288%20datasheet%20V2.4.pdf  


#### Documentation
https://rockchip.fr/RK3288%20TRM/

Hardware specs relevant for linux kernel:
#### Kernel
Mainline kernel status:  
http://opensource.rock-chips.com/wiki_Status_Matrix
Rockchip proprietary kernel tree:  
https://github.com/rockchip-linux

## PLATFORM
1.1.4 External Memory or storage  
- Nand Flash
- eMMC
- SD/MMC ver 4.5 

1.1.5 System Component
- PMU 
- Watchdog   (Synopsys DesignWare Watchdog dw_wdt)
- Bus AXI/AHB/APB    (AMBA5 ?)
- DMAC   (PL330 DMAC-241330)
- crypto:
    - Support AES-128/192/256 with ECB, CBC, OFB, CTR, CBC-MAC, CMAC, XCBC-MAC, XTS and CCM modes
    - Supports SHA-1, SHA-256 and SHA-512 modes, as well as HMAC
- Trustzone technology support
- Internal on-chip memory:
    - 20KB BootRom
    - 100KB internal SRAM for security and non-security access, detailed size is programmable
- CPU up to 2.2GHz      (freq scaling)
    
1.1.6 Video Codec
- decoder:  H264  4K/24fps HighProfile 5.2,  MPEG4 HD/60fps  (0xff660000 ?)
- encoder:  H264  HD/30fps   (Hantro H1  hantro-vpu)

1.1.7 HEVC Decoder
- H265 4K/60fps

1.1.8 JPEG Codec
- decoder/encoder 8K

1.1.10 Graphics Engine
- 3D High performance OpenGL ES1.1/2.0/3.0, OpenCL 1.1, DirectX 11
- 2D BitBlit 8K

1.1.12 HDMI
- HDMI TX 2.0,   4K@60Hz, 10-bit Deep Color  (DesignWare HDMI  dwhdmi-rockchip)

1.1.17 Connectivity
- Uart controller (bluetooth hci)
- USB Host 2.0

1.1.18 Others
- eFuse 256bits (32x8) and 1024bits (32x32)

8.1 Core system
- PL301 interconnect
- GIC400 interrupt controller

Watchdog: dw_wdt


## WiFi

Original drivers Cypress/Broadcom drivers (registration needed):    
https://www.cypress.com/documentation/software-and-drivers-archive/wifi-bt-linux-archive


     Broadcom BCM4354 sdio     
     CONFIG_WLAN_VENDOR_BROADCOM=y    
     CONFIG_BRCMUTIL=m  
     CONFIG_BRCMFMAC_PROTO_BCDC=y  
     CONFIG_BRCMFMAC_SDIO=y  

modules:  



## BUS DEVICES

#### SD/SDIO/MMC BUS
SD3.0 4bit  eMMC 4.5
mmc0: flash 16 MB HAG2e
mmc1: SDR104 SDIO 148MHz (microSD card)
mmc2: SDR104 SDIO 148MHz (Brodacom Wifi)

#### I2S BUS
max98090



See https://rockchip.fr/RK3288%20TRM/rk3288-chapter-16-i2s-pcm-controller-(8-channel).pdf

#### I2C BUSes
rk3x-i2c
* i2c-0 rk808 pmic + rtc0
* i2c-1 tpm_i2c_infineon (tpm)
* i2c-2 max98090 (sound card)
* i2c-3 elants_i2c (touchscreen)
* i2c-4 ekth3000 (touchpad)
* i2c-4 ts3a227e (headphones jack detector)

cros-ec-i2c-tunel (via spi0) 
* i2c-20 bq27500 (battery)

rockchip-dp (eDP)
* i2c-21 DP-AUX

rk3288-dw-hdmi (HDMI)
* i2c-22 DesignWare HDMI (ddc)

#### SPI BUS
* spi0.0 - Embedded Controller (EC) - keyboard 
* spi2.0 - spi-nor memory (mtd0) 4MB gigadevice gd25q32 (coreboot)


#### USB BUS
* EHCI USB Hub
* Camera  13d3:5662 IMC Networks USB2.0 HD UVC WebCam



#### kali blob
NVRam Rev: 373428  
3062 bytes  
https://gitlab.com/kalilinux/build-scripts/kali-arm/-/blob/master/bsp/firmware/veyron/brcmfmac4354-sdio.txt

Bin  4354a1-roml/sdio-ag-p2p-pno-aoe-pktfilter-keepalive-sr-mchan-proptxstatus-ampduhostreorder-lpc-wl11u-txbf-pktctx-okc-tdls-mfp Version: 7.35.79.57 CRC: fb9f1833 Date: Wed 2015-02-11 14:09:23 PST Ucode Ver: 963.3013 FWID: 01-56a4670c  
605388 bytes  
https://gitlab.com/kalilinux/build-scripts/kali-arm/-/blob/master/bsp/firmware/veyron/brcmfmac4354-sdio.bin


#### chromiumos blob
NVRam Rev: 373428  
3062 bytes  
URL not available (but same as in kali)

Bin   4354a1-roml/sdio-ag-p2p-pno-aoe-pktfilter-keepalive-sr-mchan-proptxstatus-ampduhostreorder-lpc-wl11u-txbf-pktctx-okc-tdls-mfp Version: 7.81.3 (r720286) CRC: dd23fbd8 Date: Fri 2017-09-08 03:13:12 PDT Ucode Ver: 963.316 FWID: 01-3c2554cb  
603662 bytes  
URL not available

BCM4354_003.001.012.0443.1505.hcd  
BCM4354 UART 37.4 MHz wlbga_54z_iLNA  
81417 bytes  


## Bluetooth
The key to set up bluetooth are exotic kernel options/modules for hci serial AND dtb from chromium os
(mainline dtb sucks, mainline kernel  sources5.x is OK)  

DTB file:  

    Type:         Flat Device Tree  
    Compression:  uncompressed  
    Data Size:    52193 Bytes = 50.97 KiB = 0.05 MiB  
    Architecture: ARM  
    Hash algo:    sha1  
    Hash value:   377ed6d98e7bc70422a4949e073ce9e68d4571b6  

Kernel config source  
https://unix.stackexchange.com/questions/498473/why-is-bluetooth-not-working-on-my-chromebook-arch-linux-arm  


    CONFIG_BT=m  
    CONFIG_BT_BCM=m  
    CONFIG_BT_HCIUART=m  
    CONFIG_BT_HCIUART_SERDEV=y  
    CONFIG_BT_HCIUART_H4=y  
    CONFIG_BT_HCIUART_3WIRE=y  
    CONFIG_BT_HCIUART_BCM=y  
    CONFIG_SERIAL_DEV_BUS=y  
    CONFIG_SERIAL_DEV_CTRL_TTYPORT=y  


NO FIRMWARE NEEDED! Just firmware for wifi (bin+nvram) from kali
Radio FM and GPS from BCM4354 is not supported



## Touchpad & Touchscreen
Elan touchpad&touchscreen I2S

## Camera
USB Camera  


## TPM
Infineon I2C




Mainline kernel status:  
http://opensource.rock-chips.com/wiki_Status_Matrix







