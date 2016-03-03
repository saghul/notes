
.. _c:

C
=

Compilation with musl
---------------------

First install the musl-gcc wrapper (on Debian):

::

    apt-get install musl-tools

Now set some environment variables:

::

    export CC=musl-gcc
    export LINK=musl-gcc
    export CFLAGS=-static

That's it, you can now compile your library and it will be linked with musl instead of
glibc.

