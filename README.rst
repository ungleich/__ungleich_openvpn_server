cdist-type__ungleich_openvpn_server(7)
======================================

NAME
----
cdist-type__ungleich_openvpn_server - Configure an OpenVPN Server


DESCRIPTION
-----------
This cdist type allows you to create and maintain OpenVPN servers.
It assumes existence of the directory files/openvpn/ and various
subdirectories (see below).



REQUIRED PARAMETERS
-------------------
config
   Name of the configuration file below files/openvpn/


OPTIONAL PARAMETERS
-------------------
srcdir
   Directory that contains additional files for the server
   configuration. The directory is relative to files/openvpn/.
   If not specified, defaults to "server-generic". This directory
   contains usually the following files: ca.crt, server.crt and
   server.key. Additionally a sub directory "ccd" can be present that
   contains client specific configuration files.


source
   If supplied, copy this file from the host running cdist to the target.
   If not supplied, an empty file or directory will be created.
   If source is '-' (dash), take what was written to stdin as the file content.

MESSAGES
--------
chgrp <group>
   Changed group membership
chown <owner>
   Changed owner
chmod <mode>
   Changed mode
create
   Empty file was created (no --source specified)
remove
   File exists, but state is absent, file will be removed by generated code.
upload
   File was uploaded


EXAMPLES
--------

.. code-block:: sh

    # Create  /etc/cdist-configured as an empty file
    __file /etc/cdist-configured
    # The same thing
    __file /etc/cdist-configured --state present
    # Use __file from another type
    __file /etc/issue --source "$__type/files/archlinux" --state present
    # Delete existing file
    __file /etc/cdist-configured --state absent
    # Supply some more settings
    __file /etc/shadow --source "$__type/files/shadow" \
       --owner root --group shadow --mode 0640 \
       --state present
    # Provide a default file, but let the user change it
    __file /home/frodo/.bashrc --source "/etc/skel/.bashrc" \
       --state exists \
       --owner frodo --mode 0600
    # Check that the file is present, show an error when it is not
    __file /etc/somefile --state pre-exists
    # Take file content from stdin
    __file /tmp/whatever --owner root --group root --mode 644 --source - << DONE
        Here goes the content for /tmp/whatever
    DONE


AUTHORS
-------
Nico Schottelius <nico-cdist--@--schottelius.org>


COPYING
-------
Copyright \(C) 2011-2013 Nico Schottelius. You can redistribute it
and/or modify it under the terms of the GNU General Public License as
published by the Free Software Foundation, either version 3 of the
License, or (at your option) any later version.
