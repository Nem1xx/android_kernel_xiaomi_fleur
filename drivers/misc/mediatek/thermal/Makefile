#
# Copyright (C) 2015 MediaTek Inc.
#
# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License version 2 as
# published by the Free Software Foundation.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
# GNU General Public License for more details.
#

ccflags-y += -I$(srctree)

ifeq ($(CONFIG_MACH_MT6833),y)
	PDIR = mt6833
else ifeq ($(CONFIG_MACH_MT6893),y)
	PDIR = mt6893
else ifeq ($(CONFIG_MACH_MT6781),y)
	PDIR = mt6781
else
	PDIR = $(MTK_PLATFORM)
endif

ifeq ($(CONFIG_ARCH_MT7623), y)
# MT2701 & MT7623 use the same thermal driver.
THERMAL_CHIP_DRIVER_DIR := $(srctree)/drivers/misc/mediatek/thermal/mt2701
else
THERMAL_CHIP_DRIVER_DIR := $(srctree)/drivers/misc/mediatek/thermal/$(PDIR)
endif

ccflags-y  += -I$(THERMAL_CHIP_DRIVER_DIR)/inc
ccflags-y  += -I$(srctree)/drivers/misc/mediatek/thermal/fakeHeader/
ccflags-y  += -I$(srctree)/drivers/misc/mediatek/base/power/$(PDIR)
ccflags-y  += -I$(srctree)/drivers/misc/mediatek/base/power/include/
ccflags-y  += -I$(srctree)/drivers/misc/mediatek/base/power/include/gpufreq_v1/
ccflags-y  += -I$(srctree)/drivers/misc/mediatek/flashlight/

obj-$(CONFIG_THERMAL) += mtk_thermal_monitor.o
obj-$(CONFIG_THERMAL) += mtk_cooler_shutdown.o
ifeq ($(CONFIG_MTK_LEDS), y)
    # setMaxbrightness() defined in mediatek/kernel/drivers/leds/leds_drv.c only built when CONFIG_MTK_LEDS is set
    #obj-$(CONFIG_THERMAL) += mtk_cooler_backlight.o
	obj-$(CONFIG_THERMAL) += mtk_cooler_backlight_cus.o
endif
obj-$(CONFIG_THERMAL) += mtk_cooler_flashlight_cus.o
obj-$(CONFIG_THERMAL) += mtk_cooler_kshutdown.o
#obj-$(CONFIG_THERMAL) += mtk_cooler_spkrvol.o
#obj-$(CONFIG_THERMAL) += mtk_cooler_dropcall.o
obj-$(CONFIG_THERMAL) += mtk_cooler_cam.o

ifeq (,$(filter $(CONFIG_ARCH_MT8173) $(CONFIG_ARCH_MT8163) $(CONFIG_MACH_MT2701) $(CONFIG_ARCH_MT7623) $(CONFIG_ARCH_MT8127) $(CONFIG_MACH_MT8167), y))
obj-y += common/
endif

ifeq ($(CONFIG_ARCH_MT7623), y)
# MT2701 & MT7623 use the same thermal driver.
obj-y += mt2701/
else ifeq ($(CONFIG_MACH_MT6833),y)
obj-y += mt6833/
else ifeq ($(CONFIG_MACH_MT6893),y)
obj-y += mt6893/
else ifeq ($(CONFIG_MACH_MT6781),y)
obj-y += mt6781/
else
obj-y += $(subst ",,$(CONFIG_MTK_PLATFORM))/
endif
