
.. _debian:

Debian
======

Some Debian tips and tricks.


Check for obsolete packages
---------------------------

Obsolete packages are those which cannot be installed from any of the configured
repositories.

::

    aptitude search ?obsolete

I have no idea if this can be accomplished with plain apt-get.


Override DNS resolvers received over DHCP
-----------------------------------------

If you want to override the DNS resolvers received over DHCP, add the following to
``/etc/dhcp/dhclient.conf``

::

    interface "eth0" {
        supersede domain-name-servers 8.8.8.8, 8.8.4.4;
    }

Adjust accordingly.

