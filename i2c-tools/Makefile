#
# Copyright (C) 2007 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=i2c-tools
PKG_VERSION:=3.0.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://dl.lm-sensors.org/i2c-tools/releases/
PKG_MD5SUM:=b546345ac19db56719dea6b8199f11e0

PYTHON_VERSION=2.6

PYTHON_DIR:=$(STAGING_DIR)/usr
PYTHON_BIN_DIR:=$(PYTHON_DIR)/bin
PYTHON_INC_DIR:=$(PYTHON_DIR)/include/python$(PYTHON_VERSION)
PYTHON_LIB_DIR:=$(PYTHON_DIR)/lib/python$(PYTHON_VERSION)

PYTHON:=python$(PYTHON_VERSION)

PYTHON_PKG_DIR:=/usr/lib/python$(PYTHON_VERSION)/site-packages

include $(INCLUDE_DIR)/package.mk

define Package/i2c-tools
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=I2C tools for Linux
  DEPENDS:=@LINUX_2_6
  URL:=http://www.lm-sensors.org/wiki/I2CTools
endef

define Package/python-smbus
 SUBMENU:=Python
 SECTION:=lang
 CATEGORY:=Languages
 TITLE:=Python SMBus                                 
 URL:=http://www.lm-sensors.org/wiki/I2CTools
endef

define Package/i2c-tools/description
 This package contains an heterogeneous set of I2C tools for Linux. These tools
 were originally part of the lm-sensors package.
 Includes:
 - i2cdetect
 - i2cdump
 - i2cget
 - i2cset
endef

define Package/python-smbus/description
 Python bindings for Linux SMBus access through i2c-dev
 This Python module allows SMBus access through the I2C /dev interface on
 Linux hosts.  The host kernel must have I2C support, I2C device interface
 support, and a bus adapter driver.
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		LINUX="$(LINUX_DIR)" \
		CC="$(TARGET_CC)" \
		STAGING_DIR="$(STAGING_DIR)"
	( cd $(PKG_BUILD_DIR)/py-smbus; \
                CFLAGS="$(TARGET_CFLAGS) -I../include" \
                CPPFLAGS="$(TARGET_CPPFLAGS)" \
                LDFLAGS="$(TARGET_LDFLAGS)" \
                $(PYTHON) ./setup.py build && \
                find $(PKG_INSTALL_DIR) -name "*\.pyc" -o -name "*\.pyo" | xargs rm -f \
        );
endef

define Package/i2c-tools/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/tools/i2cdetect $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/tools/i2cdump $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/tools/i2cset $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/tools/i2cget $(1)/usr/sbin/
endef

define Package/python-smbus/install
	$(INSTALL_DIR) $(1)/usr/lib/python2.6/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/py-smbus/build/lib.linux-x86_64-2.6/smbus.so $(1)/usr/lib/python2.6/
endef

$(eval $(call BuildPackage,i2c-tools))
$(eval $(call BuildPackage,python-smbus))

