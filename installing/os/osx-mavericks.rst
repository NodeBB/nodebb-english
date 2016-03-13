OSX Mavericks
==========

Required Software
---------------------

First, install the following programs:

* http://nodejs.org/
* http://brew.sh/




Running NodeBB
---------------------

Install redis with homebrew:

.. code::

  brew install redis

Start redis server, in your terminal enter:

.. code::

  redis-server

Clone NodeBB repo:

.. code:: bash

    git clone -b v1.0.0 https://github.com/NodeBB/NodeBB.git

You'll want to replace ``v1.0.0`` with the (`latest stable version <https://github.com/NodeBB/NodeBB/releases>`_), or ``v1.x.x`` if you'd like
to set up the latest weekly build of NodeBB.

Enter directory:

.. code:: bash

    cd NodeBB

Install dependencies:

.. code:: bash

    npm install

Run interactive installation:

.. code:: bash

    ./nodebb setup

You may leave all of the options as default.

And you're done! After the installation, run

.. code:: bash

    ./nodebb start

You can visit your forum at ``http://localhost:4567/``


