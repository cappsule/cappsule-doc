Introduction
============

`Cappsule <https://cappsule.github.io>`_ is an hypervisor which virtualizes any
software on-the-fly (e.g.: web browser, office suite, media player) into
lightweight VMs called cappsules. Attacks are confined into the cappsules and
don't have any impact on the host OS. Applications don't need to be repackaged,
and their usage remain the same for the end user: it's completely
imperceptible. Moreover, the OS doesn't need to be reinstalled nor modified.


Features
--------

Security
~~~~~~~~

VMs can't access to hardware thanks to hardware virtualization (Intel VT-x and
EPT). Access to the host memory is also impossible.



Lightweight VMs called cappsules
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Cappsules run a copy of the host kernel, which is `copy-on-write
<https://en.wikipedia.org/wiki/Copy-on-write>`_.  It means that the memory isn't
duplicated until it's modified.



On-the-fly virtualization
~~~~~~~~~~~~~~~~~~~~~~~~~

Cappsules don't boot a full system: they start their execution on a copy of the
host system memory (that we called `snapshot`). The snapshot is only done once,
during the initialization of the hypervisor.



Applications don't need to be repackaged
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Applications use a copy on write view (`overlayfs
<https://en.wikipedia.org/wiki/OverlayFS>`_) of the host filesystem. Any
application installed in the host can be launched into a cappsule.

Sensitive pieces of data aren't available to the cappsules thanks to the
filesystem policies.



It's completely imperceptible
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The `Qubes OS GUI protocol <https://www.qubes-os.org/doc/gui/>`_ gives the
illusion that applications run in the same window manager.



The OS doesn't need to be reinstalled nor modified
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The hypervisor virtualizes the main OS using a concept called `Blue Pill
<https://en.wikipedia.org/wiki/Blue_Pill_(software)>`_. Joanna Rutkovswka was
the first to introduce this concept in `2006
<http://theinvisiblethings.blogspot.fr/2006/06/introducing-blue-pill.html>`_,
more than 10 years ago.
