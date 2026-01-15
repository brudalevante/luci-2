#
# Copyright (C) 2017-2019 Chen Minqiang <ptpt52@gmail.com>
#
# This is free software, licensed under the GNU General Public License v3.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-fakemesh
PKG_VERSION:=1.0.2
PKG_RELEASE:=1

PKG_LICENSE:=GPLv3
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Chen Minqiang <ptpt52@gmail.com>

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/luci-app-fakemesh
	SECTION:=luci
	CATEGORY:=LuCI
	SUBMENU:=Applications
	TITLE:=LuCI Support for fakemesh
	PKGARCH:=all
	DEPENDS:=+luci-base +jsonfilter +umdns +firewall4
endef

define Package/luci-app-fakemesh/description
	LuCI Support for fakemesh.
	This package provides a LuCI web interface and supporting files
	for configuring fakemesh services and helpers (hotplug hooks, uci defaults, rpcd ACLs).
endef

define Build/Prepare
	$(INSTALL_DIR) $(PKG_BUILD_DIR)
	# Convert PO files to LMO (if any) and place them in build dir
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

define Package/luci-app-fakemesh/conffiles
/etc/config/fakemesh
endef

define Package/luci-app-fakemesh/postinst
#!/bin/sh
if [ -z "$$IPKG_INSTROOT" ]; then
  ( . /etc/uci-defaults/40_luci-app-fakemesh )
  rm -f /etc/uci-defaults/40_luci-app-fakemesh
  ( . /etc/uci-defaults/96-fakemesh-defaults )
  rm -f /etc/uci-defaults/96-fakemesh-defaults

  rm -rf /tmp/luci-indexcache /tmp/luci-modulecache
fi

exit 0
endef

define Package/luci-app-fakemesh/install
	# Lua i18n files
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/i18n
	$(if $(wildcard $(PKG_BUILD_DIR)/fakemesh.*.lmo), \
		$(INSTALL_DATA) $(PKG_BUILD_DIR)/fakemesh.*.lmo $(1)/usr/lib/lua/luci/i18n/,)

	# config
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DATA) ./root/etc/config/fakemesh $(1)/etc/config/fakemesh

	# init script
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./root/etc/init.d/fakemesh $(1)/etc/init.d/fakemesh

	# userland daemon/binary
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) ./root/usr/sbin/fakemesh $(1)/usr/sbin/fakemesh

	# uci defaults
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_DATA) ./root/etc/uci-defaults/40_luci-app-fakemesh $(1)/etc/uci-defaults/40_luci-app-fakemesh
	$(INSTALL_DATA) ./root/etc/uci-defaults/96-fakemesh-defaults $(1)/etc/uci-defaults/96-fakemesh-defaults

	# hotplug hooks
	$(INSTALL_DIR) $(1)/etc/hotplug.d/dhcp
	$(INSTALL_DATA) ./root/etc/hotplug.d/dhcp/10-fakemesh $(1)/etc/hotplug.d/dhcp/10-fakemesh
	$(INSTALL_DIR) $(1)/etc/hotplug.d/iface
	$(INSTALL_DATA) ./root/etc/hotplug.d/iface/19-fakemesh $(1)/etc/hotplug.d/iface/19-fakemesh

	# rpcd ACLs
	$(INSTALL_DIR) $(1)/usr/share/rpcd/acl.d
	$(INSTALL_DATA) ./root/usr/share/rpcd/acl.d/*.json $(1)/usr/share/rpcd/acl.d/ || true

	# LuCI menu entries
	$(INSTALL_DIR) $(1)/usr/share/luci/menu.d
	$(INSTALL_DATA) ./root/usr/share/luci/menu.d/*.json $(1)/usr/share/luci/menu.d/ || true

	# LuCI static view JS
	$(INSTALL_DIR) $(1)/www/luci-static/resources/view/fakemesh
	$(INSTALL_DATA) ./htdocs/luci-static/resources/view/fakemesh/fakemesh.js $(1)/www/luci-static/resources/view/fakemesh/fakemesh.js

	# ucitrack metadata (optional)
	$(INSTALL_DIR) $(1)/usr/share/ucitrack
	$(INSTALL_DATA) ./root/usr/share/ucitrack/*.json $(1)/usr/share/ucitrack/ || true
endef

$(eval $(call BuildPackage,luci-app-fakemesh))
