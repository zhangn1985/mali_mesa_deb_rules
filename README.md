## updated/prebuilt mesa3d driver for lima, panfrost

### Note:

this project is ONLY for debian buster. No mesa3d driver for stretch and older debian, due to build failed, and so much things need to backport.

if you are using ubuntu, please go [graphics-drivers PPA](https://launchpad.net/~oibaf/+archive/ubuntu/graphics-drivers).

these packages will be hosted in [packagecloud](https://packagecloud.io/zhangn1985/mesa), debian buster ONLY.

### NOTE

Armhf support will be dropped after Chinese New Year. but related packages will still be keeped for install, but not update.


### HOWTO:

1, enable [packagecloud](https://packagecloud.io/zhangn1985/mesa) repo

2, run `sudo apt update && apt upgrade`

3.1, configure Xserver for lima:

```
Section "ServerFlags"
        Option  "AutoAddGPU" "off"
        Option "Debug" "dmabuf_capable"
EndSection

Section "OutputClass"
        Identifier "Lima"
        MatchDriver "<display DRM driver>"
        Driver "modesetting"
        Option "PrimaryGPU" "true"
EndSection
```

Mali GPU is only for rendering, each SoC has its own seperated display engine. You need to find your display engine DRM driver name and replace `<display DRM driver>` with it. For example:

Amlogic: meson

Allwinner: sun4i-drm

RockChip: rockchip

Exynos: exynos

save it as `/etc/X11/xorg.conf.d/02-lima.conf`

3.2 configure Xserver for panfrost: same as lima

### build yourself:

1, copy debian to your mesa source code folder.

2,

```
apt build-dep mesa
debuild -i -us -uc -b
```

### plan

Regular bi-weekly/monthly update.
