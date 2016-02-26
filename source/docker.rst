
.. _docker:

Docker
======

The container technology everyone talks about. Website_.


Using official Docker on Debian Sid
-----------------------------------

In order to use the latest (and greatest?) version it's best to use the repositories
provided by Docker. As root:

::

     apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
     echo "deb https://apt.dockerproject.org/repo debian-stretch main" > /etc/apt/sources.list.d/docker.list
     apt-get update
     apt-get install docker-engine


Using OverlayFS as the storage backend
--------------------------------------

The default storage backend on Debian seems to be `devicemapper` using a loop file. If
you want to use OverlayFS, a systemd drop-in file is needed. Create a file in
``/etc/systemd/system/docker.service`` with the following content:

::

    [Service]
    ExecStart=
    ExecStart=/usr/bin/docker daemon -H fd:// --graph="/storage/docker" --storage-driver=overlay


.. _Website: http://docker.io/

