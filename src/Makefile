
obj-m := specDriver.o
specDriver-objs := base.o int.o umem.o kmem.o sysfs.o ioctl.o

KERNELDIR ?= /lib/modules/$(shell uname -r)/build
INSTALLDIR ?= /lib/modules/$(shell uname -r)/extra
PWD := $(shell pwd)

default:
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
