
MODULE := znvpair

obj-$(CONFIG_ZFS) := $(MODULE).o

ccflags-y := $(ZFS_MODULE_CFLAGS) $(ZFS_MODULE_CPPFLAGS)

$(MODULE)-objs += nvpair.o
$(MODULE)-objs += fnvpair.o
$(MODULE)-objs += nvpair_alloc_spl.o
$(MODULE)-objs += nvpair_alloc_fixed.o
