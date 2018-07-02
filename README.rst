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
   Name of the configuration file below
   files/openvpn/server-config. This is the main OpenVPN configuration file.


OPTIONAL PARAMETERS
-------------------
srcdir
   Directory that contains additional files for the server
   configuration. The directory is relative to files/openvpn/.
   If not specified, defaults to "server-generic". This directory
   contains usually the following files: ca.crt, server.crt and
   server.key. It can also contain a dh4096.pem file containing DH
   parameters. Additionally a sub directory "ccd" can be present that
   contains client specific configuration files.


EXAMPLES
--------

.. code-block:: sh

    # Use the config file ipv6-server.conf
    __ungleich_openvpn_server --config ipv6-server

    # Use a customer directory for server files
    # Will copy files from files/openvpn/custom-server-dir to /etc/openvpn
    __ungleich_openvpn_server --config custom-server \
        --srcdir custom-server-dir


AUTHORS
-------
ungleich <foss--@--ungleich.ch>


COPYING
-------
Copyright \(C) 2018 ungleich glarus ag. You can redistribute it
and/or modify it under the terms of the GNU General Public License as
published by the Free Software Foundation, either version 3 of the
License, or (at your option) any later version.
