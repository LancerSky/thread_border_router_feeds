include $(TOPDIR)/rules.mk

PKG_NAME:=paho-mqtt-sn
PKG_VERSION:=2020-07-09
PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/eclipse/paho.mqtt-sn.embedded-c.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=ab94a094b543b1b24c28ab58d741ffb928cec48f
PKG_USE_MIPS16:=0
PKG_LICENSE:=EDL

include $(INCLUDE_DIR)/package.mk

define Package/paho-mqtt-sn
	SECTION:=net
	CATEGORY:=Network
	DEPENDS:=+libopenssl +libstdcpp +libpthread +librt
	TITLE:=paho
endef

define Package/paho-mqtt-sn/description
	MQTT-SN gateway provided by the Eclipse Paho.
endef
TARGET_CXXFLAGS += -D_GLIBCXX_USE_C99=1
define Build/Configure
	$(call Build/Configure/Default)
endef

MAKE_PATH:=MQTTSNGateway

define Build/Compile
	$(call Build/Compile/Default)
endef

define Package/paho-mqtt-sn/install
	$(INSTALL_DIR) $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(MAKE_PATH)/Build/MQTT-SNGateway $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(MAKE_PATH)/Build/MQTT-SNLogmonitor $(1)/usr/bin/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/$(MAKE_PATH)/gateway.conf $(1)/etc/paho-mqtt-sn-gateway.conf
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/$(MAKE_PATH)/clients.conf $(1)/etc/paho-mqtt-sn-clients.conf
endef

$(eval $(call BuildPackage,paho-mqtt-sn))
