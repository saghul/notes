
.. _beaglebone:

BeagleBone Black
================

`Official Wiki <http://elinux.org/Beagleboard:BeagleBoneBlack>`_


Fix second boot on FreedomBox
-----------------------------

As part of its first boot, FreedomBox uses the ``flash-kernel`` utility to update the
kernel on the BBB. Unfortunately this doesn't work. To prevent this from happening
create the follopwing empty file before the first boot: ``/var/freedombox/dont-tweak-kernel``

