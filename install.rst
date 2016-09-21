Install
=======

.. warning::

   **Ubuntu 16 is the only distro on which we extensively tested Cappsule**,
   and a few modifications might be required to support other distros. The
   projet should nonetheless works on Ubuntu 14 and Debian.


Requirements
------------

A CPU which supports Intel VT-x and EPT is required: ::

  $ grep -o 'vmx\|ept' /proc/cpuinfo | sort -u
  ept
  vmx

Install
-------

::

    sudo dpkg --force-confnew -i cappsule.deb

The ``--force-confnew`` option ensures that configuration files are effectively
updated if a new version of the files inside the package are different.


Installed files
~~~~~~~~~~~~~~~

All files are installed in ``/usr/local/cappsule/`` folder, except for:

* ``/lib/systemd/system/cappsule.service``: ``systemd`` init file.
* ``/etc/rsyslog.d/30-cappsule.conf``:  ``rsyslog`` rules to redirect network
  traffic filtered by ``iptables`` into Cappsule log files.
* ``/etc/lightdm/lightdm.conf.d/cappsule.conf``: modification of the command
  used to launch ``X`` at the start up of the user session.



Uninstall
---------

::

    sudo apt purge cappsule
