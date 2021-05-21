# Asus chromebook c100 flip hardware

Similar devices: chromebook veyron veyron_pinky - they share same CPU rk3288 but can have different peripherals (bt, screen etc)

## CPU:   
rockchip rk3288 arm7 armhf.   
 

https://rockchip.fr/RK3288%20TRM/

Mainline kernel status:  
http://opensource.rock-chips.com/wiki_Status_Matrix

Rockchip proprietary kernel tree:  
https://github.com/rockchip-linux
 


##WiFi

Original drivers Cypress/Broadcom drivers (registration needed):    
https://www.cypress.com/documentation/software-and-drivers-archive/wifi-bt-linux-archive


     Broadcom BCM4354 sdio     
     CONFIG_WLAN_VENDOR_BROADCOM=y    
     CONFIG_BRCMUTIL=m  
     CONFIG_BRCMFMAC_PROTO_BCDC=y  
     CONFIG_BRCMFMAC_SDIO=y  

modules:  


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


##Bluetooth
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













