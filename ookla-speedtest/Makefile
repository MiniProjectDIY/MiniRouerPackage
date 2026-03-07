include $(TOPDIR)/rules.mk

PKG_NAME:=ookla-speedtest
PKG_VERSION:=1.2.0
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/ookla-speedtest
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Ookla Speedtest CLI
  URL:=https://www.speedtest.net/apps/cli
endef


# =====================================================
#   按架构选择不同下载文件
#   支持：
#      x86_64
#      aarch64_generic
#      aarch64_cortex-a53
# =====================================================

# ---- x86_64 ----
ifeq ($(ARCH_PACKAGES),x86_64)
  PKG_SOURCE:=ookla-speedtest-$(PKG_VERSION)-linux-x86_64.tgz
  PKG_SOURCE_URL:=https://install.speedtest.net/app/cli/
  PKG_HASH:=skip
endif

# ---- 所有 aarch64（generic + cortex-a53）----
ifeq ($(findstring aarch64,$(ARCH_PACKAGES)),aarch64)
  PKG_SOURCE:=ookla-speedtest-$(PKG_VERSION)-linux-aarch64.tgz
  PKG_SOURCE_URL:=https://install.speedtest.net/app/cli/
  PKG_HASH:=skip
endif


# =====================================================
#  Build 阶段：解压 tgz → speedtest
# =====================================================
define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	# 解压 tgz（其中包含 speedtest 可执行文件和一些 .md, LICENSE 文件）
	$(TAR) -xzf $(DL_DIR)/$(PKG_SOURCE) -C $(PKG_BUILD_DIR)
	chmod +x $(PKG_BUILD_DIR)/speedtest
endef

define Build/Compile
	# 无需编译（上游提供的是静态二进制）
endef


# =====================================================
# 安装到 /usr/bin/speedtest
# =====================================================
define Package/ookla-speedtest/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/speedtest $(1)/usr/bin/speedtest
endef


$(eval $(call BuildPackage,ookla-speedtest))

