
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


Install all build dependencies for a source package
---------------------------------------------------

Sometimes you can't use ``apt-get build-dep`` (the first time you are building the package for example). We are
going to use ``mk-build-deps`` from the ``devscripts`` package (``equivs`` also needs to be installed.

::

    mk-build-deps -ir -t "apt-get -qq -y --no-install-recommends"


Put a package on hold
---------------------

Putting a package on hold:

::

    sudo apt-mark hold package

Putting a package out of hold:

::

    sudo apt-mark unhold package

