White Label
===========

Our Name Server offer includes 4 Anycast DNS servers.
Below you will find a recommendation how such a DNS setup might look like.
We recommend 4 different domains.

DNS Records
-----------

::

    # ns.example.ch
    ns.example.ch   IN A        185.136.96.77
    ns.example.ch   IN AAAA     2a06:fb00:1::1:77
    example.ch      IN NS       ns.example.ch
    example.ch      IN NS       ns.example.li
    example.ch      IN NS       ns.example.net
    example.ch      IN NS       ns.example.org

    # ns.example.li
    ns.example.li   IN A        185.136.97.77
    ns.example.li   IN AAAA     2a06:fb00:1::2:77
    example.li      IN NS       ns.example.ch
    example.li      IN NS       ns.example.li
    example.li      IN NS       ns.example.net
    example.li      IN NS       ns.example.org

    # ns.example.net
    ns.example.net  IN A        185.136.98.77
    ns.example.net  IN AAAA     2a06:fb00:1::3:77
    example.net     IN NS       ns.example.ch
    example.net     IN NS       ns.example.li
    example.net     IN NS       ns.example.net
    example.net     IN NS       ns.example.org

    # ns.example.org
    ns.example.org  IN A        185.136.99.77
    ns.example.org  IN AAAA     2a06:fb00:1::4:77
    example.org     IN NS       ns.example.ch
    example.org     IN NS       ns.example.li
    example.org     IN NS       ns.example.net
    example.org     IN NS       ns.example.org

.. warning:: This example requires glue records, see below for more information

.. hint:: DNS changes can take up to 24 hours.

With the setup above, your customers can use the following DNS servers.

::

    ns.example.ch
    ns.example.li
    ns.example.net
    ns.example.org

Glue Records
------------

Glue records are required if a domain is using nameservers as a suddomain of itself.

::

    $ dig example.net ns +short
    ns.example.ch.
    ns.example.li.
    ns.example.net.      <-- Same domain, glue record necessary
    ns.example.org.

In this example the following glue records are required.
Please contact your domain registrar to set up Glue Records.
If you have registered the domain through us, we can set up everything for you.

::

    ns.example.net 185.136.98.77
    ns.example.net 2a06:fb00:1::3:77

.. hint:: The same for the other three domains.