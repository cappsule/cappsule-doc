Usage
=====

Launch of the daemon
--------------------

The daemon must be launched manually if ``systemd`` isn't installed: ::

    sudo /usr/local/cappsule/usr/bin/daemon

The ``--debug`` option can be use to launch the daemon in foreground.


Launch of cappsules
-------------------

The launch of a cappsule is done with the ``virt`` command. For instance, to
launch ``bash``: ::

    /usr/local/cappsule/usr/bin/virt exec --no-gui --policy unrestricted bash

The ``--no-gui`` option disables the usage of the graphical interface, and
``--policy`` specifies the name of the policy to be used.

If the policy isn't specified in the command line options, the policy is derived
from the binary name. Policies are ``.json`` files stored in the
``/usr/local/cappsule/etc/cappsule/policies/`` folder.

.. note:: It's recommended to modify the ``PATH`` variable of the shell to avoid
   to specify the full path of ``virt`` each time. For bash, modify
   ``~/.bashrc`` file: ::

        PATH=$PATH:/usr/local/cappsule/usr/bin

Usage examples: ::

    virt exec --no-gui --policy unrestricted bash -i
    virt exec firefox
    virt exec --policy firefox firefox
    virt exec evince


Log files
---------

Log files are created in the ``/var/log/cappsule/`` folder.
