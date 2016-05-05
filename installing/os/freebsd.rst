FreeBSD
==========

This guide is for FreeBSD 10.1-RELEASE. It should work, with slight modifications, for all other relatively modern versions. 

Make sure you are up to date, by running:

.. code:: bash

  freebsd-update fetch
  freebsd-update install

Install Redis:

.. code::

  pkg install redis

Follow the regular steps to run Redis at the runlevel, and start it.

Install gcc5:

.. code::

    pkg install gcc5

Install Node:

.. code::

    pkg install node

Clone NodeBB repo (this assumes you have `git` installed, otherwise use `pkg` to install it):

.. code:: bash

    git clone -b v1.x.x https://github.com/NodeBB/NodeBB.git

To track the latest weekly build of NodeBB, substitute `weekly` in place of `v1.x.x`.

Enter directory:

.. code:: bash

    cd nodebb

Install dependencies:

.. code:: bash

    npm install

Run interactive installation:

.. code:: bash

    ./nodebb setup

You may leave all of the options as default.

You are finished! After the installation, run:

.. code:: bash

    ./nodebb start

Visit your forum at ``http://FQDN:4567/`` to finish configuration and setup. FQDN is the server fully qualified domain name.
