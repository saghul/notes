
.. _raspberrypi:

Raspberry Pi
============

The tiny computer everyone loves.


Extra current for the USB ports (B+/2 only)
-------------------------------------------

Raspberry Pi models B+ and 2 are able to supply up to 1.2A over USB using a little trick.
This allows us to connect portable hard drives without using powered USB hubs.

Edit ``/boot/config.txt`` and add the following:

::

    # extra power for USB ports
    max_usb_current=1

.. warning::
    Do this at your own risk. A good power supply giving a stable current of 2A is required.

