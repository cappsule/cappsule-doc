Network
=======

In the cappsule
---------------

When a cappsule is launched, the ``netclient`` process creates a new TUN
interface and configures it with settings similar to this: ::

    ifconfig tun-caps-0 [ip] pointopoint [gateway]
    ifconfig tun-caps-0 netmask 255.255.255.0
    route add default gw [gateway] dev tun-caps-0

with:

- ``ip``: 172.17.0. ``id`` by default
- ``gateway``: 172.17.0. ``id+1`` by default



In the host
-----------

A new ``netserver`` process is created when a cappsule is launched. It also
creates a ``TUN`` interface with the following configuration: ::

    ifconfig tun-caps-[id] [gateway] pointopoint [ip]
    ifconfig tun-caps-[id] netmask 255.255.255.255

with:

- ``id`` : the cappsule ``id``
- ``ip`` : 172.17.0. ``id`` by default
- ``gateway`` : 172.17.0. ``id+1`` by default

The daemon enables routing and ``NAT`` in the host.
