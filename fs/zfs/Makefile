obj-m += avl/
obj-m += icp/
obj-m += lua/
obj-m += nvpair/
obj-m += spl/
obj-m += os/linux/spl/
obj-m += unicode/
obj-m += zcommon/
obj-m += zfs/
obj-m += os/linux/zfs/

INSTALL_MOD_DIR ?= extra

ZFS_MODULE_CFLAGS += -std=gnu99 -Wno-declaration-after-statement
ZFS_MODULE_CFLAGS +=   -Wno-format-zero-length
ZFS_MODULE_CFLAGS += -include /var/TMP-SAFE/portage/sys-fs/zfs-kmod-9999/work/zfs-kmod-9999/zfs_config.h
ZFS_MODULE_CFLAGS += -I/var/TMP-SAFE/portage/sys-fs/zfs-kmod-9999/work/zfs-kmod-9999/include/os/linux/kernel
ZFS_MODULE_CFLAGS += -I/var/TMP-SAFE/portage/sys-fs/zfs-kmod-9999/work/zfs-kmod-9999/include/os/linux/spl
ZFS_MODULE_CFLAGS += -I/var/TMP-SAFE/portage/sys-fs/zfs-kmod-9999/work/zfs-kmod-9999/include/os/linux/zfs
ZFS_MODULE_CFLAGS += -I/var/TMP-SAFE/portage/sys-fs/zfs-kmod-9999/work/zfs-kmod-9999/include
ZFS_MODULE_CPPFLAGS += -D_KERNEL
ZFS_MODULE_CPPFLAGS += -UDEBUG -DNDEBUG

#ZFS_MODULE_CFLAGS += -I/include
#KBUILD_EXTRA_SYMBOLS += 

export ZFS_MODULE_CFLAGS ZFS_MODULE_CPPFLAGS

SUBDIR_TARGETS = icp lua

all: modules
distclean maintainer-clean: clean
install: modules_install
uninstall: modules_uninstall
check:

modules-Linux:
	list='$(SUBDIR_TARGETS)'; for targetdir in $$list; do \
		$(MAKE) -C $$targetdir; \
	done
	$(MAKE) -C /usr/src/linux M=`pwd`  CONFIG_ZFS=m modules

# Only pass down gmake -j flag, if used.
modules-FreeBSD:
	flags="$$(echo $$MAKEFLAGS | awk -v RS=' ' /^-j/)"; \
	env MAKEFLAGS="" make $${flags} -f Makefile.bsd

modules-unknown:
	@true

modules: modules-Linux

clean-Linux:
	@# Only cleanup the kernel build directories when CONFIG_KERNEL
	@# is defined.  This indicates that kernel modules should be built.
#	$(MAKE) -C /usr/src/linux M=`pwd`  clean

	if [ -f NONE ]; then $(RM) NONE; fi
	if [ -f Module.markers ]; then $(RM) Module.markers; fi

	find . -name '*.ur-safe' -type f -print | xargs $(RM)

clean-FreeBSD:
	flags="$$(echo $$MAKEFLAGS | awk -v RS=' ' /^-j/)"; \
	env MAKEFLAGS="" make $${flags} -f Makefile.bsd clean

clean: clean-Linux

modules_install-Linux:
	@# Install the kernel modules
	$(MAKE) -C /usr/src/linux M=`pwd` modules_install \
		INSTALL_MOD_PATH=$(DESTDIR)$(INSTALL_MOD_PATH) \
		INSTALL_MOD_DIR=$(INSTALL_MOD_DIR) \
		KERNELRELEASE=5.6.7-rt-jsX-g07571df78
	@# Remove extraneous build products when packaging
	kmoddir=$(DESTDIR)$(INSTALL_MOD_PATH)/lib/modules/5.6.7-rt-jsX-g07571df78; \
	if [ -n "$(DESTDIR)" ]; then \
		find $$kmoddir -name 'modules.*' | xargs $(RM); \
	fi
	sysmap=$(DESTDIR)$(INSTALL_MOD_PATH)/boot/System.map-5.6.7-rt-jsX-g07571df78; \
	if [ -f $$sysmap ]; then \
		depmod -ae -F $$sysmap 5.6.7-rt-jsX-g07571df78; \
	fi

CTAGS: ctags
ctags-am: $(TAGS_DEPENDENCIES) $(am__tagged_files)
	$(am__define_uniq_tagged_files); \
	test -z "$(CTAGS_ARGS)$$unique" \
	  || $(CTAGS) $(CTAGSFLAGS) $(AM_CTAGSFLAGS) $(CTAGS_ARGS) \
	     $$unique

GTAGS:
	here=`$(am__cd) $(top_builddir) && pwd` \
	  && $(am__cd) $(top_srcdir) \
	  && gtags -i $(GTAGS_ARGS) "$$here"
cscopelist: cscopelist-recursive

cscopelist-am: $(am__tagged_files)
	list='$(am__tagged_files)'; \
	case "$(srcdir)" in \
	  [\\/]* | ?:[\\/]*) sdir="$(srcdir)" ;; \
	  *) sdir=$(subdir)/$(srcdir) ;; \
	esac; \
	for i in $$list; do \
	  if test -f "$$i"; then \
	    echo "$(subdir)/$$i"; \
	  else \
	    echo "$$sdir/$$i"; \
	  fi; \
	done >> $(top_builddir)/cscope.files

modules_install-FreeBSD:
	@# Install the kernel modules
	flags="$$(echo $$MAKEFLAGS | awk -v RS=' ' /^-j/)"; \
	env MAKEFLAGS="" make $${flags} -f Makefile.bsd install

modules_install: modules_install-Linux

modules_uninstall-Linux:
	@# Uninstall the kernel modules
	kmoddir=$(DESTDIR)$(INSTALL_MOD_PATH)/lib/modules/5.6.7-rt-jsX-g07571df78
	list='$(obj-m)'; for objdir in $$list; do \
		$(RM) -R $$kmoddir/$(INSTALL_MOD_DIR)/$$objdir; \
	done

modules_uninstall-FreeBSD:
	@false

modules_uninstall: modules_uninstall-Linux

distdir:
	list='$(obj-m)'; for objdir in $$list; do \
		(cd ../module && find $$objdir -name '*.[chS]' | \
		while read path; do \
			mkdir -p /var/TMP-SAFE/portage/sys-fs/zfs-kmod-9999/work/zfs-kmod-9999/module/$$distdir/$${path%/*}; \
			cp $$path /var/TMP-SAFE/portage/sys-fs/zfs-kmod-9999/work/zfs-kmod-9999/module/$$distdir/$$path; \
		done); \
	done
