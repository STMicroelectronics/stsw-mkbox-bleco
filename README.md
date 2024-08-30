# SensorTile.box controller-only f/w images

![latest tag](https://img.shields.io/github/v/tag/STMicroelectronics/stsw-mkbox-bleco.svg?color=brightgreen)

# Overview

SensorTile.box is a family of ready-to-use programmable wireless box kits
equipped with a Bluetooth Low Energy SoC. acting as a network coprocessor,
for developing any IoT application based on remote data gathering and evaluation.

This repo contains [BLE Controller-only firmware](#ctrl-only-fw) images, and a
[Zephyr](https://github.com/zephyrproject-rtos) application to upload them, for
the following SensorTile.box family boards:

- [STEVAL-MKBOXPRO](https://www.st.com/en/evaluation-tools/steval-mkboxpro.html)
- [STEVAL-MKSBOX1V1](https://www.st.com/en/evaluation-tools/steval-mksbox1v1.html)

This repo contains software which is distributed as part of the
[STSW-MKBOX-BLECO](https://www.st.com/en/embedded-software/stsw-mkbox-bleco.html)
package.

# Bluetooth protocol stack

There are 3 main layers that together constitute a full Bluetooth Low Energy protocol stack:

- **Host**: This layer sits right below the application, and is comprised of multiple
 (non real-time) network and transport protocols enabling applications to communicate
 with peer devices in a standard and interoperable way.

- **Controller**: The Controller implements the Link Layer (LE LL), the low-level
  real-time protocol which provides, in conjunction with the Radio Hardware,
  standard-interoperable over-the-air communication.
  The LL schedules packet reception and transmission, guarantees the delivery of data,
  and handles all the LL control procedures.

- **Radio Hardware**: Hardware implements the required analog and digital baseband
functional blocks that permit the Link Layer firmware to send and receive in the
2.4GHz band of the spectrum.

The BLE SoC may be programmed in two different ways, according to how many
protocol stack layers are present. The following sections cover this topic.

## Host/Controller firmware

The network coprocessor firmware implements all three layers. The
application layer running on the MCU interfaces directly with the Host layer
running in the coprocessor.

This is the _factory default_ configuration selected for the kit.

## <a id="ctrl-only-fw"></a> Controller-only firmware

The network coprocessor firmware implements up to the controller layer only,
leaving outside the host layer.
This is needed by some systems, like [Zephyr RTOS](https://www.zephyrproject.org/),
which already offer their own Host solution (see for example the
[Zephyr Bluetooth Stack](https://docs.zephyrproject.org/latest/connectivity/bluetooth/bluetooth-arch.html)
for getting more specific information).

Hence a standard SensorTile.box board which runs, for example, Zephyr BLE subsystem (or
others based on the same concept), requires replacing the BLE SoC default firmware
with a controller-only one.

# Update the BLE SoC firmware

Currently the Zephyr RTOS supports the following SensorTile boards:

- [Zephyr STEVAL-MKBOXPRO](https://docs.zephyrproject.org/latest/boards/st/sensortile_box_pro/doc/index.html)
- [Zephyr STEVAL-MKSBOX1V1](https://docs.zephyrproject.org/latest/boards/st/sensortile_box/doc/index.html)

This repo contains a Zephyr application under
[ble_fw_upg_app](https://github.com/STMicroelectronics/stsw-mkbox-bleco/tree/master/ble_fw_upg_app) directory,
where you can also find a README file which explains the usage,
which can be used to upload the ble firmware on sensortile_box_pro board

------

**More information: [http://www.st.com](http://st.com/MEMS)**

**Copyright (C) 2024 STMicroelectronics**

