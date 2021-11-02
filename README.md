# retrorun-go2
libretro frontend for ODROID-GO Advance \
Use this for RG351P with rg351p-js2box available [here](https://github.com/christianhaitian/RG351P_virtual-gamepad).  For the RGB10, use the rgb10 branch.  For the RK2020, use the rk2020 branch.

Build
======
```
git clone https://github.com/christianhaitian/retrorun-go2.git
make
strip retrorun
```

Buildroot package
======
```
################################################################################
#
# RETRORUN
#
################################################################################

RETRORUN_VERSION = master
RETRORUN_SITE = $(call github,lualiliu,retrorun-go2,$(RETRORUN_VERSION))
RETRORUN_LICENSE = GPLv2
RETRORUN_DEPENDENCIES = libgo2 librga libevdev libpng libopenal libasound

define RETRORUN_BUILD_CMDS
   PKG_CONFIG="$(BASE_DIR)/host/bin/pkg-config" $(MAKE) CC="$(TARGET_CC)" LD="$(TARGET_LD)" CXX="$(TARGET_CXX)" -C $(@D)
endef

define RETRORUN_INSTALL_TARGET_CMDS
	$(INSTALL) -D -m 0755 $(@D)/retrorun \
		$(TARGET_DIR)/usr/bin/retrorun
endef

$(eval $(generic-package))

```