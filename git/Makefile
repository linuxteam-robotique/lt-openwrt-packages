#
# Copyright (C) 2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Alessandro Di Marco <dmr-wrt@ethzero.com>

include $(TOPDIR)/rules.mk

PKG_NAME:=git
PKG_VERSION:=1.6.5.6
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=@KERNEL/software/scm/git
PKG_MD5SUM:=03aefaaecae7a236b88d04d1a83698d9

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/git
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Version Control Systems
  DEPENDS:=+libopenssl +libpthread
  TITLE:=The fast version control system
  URL:=http://git-scm.com
endef

define Package/git/description
 Git is a free & open source, distributed version control system
 designed to handle everything from small to very large projects
 with speed and efficiency.
endef

MAKE_FLAGS := \
	CC="$(TARGET_CC)" \
	LD="$(TARGET_CC)" \
	CFLAGS="$(TARGET_CFLAGS) $(TARGET_CPPFLAGS)" \
	CPPFLAGS="$(TARGET_CPPFLAGS)" \
	LDFLAGS="$(TARGET_LDFLAGS)" \
	NO_PERL="YesPlease" \
	NO_EXPAT="YesPlease" \
	NO_WISH="YesPlease" \
	NO_ICONV="YesPlease" \
	NO_NSEC="YesPlease" \
	NO_CURL="YesPlease" \
	NO_TCLTK="YesPlease" \

define Build/Configure
	$(MAKE) -C $(PKG_BUILD_DIR) \
		configure

	(cd $(PKG_BUILD_DIR); \
		./configure \
			--prefix=/usr \
	);
endef

define Package/git/install
	$(INSTALL_DIR) $(1)
	$(CP) $(PKG_INSTALL_DIR)/* $(1)/
endef

$(eval $(call BuildPackage,git))
