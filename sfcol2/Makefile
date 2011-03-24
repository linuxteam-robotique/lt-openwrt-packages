include $(TOPDIR)/rules.mk
PKG_NAME:=sfcol2
PKG_RELEASE:=2
PKG_MD5SUM:=1b165dd7cb8a3298af5ecd4aa6a295b5
PKG_SOURCE_URL:=http://castor.xenbox.fr/~yam/tmp/ 
PKG_SOURCE:=$(PKG_NAME).tar.gz

include $(INCLUDE_DIR)/package.mk

define Package/sfcol2
	SECTION:=tuxy
	CATEGORY:=Eurobot2010
	SUBMENU:=Video
	DEPENDS:=+libpthread
	TITLE:=Color and Shape analysis
	URL:=http://linuxteam.xenbox.fr/
endef

define Package/sfcol2/description
	blabla
endef

define Build/Compile
        $(MAKE) -C $(PKG_BUILD_DIR) $(TARGET_CONFIGURE_OPTS) \
	SERVFLAGS="$(TARGET_CFLAGS) -I$(STAGING_DIR)/usr/include"
endef

define Package/sfcol2/install
	$(INSTALL_DIR) $(1)
	$(CP) $(PKG_BUILD_DIR)/sfcol2 $(1)/
endef

$(eval $(call BuildPackage,sfcol2))
