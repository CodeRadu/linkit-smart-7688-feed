# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=mtk-linkit
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/mtk-linkit
  TITLE:=Linkit smart 7688 support
  DEPENDS:=+gdbserver +curl +strace +coreutils +coreutils-stty \
  	+avahi-nodbus-daemon +fstools +mjpg-streamer \
	+uhttpd +rpcd +rpcd-mod-iwinfo +git +git-http +ksmbd-server \
	+python3 +python3-pyserial +python3-pip +hidapi \
#	+libmraa +libupm +node +node-cylon-firmata \
	+luci +luci-app-mjpg-streamer +luci-app-ksmbd +luci-lib-json \
	+rpcd-mod-rpcsys +cgi-io +avrdude +spi-tools +uboot-envtools \
	+kmod-fs-vfat +kmod-fs-exfat +kmod-i2c-core +kmod-i2c-ralink \
	+kmod-nls-base +kmod-nls-cp437 +kmod-nls-iso8859-1 \
	+kmod-nls-iso8859-15 +kmod-nls-iso8859-2 +kmod-nls-utf8 \
	+kmod-sdhci-mt7620 +kmod-usb-storage \
	+kmod-video-core +kmod-video-uvc \
	+kmod-sound-core +alsa-utils \
	+mtk-linkit-webui +mtk-sdk-wifi +tcpdump-mini +node +node-cylon-firmata +libmraa +libupm

  CATEGORY:=Board
  DEFAULT:=y
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
endef

define Build/Compile
        $(TARGET_CC) $(TARGET_CFLAGS) $(EXTRA_CFLAGS) -Wall -Werror -o $(PKG_BUILD_DIR)/pinmux src/pinmux.c ; \
        $(TARGET_CC) $(TARGET_CFLAGS) $(EXTRA_CFLAGS) -Wall -Werror -o $(PKG_BUILD_DIR)/refclk src/refclk.c
endef

define Package/mtk-linkit/install
	$(INSTALL_DIR) $(1)/sbin
	
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/pinmux $(1)/sbin/mt7688_pinmux
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/refclk $(1)/sbin/mt7688_reclk
	$(CP) ./files/* $(1)
endef

$(eval $(call BuildPackage,mtk-linkit))
