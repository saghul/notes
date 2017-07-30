
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


SMART
-----

Monitor the hard drives health with SMART. Full guide `here <https://wiki.archlinux.org/index.php/S.M.A.R.T.>`_.

Configuration
^^^^^^^^^^^^^

The following configuration will:

* Monitor all drives
* Except the ones in standby
* Run a short self-test every day between 2-3am, and an extended self test weekly on Saturdays between 3-4am
* Log temperature changes of 4 degrees or more, log when temp reaches 35 degrees, and log/email a warning when temp reaches 40
* Alert using `Pushover <https://pushover.net>`_


``/etc/smartd.conf``

::

    DEVICESCAN -a -n standby,q -s (S/../.././02|L/../../6/03) -W 4,35,40 -m root -M exec /usr/share/smartmontools/smartd-runner


``/etc/smartmontools/run.d/10pushover``

::

    #!/bin/bash

    # Send notification
    echo "$SMARTD_MESSAGE" | pushover-notify -t "SMART failure: $SMARTD_FAILTYPE"


``/usr/local/bin/pushover-notify``

::

    #!/usr/bin/env python

    import argparse
    import requests
    import sys

    APP_TOKEN = 'TODO'
    USER_KEY  = 'TODO'
    PUSHOVER_URL = 'https://api.pushover.net/1/messages.json'


    parser = argparse.ArgumentParser()
    parser.add_argument('-t', '--title', help='Title for the notification')
    args = parser.parse_args()

    title = args.title or ''
    data = sys.stdin.read()

    payload = {'token': APP_TOKEN, 'user': USER_KEY, 'title': title, 'message': data}
    requests.post(PUSHOVER_URL, data=payload)


CUPS
----

Sharing a printer without the drivers (raw)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following method facilitates sharing a printer in a network, without having the
drivers for it. This means the computers wantint to print on it will have to have
the drivers, but that's ok.

Install CUPS and configure it for remote access (run all these commands as root):

::

    apt install cups
    usermod -a -G lpadmin pi
    cupsctl --remote-admin --remote-any
    systemctl restart cups

Now open http://IP:631 in a browser and chick "add printer". Select the "Raw" make
and "Raw Queue" as the model.

Install the drivers on the client computer and add the remote printer. Done!

