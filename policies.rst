Policies
========

We call `policies` the rules applied to filter access to the filesystem and the
network. They are stored in ``.json`` files located in the
``/usr/local/cappsule/etc/cappsule/policies/`` folder. They can be reloaded by
sending a ``SIGHUP`` signal to the ``daemon`` process: ::

  sudo kill -s SIGHUP $(pidof daemon)

Note that even if the filesystem policies are too permissive, attackers can't
write to the host filesystem.

The list of default policies can be found in the `tools repository
<https://github.com/cappsule/cappsule-tools/blob/master/policies>`_.



GUI
---

The border colors of a window are specified by the ``color`` key. For instance:
::

   "color": "maroon",



Network
-------

Network rules allow TCP and UDP trafic. For instance: ::

    "network": {
        "udp": [
            "8.8.8.8:53"
        ],

        "tcp": [
            "*:80-81",
            "12.34.13.37:*",
            "192.168.234.0-192.168.234.255:*"
        ]
    }



Filesystem
----------

The rules granting access to the host filesystem are specified in the
``filesystem`` section: ::

    "filesystem": {
        "/usr/bin/id": "rx",
        "/etc/passwd": "r",
        "/@HOME@/*": "r",
        "/@HOME@/.bash_history": "w",
        "/lib/x86_64-linux-gnu/**": "r",
        "/@HOME@/.cache/mozilla/**/": "r",
    }

Dans l'exemple précédent :

* ``/usr/bin/id``: read and exec.
* ``/etc/passwd``: read only.
* ``/@HOME@/*``: every file inside the ``~/`` folder of the user who launched
  the cappsule is readable. Files in subfolders aren't available.
* ``/@HOME@/.bash_history``: write-only.
* ``/lib/x86_64-linux-gnu/**``: everything in the ``/lib/x86_64-linux-gnu/`` and
  its subfolders is readable.
* ``/@HOME@/.cache/mozilla/**/``: everything in the ``~/.cache/mozilla/**/``
  folder and in its subfolders is readable and listable.


Shared folders
~~~~~~~~~~~~~~

Shared folders between the cappsule and the host filesystem are specified in the
``shared`` section: ::

    "shared": [
        "/@HOME@/Downloads"
    ]

Shared folders can also be specified by the command line through the ``-f`` or
``--miscfs`` switches: ::

  --miscfs /root:overlay
