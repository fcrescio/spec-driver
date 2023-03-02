# SPEC Driver

PCIe kernel driver designed for Simple PCIe Carrier Cards with FPGA.

Meant to be used with [YARR-PCIe firmware](https://gitlab.cern.ch/YARR/yarr-pcie/yarr-pcie-fw) and [YARR software](https://gitlab.cern.ch/YARR/YARR).

## How to install

Driver only needs to be installed once and should load automatically afterwards.

```
cd src
make
sudo make install
sudo make depmod
modprobe -v specDriver
```

## Troubleshooting

- Sometimes during kernel updates custom drivers do not get migrated. If the driver is not loaded automatically after a kernel update, re-install the driver.
