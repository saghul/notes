
.. _linux:

Linux
=====

Or GNU/Linux.


Map Caps Lock to Control
------------------------

But not the other way around. Put this in ``.profile`` or ``.bashrc``:

::

    setxkbmap -layout us -option ctrl:nocaps


LUKS
----

Simple use, for external devices, using a passphrase.
For more options `check this out <https://wiki.archlinux.org/index.php/Dm-crypt/Encrypting_an_entire_system>`_.

Creating a LUKS volume
^^^^^^^^^^^^^^^^^^^^^^

::

     cryptsetup -v luksFormat /dev/sdaX
     cryptsetup open /dev/sdaX LUKS001
     mkfs -t ext4 /dev/mapper/LUKS001
     cryptsetup close LUKS001

Mounting a LUKS volume
^^^^^^^^^^^^^^^^^^^^^^

::

     cryptsetup open /dev/sdaX LUKS001
     mount -t ext4 /dev/mapper/LUKS001 /mnt/usb

Unmounting a LUKS volume
^^^^^^^^^^^^^^^^^^^^^^^^

::

    umount /mnt/usb
    cryptsetup close LUKS001


Creating a 'fake' webcam device
-------------------------------

For testing, one might need some 'fake' webcam, here is how to do it.

* Install `v4l2loopback <https://github.com/umlaeute/v4l2loopback>`_ - this is
  typically available as a package in your distro

* Load the kernel module with the amount of virtual video devices you want:

::

    sudo modprobe v4l2loopback devices=X

* Get GStreamer 0.10 - looks like 1.0 doesn't work well with the videotestsrc plugin
  `see here <https://github.com/umlaeute/v4l2loopback/issues/83>`_

* Launch GStreamer as follows:

::

    gst-launch-0.10 -v videotestsrc pattern=snow ! "video/x-raw-yuv,width=640,height=480,framerate=15/1,format=(fourcc)YUY2" ! v4l2sink device=/dev/videoX

The `pattern` can be a number between 0 and 16 or the name of a pattern.
More examples `here <https://github.com/umlaeute/v4l2loopback/wiki/Gstreamer>`_.
