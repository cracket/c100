## Asus Chromebook c100 flip veyron - linux 5.x video hardware drivers with mainline kernel

Official specs  
• Quad-core ARM Mali-T760 MP4 GPU  
• clocked at 650 MHz  
• supporting OpenGL ES 1.1/2.0/3.0/3.1  
• OpenCL 1.1  
• Renderscript  
• Direct3D 11.1  
• 1080P video encoding for H.264 and VP8, MVC  
• 4K H.264 and 10bits H.265 video decode, 1080P multi video decode (MPP)  
• Supports 4Kx2K H.265 resolution  
• Up to 3840x2160 display output, HDMI 2.0


###### Video components status  

|feature | rockchip name / kernel driver | kernel status | userspace driver | userspace status |  
| :--- | ---- | ---| ----| ---|
|Internal display 1280x800 | VOP: panfrost,  | OK | x11/wayland ?| ?|
| 2D acceleration | RGA2 | OK | V4L2 ? | ? |
| 3D acceleration | panfrost kernel driver   kmssink  etc          mali-midgard&nbsp;dkms(legacy)  | OK |  mesa (buggy) | ? |
| video acceleration (x264,hevc etc..) | Rockchip VDEC(rkvdec)-4K h264 dec only  / Hantro H1 co-dec | OK | vaapi / V4L2 | ?|
| HDMI video out | ? |  ?| ? | ? |
| HDMI cec | ? |  ? | ? | ? | 
| rk video enhancement |IEP |? |?|?| 



#### Kernel config

###### Panfrost Mali driver (3D acceleration only)

CONFIG_DRM_ROCKCHIP  
CONFIG_DRM_DW_HDMI_CEC  

###### RGA/RGA2 (2D acceleration)
CONFIG_VIDEO_ROCKCHIP_RGA

###### h264/hevc codec / hantro codec

CONFIG_RK_VCODEC -->   CONFIG_VIDEO_ROCKCHIP_VDEC (rockchip kernel?)
CONFIG_STAGING  
CONFIG_STAGING_MEDIA  
CONFIG_VIDEO_HANTRO  
CONFIG_VIDEO_HANTRO_ROCKCHIP  

rkvdec.ko
drivers/staging/  rockchip-vdec.ko

#### Test


    panfrost ffa30000.gpu: clock rate = 400000000
    panfrost ffa30000.gpu: [drm:panfrost_devfreq_init] *ERROR* Couldn't set OPP regulators
    panfrost ffa30000.gpu: clock rate = 400000000
    panfrost ffa30000.gpu: mali-t760 id 0x750 major 0x0 minor 0x0 status 0x1
    panfrost ffa30000.gpu: features: 00000000,100277bf, issues: 00000000,24040400
    panfrost ffa30000.gpu: Features: L2:0x07120206 Shader:0x00000000 Tiler:0x00000809 Mem:0x1 MMU:0x00002830 AS:0xff JS:0x7
    panfrost ffa30000.gpu: shader_present=0xf l2_present=0x1
    [drm] Initialized panfrost 1.1.0 20180908 for ffa30000.gpu on minor 2


    dwhdmi-rockchip ff980000.hdmi: Detected HDMI TX controller v2.00a with HDCP (DWC MHL PHY)
    dwhdmi-rockchip ff980000.hdmi: registered DesignWare HDMI I2C bus driver
    rockchip-drm display-subsystem: bound ff980000.hdmi (ops 0xc0c42f4c)

###### userland libraries / kernel connectors

libdrm - not needed
mesa
kms -?

###### userland test apps

v4l2: ffmpeg    configure: --enable-rkmpp    ffmpeg -hwaccels 
/sys/class/video4linux

vdpau:  
https://github.com/wzyy2/libvdpau-rockchip  X11-dev,rkdec-264d, drm-dev  
https://gitlab.freedesktop.org/vdpau/libvdpau/-/tree/master   (generic)


va-api(wayland):
https://github.com/hizukiayaka/rockchip-video-driver

mpp: full hd, no 4k

kmssink: gstreamer 1.19


glx(wayland):
/usr/lib/<arch>/libEGL..







cec-utils, vainfo,

    $ vainfo
    libva info: VA-API version 1.1.0
    libva info: va_getDriverName() returns 0
    libva info: Trying to open /usr/lib/x86_64-linux-gnu/dri/nvidia_drv_video.so
    libva info: va_openDriver() returns -1
    vaInitialize failed with error code -1 (unknown libva error),exit


v4l-cec


  cec-client -l



