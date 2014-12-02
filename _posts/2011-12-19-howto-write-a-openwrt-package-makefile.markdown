---
layout: post
title: "OpenWrt的Makefile规则"
date: '2011-12-19'
comments: true
---
OPENWRT集成非官方包之Makefile规则

```
include $(TOPDIR)/rules.mk

PKG_NAME:=[软件包名字 和文件夹名称一样]
PKG_VERSION:=[软件包版本 自己写个]
PKG_RELEASE:=1

PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
        SECTION:=utils
        CATEGORY:=[软件包在menuconfig里的位置 比如Base system]
        DEPENDS:=[依赖包 两个之间通过空格分隔 前面加+为默认显示 选中该软件包自动选中依赖包 不加+为默认不显示 选中依赖包才显示]
        TITLE:=[标题]
        PKGARCH:=[平台 比如ar71xx 全部写all]
        MAINTAINER:=[作者]
endef

define Package/$(PKG_NAME)/description
        [软件包简介]
endef

define Build/Prepare
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/$(PKG_NAME)/conffiles
[升级时保留文件/备份时备份文件 一个文件一行]
endef

define Package/$(PKG_NAME)/install
        $(CP) ./files/* $(1)/
[安装(编译)时执行的脚本 记得加上#!/bin/sh 没有就空着]
endef

define Package/$(PKG_NAME)/preinst
[安装前执行的脚本 记得加上#!/bin/sh 没有就空着]
endef

define Package/$(PKG_NAME)/postinst
[安装后执行的脚本 记得加上#!/bin/sh 没有就空着]
endef

Package/$(PKG_NAME)/prerm
[删除前执行的脚本 记得加上#!/bin/sh 没有就空着]
endef

Package/$(PKG_NAME)/postrm
[删除后执行的脚本 记得加上#!/bin/sh 没有就空着]
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
```
