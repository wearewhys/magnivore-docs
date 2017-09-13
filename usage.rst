Usage
======

.. highlight:: bash

Magnivore keeps track of foreign keys and other data, so you must init
magnivore before starting a migration session::

    magnivore init

A session here is a migration process that occurs with the same dataset against
the same database. If your dataset or database change, you will need to restart
the session and every dataset/database should have its own session.

Workarounds to this limitation are explained later in the documentation.

Migrating
#########

Use the run command and the path of the rules files that you want to use to
perform a migration::

    magnivore run myrules.json


Increase verbosity with -v::

    magnivore run myrules.json -vvvv


Version
#######
You can check magnivore's version::

    magnivore hello
