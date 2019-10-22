MCRcon
======

This library provides a straightforward implementation of Minecraft's
`Rcon protocol`_ in Python to provide a client for handling Remote Commands
(RCON) to a Minecraft server.

.. _Rcon protocol: http://wiki.vg/Rcon

Installation
############

The library is availble on PYPI and can be installed with pip::

    pip install mcrcon

Usage
#####

The recommend way to run this client is using the python 'with' statement.
This ensures that the socket is correctly closed when you are done with it
rather than being left open.

Example::

    In [1]: from mcrcon import MCRcon
    In [2]: with MCRcon("10.1.1.1", "sekret") as mcr:
       ...:     resp = mcr.command("/whitelist add bob")
       ...:     print(resp)

While you can use it without the 'with' statement, you have to connect
manually, and ideally disconnect::

    In [3]: mcr = MCRcon("10.1.1.1", "sekret")
    In [4]: mcr.connect()
    In [5]: resp = mcr.command("/whitelist add bob")
    In [6]: print(resp)
    In [7]: mcr.disconnect()

Command Line Usage
##################

You can connect from the console with commands like the following::

    python -m mcrcon 10.1.1.1 sekret

The output from `python -m mcrcon --help` is provided here::

    usage: mcrcon.py [-h] [-p PORT] [-t] HOST PASSWORD
    
    connect to and use Minecraft Server remote console protocol
    
    positional arguments:
      HOST                  the host to connect to
      PASSWORD              the password to connect with
    
    optional arguments:
      -h, --help            show this help message and exit
      -p PORT, --port PORT  the port to connect to
      -t, --tls             connect to the server with tls encryption
