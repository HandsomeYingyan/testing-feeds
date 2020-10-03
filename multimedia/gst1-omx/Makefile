#
# Copyright (C) 2020 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=gst-omx
PKG_VERSION:=1.10.4
PKG_RELEASE:=1
PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/gst-omx
	SECTION:=multimedia
	CATEGORY:=Multimedia
	TITLE:=gst openmax lib
	DEPENDS:=+gstreamer1 +gstreamer1-plugins-base +libgst1video +libgst1audio +libgst1pbutils +libcedarx +PACKAGE_libgst1gl:libgst1gl
endef

define Package/gst-omx/description
 GStreamer openmax API
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef


OMX_COMPILE_TOOL_CHAIN = arm-openwrt-linux

EXTRA_LDFLAGS+= \
	-Wl,-rpath-link=$(STAGING_DIR)/rootfs/lib \

define Build/Configure
	cd $(PKG_BUILD_DIR);./autogen.sh --host=$(OMX_COMPILE_TOOL_CHAIN) --prefix=$(PKG_BUILD_DIR) --target=arm-openwrt-linux --disable-gtk-doc --with-omx-target=generic
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/ \
		ARCH="$(TARGET_ARCH)" \
		AR="$(TARGET_AR)" \
		CC="$(TARGET_CC)" \
		CXX="$(TARGET_CXX)" \
		CFLAGS="$(TARGET_CFLAGS)" \
		LDFLAGS="$(TARGET_LDFLAGS) $(EXTRA_LDFLAGS)" \
		TARGET_BOARD="$(TARGET_BOARD_PLATFORM)"
	$(MAKE) -C $(PKG_BUILD_DIR)/ \
		ARCH="$(TARGET_ARCH)" \
		AR="$(TARGET_AR)" \
		CC="$(TARGET_CC)" \
		CXX="$(TARGET_CXX)" \
		CFLAGS="$(TARGET_CFLAGS)" \
		LDFLAGS="$(TARGET_LDFLAGS)" \
		TARGET_BOARD="$(TARGET_BOARD_PLATFORM)" \
		install
endef

define Package/gst-omx/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) -rf $(PKG_BUILD_DIR)/lib/gstreamer-1.0 $(1)/usr/lib
	mkdir -p $(1)/etc/xdg
	$(CP) $(PKG_BUILD_DIR)/config/bellagio/gstomx.conf $(1)/etc/xdg/
endef

$(eval $(call BuildPackage,gst-omx))
