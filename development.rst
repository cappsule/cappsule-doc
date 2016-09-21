Development
===========

.. warning::

   **Ubuntu 16 is the only distro on which we extensively tested Cappsule**,
   and a few modifications might be required to support other distros. The
   projet should nonetheless works on Ubuntu 14 and Debian.



Sources
-------

The source code of the different parts of the project are in different git
repositories. They can be checked out with the following command lines: ::

    mkdir src/
    git clone https://github.com/cappsule/hypervisor.git src/hv
    git clone https://github.com/cappsule/userland.git src/userland
    git clone https://github.com/cappsule/gui.git src/userland/devices/gui
    git clone https://github.com/cappsule/tools.git tools

Coding style
~~~~~~~~~~~~

The coding style of the whole project is the same than the Linux Kernel: `Linux
kernel coding style <https://www.kernel.org/doc/Documentation/CodingStyle>`_.



Build
-----

The build is done with a standard ``Makefile`` system: ::

    make -C src/hv
    make -C src/userland

Dependencies
~~~~~~~~~~~~

List of dependencies (Ubuntu packages, adapt it depending of the distro used for
the developement) for the different parts of the project:

- documentation : ``python-sphinx``
- hv : ``linux-headers-generic``
- userland : ``libssl-dev`` ``libjson-c-dev`` ``libcmocka-dev`` ``libcap-dev``
  ``pkg-config`` ``libfuse-dev``
- gui : ``xserver-xorg-dev`` ``libxcomposite-dev`` ``libxdamage-dev``
  ``libxtst-dev`` ``libxxf86dga-dev`` ``libcairo2-dev``
  ``xserver-xorg-video-dummy``
- debian package : ``fakeroot``

Or in a single command line: ::

    sudo apt install git libssl-dev libjson-c-dev libcmocka-dev libcap-dev \
    libfuse-dev xserver-xorg-dev libxcomposite-dev libxdamage-dev libxtst-dev \
    libxxf86dga-dev libcairo2-dev xserver-xorg-video-dummy fakeroot \
    python-sphinx linux-headers-generic

Environment variables
~~~~~~~~~~~~~~~~~~~~~

Somes environment variables influence the build:

- ``NOGUI=1`` : the graphical part isn't built.
- ``RELEASE=1`` : some debug messages aren't included, and the kernel module is
  slightly obfuscated.

Thus, to build the userland part without the graphical part: ::

    NOGUI=1 make -C src/userland



Distribution and installation
-----------------------------

The script ``tools/build_package.py`` builds a debian package, and the
installation is done with ``dpkg``: ::

    ./tools/build_package.py -f ./cappsule.deb
    sudo dpkg --force-confnew -i ./cappsule.deb

The ``--force-confnew`` option ensures that configuration files are effectively
updated if a new version of the files inside the package are different.

The package can also be built without the graphical part with the
``--config=server`` option: ::

    ./tools/build_package.py -f ./cappsule.deb



Usage
-----

Launch of the daemon: ::

    sudo /usr/local/cappsule/usr/bin/daemon --debug

Encapsulation of applications: ::

    /usr/local/cappsule/usr/bin/virt exec id
    /usr/local/cappsule/usr/bin/virt exec firefox



Recommended development environment
-----------------------------------

It's convenient to use a virtual machine to test modifications introduced in the
source code. Since VMware handles quite well `nested virtualization`, it's the
recommanded hypervisor even if it isn't free. The CPU option `Virtualize Intel
VT-x/EPT or AMD-V/RVI` must be enabled.

The script ``tools/upload.sh`` creates the debian package, uploads it on a VM
before extracting it, and launches the daemon.
