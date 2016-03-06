
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

