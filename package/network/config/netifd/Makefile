include $(TOPDIR)/rules.mk

PKG_NAME:=netifd
PKG_VERSION:=20140411
PKG_RELEASE=$(PKG_SOURCE_VERSION)-20140530-1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://nbd.name/luci2/netifd.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=d2a33f3f0fe704e4396fa2ada08401cb955ba7cb
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
PKG_MIRROR_MD5SUM:=368f2e9445acba1a0f12abe12bfc056a
PKG_MAINTAINER:=Felix Fietkau <nbd@openwrt.org>
# PKG_MIRROR_MD5SUM:=
# CMAKE_INSTALL:=1

PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/netifd
  SECTION:=base
  CATEGORY:=Base system
  DEPENDS:=+libuci +libnl-tiny +libubus +ubus +ubusd +jshn
  TITLE:=OpenWrt Network Interface Configuration Daemon
endef

TARGET_CFLAGS += \
	-I$(STAGING_DIR)/usr/include/libnl-tiny \
	-I$(STAGING_DIR)/usr/include

CMAKE_OPTIONS += \
	-DLIBNL_LIBS=-lnl-tiny \
	-DDEBUG=1

define Package/netifd/install
	$(INSTALL_DIR) $(1)/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/netifd $(1)/sbin/
	$(CP) ./files/* $(1)/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/scripts/*.sh $(1)/lib/netifd/
endef

$(eval $(call BuildPackage,netifd))
