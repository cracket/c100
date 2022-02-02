# Asus chromebook c100 flip hardware

Similar devices: chromebook veyron veyron_pinky - they share same CPU rk3288 but can have different peripherals (bt, screen etc)


#### Documentation
https://rockchip.fr/RK3288%20TRM/

#### Kernel
Mainline kernel status:  
http://opensource.rock-chips.com/wiki_Status_Matrix

Rockchip proprietary kernel tree:  
https://github.com/rockchip-linux



## CPU   
rockchip rk3288 arm7 armhf.   

 


## PLATFORM

#### PWM

See https://rockchip.fr/RK3288%20TRM/rk3288-chapter-51-pulse-width-modulation-(pwm).pdf

 
#### ADC - SARADC, TSADC

* Temperature Sensor(TS-ADC)

    3 bipolar-based temperature-sensing cell embedded
    3-channel 12-bits SAR ADC
    Temperature accuracy sensed is ±5 degree
    SAR-ADC clock must be less than 50KHz  
    Power Down Current is about 1uA for anolog and 2uA for digital logic
* SAR-ADC(Successive Approximation Register) 

3-channel single-ended 10-bit SAR analog-to-digital converter
Conversion speed range is up to 1 MSPS
SAR-ADC clock must be less than 1MHz
DNL is less than ±1 LSB , INL is   less than ±2.0 LSB
Power down current is about 0.5uA for analog and digital logic
Power supply is 1.8V (±10%) for analog interface

See https://rockchip.fr/RK3288%20TRM/rk3288-chapter-45-sar-adc.pdf

See https://rockchip.fr/RK3288%20TRM/rk3288-chapter-46-temperature-sensor-adc(ts-adc).pdf

#### WATCHDOG

* 32 bits watchdog counter width
* Counter clock is from apb bus clock
* Counter counts down from a preset value to 0 to indicate the occurrence of a timeout 
* WDT can perform two types of operations when timeout occurs:Generate a system reset, First generate an interrupt and if this is not cleared by the service routine by the time a second timeout occurs then generate a system reset
* Programmable reset pulse length
* Totally 16 defined-ranges of main timeout period

See https://rockchip.fr/RK3288%20TRM/rk3288-chapter-50-watchdog.pdf


#### EFUSE

* Two high-density electrical Fuse is integrated: 256bits (32x8) / 1024bits (32x32)
* Support standby mode

#### TIMER

See https://rockchip.fr/RK3288%20TRM/rk3288-chapter-47-timer.pdf


#### Unused 
GPS  
MIPI-CSI, 
ISP 


## GPU & DISPLAY


#### 3D ENGINE 
* High performance OpenGL ES1.1/2.0/3.0, OpenCL 1.1, DirectX 11 etc.
* Embedded 4 shader cores with shared hierarchical tiler
* Provide MMU and L2 Cache with 256KB size
* Image quality using double-precision FP64, and anti-aliasing



#### 2D ENGINE  (RGA)

See https://rockchip.fr/RK3288%20TRM/rk3288-chapter-28-rga2.pdf

#### IEP - Image Enhancement Processor

See https://rockchip.fr/RK3288%20TRM/rk3288-chapter-29-image-enhancement-processor-(iep).pdf


#### Video Codec

###### Video Decoder 

* Real-time video decoder of MPEG-1, MPEG-2, MPEG-4, H.263, H.264, AVS, VC-1, RV, VP6/VP8, Sorenson Spark, MVC 

###### Video Encoder

* Support video encoder for H.264 (BP@level4.0, MP@level4.0, HP@level4.0), MVC and VP8
* Only support I and P slices, not B slices

See https://rockchip.fr/RK3288%20TRM/rk3288-chapter-25-video-encoder-decoder-unit-(vcodec).pdf

#### IEP - Image Enhancement
* Image pre-processor for Video Encoder
* Video stabilization (for Video Encoder)
* Image post-processor (for Video Decoder and JPEG codec)
* Image enhancement processor


#### HEVC Decoder

* Main/Main10 HEVC/H.265 decoderof 4k@60FPS
* Support up to 4096x2304 resolution
* Support up to 100Mbps bit rate 
* Embedded memory management unit(MMU) 
* Stream error detector (28 IDs) 
* Internal 128k cache for bandwidth reduction
* Multi-clock domains and auto clock-gating design for power saving


#### VPU JPEG Codec

#### VOP DRM Display


###### eDP


###### HDMI
Up to 1080p at 120 Hz and 4k x 2k at 60 Hz HDTV display resolutions and up to QXGA graphic display resolutions



## BUS DEVICES

#### SD/SDIO/MMC BUS
SD3.0 4bit  eMMC 4.5

#### I2S BUS


See https://rockchip.fr/RK3288%20TRM/rk3288-chapter-16-i2s-pcm-controller-(8-channel).pdf

#### I2C BUS
* pmic 
* tpm 
* max98090?
* elants_i2c
* ekth3000
* ts3a227e
* bq27500


#### SPI BUS
* spi-nor memory


#### USB BUS
* UART
* Camera



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













