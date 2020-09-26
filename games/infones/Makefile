#
#
# Copyright (C) 2020 HandsomeMod Project
#
#
include $(TOPDIR)/rules.mk


PKG_NAME:=infones
PKG_VERSION:=1.0.0

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/nejidev/arm-NES-linux.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:= e14ec579b3fb58f4c061ca38c103cc11d58d1673
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)
PKG_MAINTAINER:=HandsomeYingyan <handsomeyingyan@gmail.com>

include $(INCLUDE_DIR)/package.mk


define Package/$(PKG_NAME)
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=NES emulator
  DEPENDS:=+alsa-lib
endef

define Package/$(PKG_NAME)/description
 InfoNes Is a NES emulator！
endef

# Nothing just to be sure
#define Build/Configure
#endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		$(TARGET_CONFIGURE_OPTS) \
		TARGET=Linux \
		CFLAGS="$(TARGET_CFLAGS) $(TARGET_CPPFLAGS)" \
		LDFLAGS="$(TARGET_LDFLAGS)" \
		-f $(PKG_BUILD_DIR)/linux/Makefile
endef


define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/linux/InfoNES $(1)/usr/bin/infones
endef

$(eval $(call BuildPackage,$(PKG_NAME)))

