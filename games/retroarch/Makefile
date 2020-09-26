#
# Copyright (C) 2020 HandsomeMod Project
#
# This program is relesed under gplv3 license
#

include $(TOPDIR)/rules.mk

PKG_NAME:=retroarch
PKG_VERSION:=1.8.9
PKG_SOURCE:=v$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/libretro/retroarch/archive/release
PKG_MD5SUM:=5a2114f2a6f348bdab5bf52b994811db
PKG_FIXUP:=autoreconf
PKG_INSTALL:=1



include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=retroarch
  CATEGORY:=RetroArch
  TITLE:=Reference frontend for the libretro API
  DEPENDS:=+ffmpeg +qt5-core +zlib +alsa-lib +eudev +SDL2 +libfreetype +mali400-um +retroarch-assets
  URL:=https://retroarch.com
endef

define Package/$(PKG_NAME)/decription
  Reference frontend for the libretro API
endef

CONFIGURE_ARGS += \
		--prefix=/usr \
		--enable-dynamic \
		--disable-vg \
		--disable-discord \
		--disable-builtinminiupnpc \
		--disable-builtinmbedtls \
		--disable-builtinflac \
		--disable-builtinzlib \
		--disable-opengl \
		--enable-mali_fbdev \
		--disable-x11 \
		--enable-opengles \
		--disable-wayland \
		--enable-alsa \
		--enable-qt \
		--disable-systemd \
		--enable-udev \
		--enable-sdl2 \
		--enable-networking \
		--disable-d3dx \
		--disable-d3d8 \
		--disable-d3d9 \
		--disable-d3d10 \
		--disable-d3d11 \
		--disable-d3d12 \
		--enable-materialui

define Build/InstallDev
	$(MAKE) install
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/share
	$(CP) $(PKG_INSTALL_DIR)/usr/share/* $(1)/usr/share
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
