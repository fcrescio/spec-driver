
obj-m := specDriver.o
specDriver-objs := base.o int.o umem.o kmem.o sysfs.o ioctl.o

KERNELDIR ?= /lib/modules/$(shell uname -r)/build
INSTALLDIR ?= /lib/modules/$(shell uname -r)/extra
PWD := $(shell pwd)
OS_NAME := $(shell cat /etc/os-release | grep -w "ID=" | awk -F= '{print $$2}'  | sed s/\"//g)
OS_VERSION := $(shell cat /etc/os-release | grep -w "VERSION_ID=" | awk -F= '{print $$2}' |  awk -F. '{print $$1}' | sed s/\"//g)
OS_MINOR :=  $(shell cat /etc/os-release | grep -w "VERSION_ID=" | awk -F= '{print $$2}' |  awk -F. '{print $$2}' | sed s/\"//g)

ifeq ($(OS_NAME),almalinux)
    ifeq ($(OS_VERSION),9)
       KBUILD_CFLAGS += -DKERNEL_ALMA=${OS_VERSION}${OS_MINOR}
    endif
endif


default:
	@echo "OS_NAME: $(OS_NAME)"
	@echo "OS_VERSION: $(OS_VERSION)"
	@echo "OS_VERSION: $(OS_MINOR)"
	@echo "KBUILD_CFLAGS: $(KBUILD_CFLAGS)"
	$(MAKE) -C $(KERNELDIR) M=$(PWD) modules

install:
	@mkdir -p $(INSTALLDIR)
	@echo "INSTALL $(INSTALLDIR)/specDriver.ko"
	@install -m 755 specDriver.ko $(INSTALLDIR)
	@echo "INSTALL /usr/include/specDriver/driver/specDriver.h"
	@mkdir -p /usr/include/specDriver/driver
	@install -m 644 specDriver.h /usr/include/specDriver/driver
	@echo "INSTALL /etc/udev/rules.d/99-spec.rules"
	@install -m 644 99-spec.rules /etc/udev/rules.d

uninstall:
	@echo "UNINSTALL $(INSTALLDIR)/specDriver.ko"
	@rm -f $(INSTALLDIR)/specDriver.ko
	@echo "UNINSTALL /usr/include/specDriver/driver/specDriver.h"
	@rm -rf /usr/include/specDriver/driver
	@echo "UNINSTALL /etc/udev/rules.d/99-spec.rules"
	@rm /etc/udev/rules.d/99-spec.rules

clean:
	rm -f *.o *.ko *.mod.c .*.cmd *.unsigned *.order *.symvers
	rm -rf .tmp_versions 
