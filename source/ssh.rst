
.. _ssh:

SSH
===

Using a jump host
-----------------

::

    $ ssh -o ProxyCommand="ssh -W %h:%p firewall.example.com" server2.example.org

or

::

    $ ssh -tt firewall.example.com ssh -tt server2.example.org

Source `here <https://en.wikibooks.org/wiki/OpenSSH/Cookbook/Proxies_and_Jump_Hosts#Jump_Hosts_--_Passing_through_a_gateway_or_two>`_.
