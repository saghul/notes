
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

