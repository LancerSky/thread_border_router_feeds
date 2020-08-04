include $(TOPDIR)/rules.mk

PKG_NAME:=wpantund
PKG_VERSION:=2019-11-13
PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/openthread/wpantund.git
PKG_SOURCE_VERSION:=9e1c0daf7d139ef2668ca28faff8789d2e68364d

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/target.mk
include $(INCLUDE_DIR)/host-build.mk

MAKE_PATH:=src
CONFIGURE_ARGS += \
	--sysconfdir=/etc 

define Host/Configure
	$(call Host/Configure/Default)
endef

define Host/Compile
	$(call Host/Compile/Default)
endef

define Host/Install
	$(call Host/Install/Default)
endef

define Package/wpantund
	SECTION:=net
	CATEGORY:=Network
	TITLE:=wpantund
	DEPENDS:=+libreadline +dbus +libstdcpp +libncurses +boost +boost-signals +boost-system +kmod-tun
endef

define Package/wpantund/description
 wpantund is a user-space network interface driver/daemon that provides a native IPv6 network interface to a low-power wireless Network Co-Processor (or NCP).
 It was written and developed by Nest Labs to make supporting Thread connectivity on Unix-like operating systems more straightforward.

 wpantund is designed to marshall all access to the NCP, ensuring that it always remains in a consistent and well-defined state.
endef

define Build/Configure
	cd $(PKG_BUILD_DIR) && ./bootstrap.sh
	$(call Build/Configure/Default,--sysconfdir=/etc)
endef

define Package/wpantund/install
	$(INSTALL_DIR) $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc/
	$(INSTALL_DIR) $(1)/usr/local/bin/
	$(INSTALL_DIR) $(1)/usr/local/etc/
	$(INSTALL_DIR) $(1)/usr/local/lib/
	$(INSTALL_DIR) $(1)/usr/local/include/wpantund/
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/etc/dbus-1/system.d/
	$(INSTALL_DIR) $(1)/usr/local/share/man/man1/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/wpantund/wpantund $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/wpanctl/wpanctl $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/ncp-spinel/ncp-spinel.la $(1)/usr/lib/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/ncp-dummy/ncp-dummy.la $(1)/usr/lib/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/ncp-spinel/.libs/ncp-spinel.so $(1)/usr/lib/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/ncp-spinel/ncp-spinel.la $(1)/usr/local/lib/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/ncp-dummy/.libs/ncp-dummy.so $(1)/usr/local/lib/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/ncp-dummy/ncp-dummy.la $(1)/usr/local/lib/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/src/ipc-dbus/wpan-dbus-v0.h $(1)/usr/local/include/wpantund/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/src/ipc-dbus/wpan-dbus-v1.h $(1)/usr/local/include/wpantund/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/src/ipc-dbus/wpantund.conf $(1)/etc/dbus-1/system.d/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/src/wpantund/wpantund.conf $(1)/etc/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/src/wpantund/wpan-properties.h $(1)/usr/local/include/wpantund
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/src/wpantund/wpan-error.h $(1)/usr/local/include/wpantund
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,wpantund))
