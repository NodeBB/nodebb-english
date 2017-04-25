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

    git clone -b v1.x.x https://github.com/NodeBB/NodeBB.git

To track the latest weekly build of NodeBB, substitute `weekly` in place of `v1.x.x`.

Enter directory:

.. code:: bash

    cd NodeBB

Install dependencies:

.. code:: bash

    npm install

Run interactive installation:

.. code:: bash

    ./nodebb setup

You may leave all of the options as default, except "Which database to use (mongo)", which you should answer with "redis"

And you're done! After the installation, run

.. code:: bash

    ./nodebb start

You can visit your forum at ``http://localhost:4567/``


