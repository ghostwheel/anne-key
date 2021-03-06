Firmware for Anne Pro Keyboard written in Rust
==============================================

[![Travis Build Status](https://travis-ci.org/ah-/anne-key.svg?branch=master)](https://travis-ci.org/ah-/anne-key)

<img src="docs/images/ferris.png" width=30%/> <img src="docs/images/anne.jpg" width=50%/>


This is an alternative firmware for the [Anne Pro Keyboard](http://en.obins.net/anne-pro), with the goal of being more stable than the original firmware and adding extra features.

Status
------

This project is still under heavy development and probably not quite ready yet to serve as your only keyboard.

Working today:

- Basic keyboard functionality
- Bluetooth (as a keyboard)
- LED control (switching on/off, changing themes)
- USB charging
- Drop in replacement as a simple firmware update

Not yet implemented:

- USB
- Bluetooth communication with the Anne Pro App
- Media controls / special keys
- Uploading custom lighting settings
- Uploading custom keymaps
- Power Management
- BT setup mode with LEDs etc.

Community
---------

We hang out in the [Anne Pro Dev discord](https://discord.gg/ARQmrNn). Please observe the [Rust Code of Conduct](https://www.rust-lang.org/conduct.html) within our community.

Documentation
---------

There is some documentation on hardware [here](docs/hardware.md).

Flashing
--------

You can find the latest build on the [Releases page](https://github.com/ah-/anne-key/releases). Download `anne-key.dfu`.

Then you can either follow the [obins firmware update steps](http://en.obins.net/firmware) (click Update manual) or use `dfu-util`.

### dfu-util

First you'll need to [install dfu-util](https://docs.particle.io/faq/particle-tools/installing-dfu-util/core/).

To flash your Anne Pro connect via USB, then hold down the Esc button, press the little reset switch on the back and finally release Esc.

Now your keyboard is in DfuSe mode. It should show up in dfu-util:

```
$ dfu-util -l
dfu-util 0.9

...

Found DFU: [0483:df11] ver=0200, devnum=23, cfg=1, intf=0, path="20-2", alt=2, name="@BluetoothFlash  /0x1c000000/14*256 a,192*256 g", serial="057C37553731"
Found DFU: [0483:df11] ver=0200, devnum=23, cfg=1, intf=0, path="20-2", alt=1, name="@Internal Flash  /0x0c000000/64*256 a,192*256 g", serial="057C37553731"
Found DFU: [0483:df11] ver=0200, devnum=23, cfg=1, intf=0, path="20-2", alt=0, name="@Internal Flash  /0x08000000/64*256 a,192*256 g", serial="057C37553731"
```

Then you can flash your keyboard firmware:

```
$ dfu-util --alt 0 --intf 0 --download anne-key.dfu

...

file contains 1 DFU images
parsing DFU image 1
image for alternate setting 0, (1 elements, total size = 5104)
parsing element 1, address = 0x08004000, size = 5096
Download        [=========================] 100%         5096 bytes
Download done.
done parsing DfuSe file
```

And that's it. Press the reset button again to exit the bootloader and return to normal keyboard mode and you're done!

If you want to return to the original firmware you can flash the [original firmware](http://en.obins.net/firmware) with:

```
$ dfu-util --alt 0 --intf 0 --download "anne pro key 1.4.dfu"
```
