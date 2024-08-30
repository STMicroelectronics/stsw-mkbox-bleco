Overview
********
This application provides a simple method to upgrade the firmware for
the BLE chip present on
[STEVAL-MKBOXPRO](https://www.st.com/en/evaluation-tools/steval-mkboxpro.html)
board.

It is based on the BlueNRG-LPS UART bootloader protocol explained in `AN5471`_ .

Getting Started
***************

Please make sure you have a proper Zephyr development environment. Follow the official
[Zephyr Getting Started Guide](https://docs.zephyrproject.org/latest/getting_started/index.html).

Then open a shell and run the `Zephyr Environment Scripts`_
in order to setup the proper environment variables.

Finally clone the STSW-MKBOX-BLECO repo:

.. code-block:: console

   # clone the STSW-MKBOX-BLECO repo somewhere
   $ cd /tmp
   $ git clone https://github.com/STMicroelectronics/stsw-mkbox-bleco.git
   $ cd stsw-mkbox-bleco/

Console
*******

The application requires a SensorTile.box PRO board connected to the PC through USB.

To run this app the console is not strictly needed, but might be useful.
Following is an example for minicom.

.. code-block:: console

   $ minicom -D <tty_device> -b 115200

Replace `<tty_device>` with the correct device path automatically created on
the host after the SensorTile.box Pro board gets connected to it,
usually `/dev/ttyUSB{x}` or `/dev/ttyACM{x}` (with x being 0, 1, 2, ...).
The ``-b`` option sets baud rate ignoring the value from config.

Building and Running
********************

To build and flash the application on the SensorTile.box PRO use following commands:

.. code-block:: console

   $ west build -b sensortile_box_pro ble_fw_upg_app/
   $ west flash

Please note that flashing the board requires a few preliminary steps to put the board
in DFU mode, as described in `SensorTile.box PRO DFU flashing`_.

After flashing, the app starts and asks the user to acknowledge the f/w update on console.
User should press `y` or `Y` to proceed in upgrading the BLE f/w.

 .. code-block:: console

    Start BLE f/w update (press Y to proceed):

Nevertheless it is not strictly necessary to use the console, as the user may also acknowledge
the f/w update pressing the User `BT2 button`_ and check on user manual and/or schematic to
see where the button is located and how it works.

LEDs status
-----------

The blue LED blinks three times with 200ms interval to indicate the procedure is starting.
Then blue LED start blinking very fast to indicate the BLE flash activity is on going.

After BLE flashing is complete:

- If status is OK the green LED blinks three times with 200ms interval and remains on.
- If flashing failed the red LED blinks three times with 200ms interval and remains on.

Console messages
----------------

To properly see messages on your terminale emulatore you may also need to set lineWrap to on.
In case of minicom just enter the menu with `Ctrl-A Z` an then press `W`.

The app outputs following messages.

 .. code-block:: console

    SensorTile.box Pro BLE f/w upgrade
    bootloader activated!
    ble bootloader version is 4.0
    MASS ERASE ok
    ..............................................................................................
    ..............................................................................................
    ..............................................................................................
    ..............................................................................................
    ..............................................................................................
    ..............................................................................................
    ..............................................................................................
    ............................................
    BLE f/w upgrade ok

References
**********

.. target-notes::

.. _AN5471:
   https://www.st.com/resource/en/application_note/an5471-the-bluenrglp-bluenrglps-uart-bootloader-protocol-stmicroelectronics.pdf

.. _Zephyr Environment Scripts:
   https://docs.zephyrproject.org/latest/develop/env_vars.html#zephyr-environment-scripts

.. _SensorTile.box PRO DFU flashing:
   https://docs.zephyrproject.org/latest/boards/st/sensortile_box_pro/doc/index.html#dfu-flashing

.. _BT2 button:
   https://docs.zephyrproject.org/latest/boards/st/sensortile_box_pro/doc/index.html#connections-and-ios
