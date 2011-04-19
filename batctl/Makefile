#
# Copyright (C) 2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# $Id: Makefile 5624 2006-11-23 00:29:07Z nbd $

include $(TOPDIR)/rules.mk

PKG_NAME:=batctl-devel

PKG_REV:=HEAD

PKG_VERSION:=$(PKG_REV)
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_URL:=../../../batctl
PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/batctl-devel
  URL:=http://www.open-mesh.org/
  MAINTAINER:=Marek Lindner <lindner_marek@yahoo.de>
  SUBMENU:=Network Support
  DEPENDS:=@!LINUX_2_4
  TITLE:=Batctl devel
  FILES:=$(PKG_BUILD_DIR)/batctl
endef

define Package/batctl/description
batctl is a more intuitive managment utility for B.A.T.M.A.N.-Advanced.
It is an easier method for configuring batman-adv and
provides some additional tools for debugging as well.
endef

MAKE_BATCTL_ARGS += \
	CFLAGS="$(TARGET_CFLAGS)" \
	CCFLAGS="$(TARGET_CFLAGS)" \
	OFLAGS="$(TARGET_CFLAGS)" \
	REVISION="$(PKG_REV)" \
	CC="$(TARGET_CC)" \
	NODEBUG=1 \
	UNAME="Linux" \
	INSTALL_PREFIX="$(PKG_INSTALL_DIR)" \
	STRIP="/bin/true" \
	batctl install

ifneq ($(DEVELOPER)$(CONFIG_KMOD_BATMAN_ADV_DEVEL_BATCTL),)
BUILD_BATCTL = $(MAKE) -C $(PKG_BUILD_DIR) $(MAKE_BATCTL_ARGS)
endif

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) $(MAKE_BATCTL_ARGS)
endef

define Build/Clean
	rm -rf $(BUILD_DIR)/$(PKG_NAME)/
endef

define Package/batctl-devel/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/batctl $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,batctl-devel))
