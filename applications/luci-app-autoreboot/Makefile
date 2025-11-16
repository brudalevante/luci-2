#
# Copyright (C) 2020-2025 Chen Minqiang <ptpt52@gmail.com>
#
# This is free software, licensed under the GNU General Public License v3.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-autoreboot
PKG_VERSION:=1.0.1
PKG_RELEASE:=1

PKG_LICENSE:=GPLv3
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Chen Minqiang <ptpt52@gmail.com>

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/luci-app-autoreboot
	SECTION:=luci
	CATEGORY:=LuCI
	SUBMENU:=Applications
	TITLE:=LuCI Support for autoreboot
	PKGARCH:=all
	DEPENDS:=+busybox +@BUSYBOX_CONFIG_CROND +luci-base
endef

define Package/luci-app-autoreboot/description
	LuCI Support for autoreboot.
	This package provides a LuCI web interface and supporting files
	for configuring automatic reboots.
endef

define Build/Prepare
	$(INSTALL_DIR) $(PKG_BUILD_DIR)
	# Convert PO files to LMO (if any)
	$(foreach po,$(wildcard $(CURDIR)/files/luci/i18n/*.po), \
		$(INSTALL_DIR) $(PKG_BUILD_DIR)/i18n; \
		po2lmo $(po) $(PKG_BUILD_DIR)/$(notdir $(patsubst %.po,%.lmo,$(po)));)
endef

define Build/Configure
	# no configure step
endef

define Build/Compile
	# no compile step
endef

define Package/luci-app-autoreboot/conffiles
/etc/config/autoreboot
endef

define Package/luci-app-autoreboot/postinst
#!/bin/sh
if [ -z "$$IPKG_INSTROOT" ]; then
  ( . /etc/uci-defaults/40_luci-app-autoreboot )
  rm -f /etc/uci-defaults/40_luci-app-autoreboot

  rm -rf /tmp/luci-indexcache /tmp/luci-modulecache
fi

exit 0
endef

define Package/luci-app-autoreboot/install
	# lua i18n
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/i18n
	$(if $(wildcard $(PKG_BUILD_DIR)/autoreboot.*.lmo), \
		$(INSTALL_DATA) $(PKG_BUILD_DIR)/autoreboot.*.lmo $(1)/usr/lib/lua/luci/i18n/,)

	# config file
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DATA) ./root/etc/config/autoreboot $(1)/etc/config/autoreboot

	# init script
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./root/etc/init.d/autoreboot $(1)/etc/init.d/autoreboot

	# uci defaults
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_DATA) ./root/etc/uci-defaults/40_luci-app-autoreboot $(1)/etc/uci-defaults/40_luci-app-autoreboot

	# rpcd ACLs
	$(INSTALL_DIR) $(1)/usr/share/rpcd/acl.d
	$(INSTALL_DATA) ./root/usr/share/rpcd/acl.d/*.json $(1)/usr/share/rpcd/acl.d/

	# menu entries
	$(INSTALL_DIR) $(1)/usr/share/luci/menu.d
	$(INSTALL_DATA) ./root/usr/share/luci/menu.d/*.json $(1)/usr/share/luci/menu.d/

	# LuCI static JS (view)
	$(INSTALL_DIR) $(1)/www/luci-static/resources/view/system
	$(INSTALL_DATA) ./htdocs/luci-static/resources/view/system/autoreboot.js $(1)/www/luci-static/resources/view/system/autoreboot.js

	# ucitrack (if provided)
	$(INSTALL_DIR) $(1)/usr/share/ucitrack
	$(INSTALL_DATA) ./root/usr/share/ucitrack/*.json $(1)/usr/share/ucitrack/ || true
endef

$(eval $(call BuildPackage,luci-app-autoreboot))
