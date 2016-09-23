Graphical interface
===================

The GUI is the only part of Cappsule which hasn't been developed from scratch,
but forked from Qubes OS because they share the very same goals.

The fork  is a merge of the different Qubes OS GUI repositories into a single
`one <https://github.com/cappsule/cappsule-gui>`_:

- https://github.com/QubesOS/qubes-gui-daemon
- https://github.com/QubesOS/qubes-gui-common
- https://github.com/QubesOS/qubes-gui-agent-linux

Some features (copy/paste and sound support) aren't implemented.



GUI support
-----------

Requirements
~~~~~~~~~~~~

GUI support requires ``Xorg`` to be launched from Qubes OS wrapper
(``/usr/local/cappsule/usr/bin/X-wrapper-qubes``) in order to load a shared
library.

Originally, Cappsule used ``LightDM`` to launch the wrapper, but it doesn't
support it anymore. ``GDM`` seems more convenient nowadays because it doesn't
require ``Xorg`` to run as root. The wrapper is launched from
``/usr/lib/xorg/Xorg.wrap``.


No GUI support
~~~~~~~~~~~~~~

GUI support is optional. Cappsules can be run without GUI support thanks to the
server version, or using the following command lines.

Launch ``daemon`` without GUI support: ::

  /usr/local/cappsule/usr/bin/daemon --no-gui

Launch a new cappsule without GUI support (for command line application for
instance): ::

  virt exec --no-gui bash



Window border colors
--------------------

Window manager don't implement window border color feature, thus they have to be
patched in order to support it.

Ubuntu 16 default window manager is ``Unity``. We chosed to support the previous
window manager, ``metacity``, which is provided by the
``gnome-session-flashback`` package. The patch can be found in the `GUI
repository <https://github.com/cappsule/cappsule-gui/metacity>`_.

Si le gestionnaire de fenêtre n'est pas ``Metacity``, les contributions sont
les bienvenues.
