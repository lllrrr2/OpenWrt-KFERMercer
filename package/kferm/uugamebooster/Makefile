#
# Copyright (C) 2021 KFERMercer <KFER.Mercer@gmail.com>
#
# This is free software, licensed under the GNU General Public License v3.
#

# 
# to get the latest version & md5 checksum:
# curl -L -s -k -H "Accept:text/plain" "http://router.uu.163.com/api/plugin?type=openwrt-$(UU_ARCH)"
# 

include $(TOPDIR)/rules.mk

PKG_NAME:=uugamebooster
PKG_VERSION:=v2.7.8
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=net
	CATEGORY:=Network
	DEPENDS:=@(aarch64||arm||mips||mipsel||x86_64) +kmod-tun
	TITLE:=NetEase UU Game Booster
	URL:=https://uu.163.com
endef

define Package/$(PKG_NAME)/description
NetEase's UU Game Booster Accelerates Triple-A Gameplay and Market
endef

ifeq ($(ARCH),x86_64)
	UU_ARCH:=x86_64
	PKG_MD5SUM:=7964978383c6c1535a8a8799b96498d7
endif

ifeq ($(ARCH),mipsel)
	UU_ARCH:=mipsel
	PKG_MD5SUM:=e25531db253ae05e13367d98ab862e45
endif

ifeq ($(ARCH),mips)
	UU_ARCH:=mipsel
	PKG_MD5SUM:=e25531db253ae05e13367d98ab862e45
endif

ifeq ($(ARCH),arm)
	UU_ARCH:=arm
	PKG_MD5SUM:=5a308f12a9855841dab6c534453850aa
endif

ifeq ($(ARCH),aarch64)
	UU_ARCH:=aarch64
	PKG_MD5SUM:=f7d891a1c9eecb900a1981df47bf365f
endif

PKG_SOURCE_URL:=http://uu.gdl.netease.com/openwrt-$(UU_ARCH)/$(PKG_VERSION)/uu.tar.gz?
PKG_SOURCE:=$(PKG_NAME)-$(UU_ARCH)-$(PKG_VERSION).tar.gz

STRIP:=true

UNTAR_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)/$(PKG_NAME)-$(UU_ARCH)-bin

define Build/Prepare
	mkdir -vp $(UNTAR_DIR)
	tar -zxvf $(DL_DIR)/$(PKG_SOURCE) -C $(UNTAR_DIR)
endef

define Build/Compile
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/uugamebooster.init $(1)/etc/init.d/uugamebooster

	$(INSTALL_DIR) $(1)/usr/share/$(PKG_NAME)
	$(INSTALL_BIN) $(UNTAR_DIR)/uuplugin $(1)/usr/share/$(PKG_NAME)/uuplugin
	$(INSTALL_CONF) $(UNTAR_DIR)/uu.conf $(1)/usr/share/$(PKG_NAME)/uu.conf

	# not finish yet:
	# $(INSTALL_DIR) $(1)/usr/bin
	# $(INSTALL_BIN) ./files/uugamebooster-update $(1)/usr/bin/$(PKG_NAME)
	# $(LN) $(1)/usr/bin/$(PKG_NAME)/uugamebooster-update $(1)/usr/bin/uugamebooster-update
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
