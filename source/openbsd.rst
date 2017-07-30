
.. _openbsd:

OpenBSD
=======

Some OpenBSD tips and tricks.


Start a network interface
-------------------------

::

    sh /etc/netstart re0

Replace ``re0`` with the interface name.


Use a serial console for installation
-------------------------------------

At the boot prompt:

::

    > stty com0 115200
    > set tty com0

Adjust the baudrate accordingly.


Reload pf rules
---------------

::

    pfctl -f /etc/pf.conf -F all

The ``-F all`` part can be omitted if you don't want to flush the current rules.

